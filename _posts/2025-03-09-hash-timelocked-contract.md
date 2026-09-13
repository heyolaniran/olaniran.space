---
layout: post
title: "HTLCs explained: how Lightning moves money without trust"
description: "What is a Hash Timelocked Contract? I explain how Lightning routes a payment across channels with hashes and timeouts — no need to trust middlemen."
tags: [lightning, seminar, htlc]
lang: en
---

I kept hearing "HTLC" and nodding along — until I had to explain it myself. Here is the simple version I wish someone gave me: how Lightning moves sats across people you don't trust, using a hash and a deadline.

## What is an HTLC?

A Hash Timelocked Contract is basically a contract between two entities (nodes) in the Lightning Network. This contract says:

If you are able to prove to me you made a payment of `X satoshis` with a secret which hashes to this `Hash` before `X units of time`, you can spend these `Y >= X satoshis`, otherwise, I'll get back my funds.

Let's take an example to understand this better.
Let's say I want to send 2300 sats to Fadi but I do not have an open channel with her.

I have an open channel with Ariel and have `10_998 sats` as channel capacity. By the `pathfinding` algorithm, I found the shortest path to Fadi through Ariel.

Our actual configuration looks like:

![Pathfinding]({{ '/assets/images/lpd/topic-001-htlc-pathfinding.png' | relative_url }})

## How does an HTLC work in that configuration?

To send some sats to Fadi I need to get an invoice from her, maybe through her blog or when she sends it to me. The invoice will contain the following information: `amount`, `hash` and `expiration`.

![invoice]({{ '/assets/images/lpd/topic-001-htlc-img1.png' | relative_url }})

Let's focus on the `hash` part. The hash is a hash of the secret which will be used to prove the payment.

Since I use this route found by pathfinding, we will now call it a `routed payment`, with the route: `I -> Ariel -> Velia -> Fadi`

I need to make a contract with Ariel to send 2300 sats to Fadi that says:

If he is able to prove he successfully made this transfer with 30s left, he can spend the 3000 sats we both signed in a 2-of-2 multisig address, otherwise I will get back my funds.

In turn, `Ariel` will sign a contract with `Velia` to send `2300 sats to Fadi`, and if she is able to prove she successfully made this transfer with `20s left`, she can spend the `2700 sats` they both signed in a 2-of-2 multisig address, otherwise Ariel will get back his funds.

Then `Velia` will sign a contract with `Fadi` that says:

You can spend the `2300 sats` we both signed in a 2-of-2 multisig address if you give me the secret which hashes to `hash` with `10s left`, otherwise I will get back my funds.

![HTLCs]({{ '/assets/images/lpd/topic-001-img2.png' | relative_url }})

## HTLC successful case

Once we have established an HTLC between Fadi and an intermediate node, Velia in our case, if Fadi gives her secret (unique) for this payment hash to Velia before the expiration time, she will be able to spend the `2300 sats`. She successfully received our satoshis.

In turn, Velia will give the secret to Ariel before the expiration time, he will be able to spend, and so on... `We move backward with the secret from Fadi to me`.

![success]({{ '/assets/images/lpd/topic-001-htlc-img2.png' | relative_url }})

## HTLC failure case

For any reason, if some node is unable to fulfill its HTLC contract, primarily:

- Every node will get back its own funds
- And all failed HTLCs make the payment fail too.

```
This is the atomicity of the HTLC. If one node fails to complete the HTLC, the entire payment fails.
```

![FAILURES]({{ '/assets/images/lpd/topic-001-htlc-img3.png' | relative_url }})

## Do I need to trust the following nodes?

No, you don't need to trust the nodes in the path. The HTLC is a trust mechanism: thanks to the 2-of-2 multisig address you lock the funds in, your partner cannot spend your funds without your validation.

As Lightning is a punishment-based system, cheaters risk losing their entire funds in the payment channel used.

HTLCs ensure trustlessness in that way.

## What do participants gain?

Remember that the HTLC is a mechanism to ensure the payment is atomic. The participants gain the following:

- **Security**: the payment is secure, even if one node fails to complete the HTLC,
- **Atomicity**: the payment is atomic, even if one node fails to complete the HTLC,
- **Trustlessness**: the payment is trustless, you don't need to trust the nodes.

And if you remember well, `the Y amount in the HTLC definition is greater than or equal to the amount they have to send. So they do not lose money.`

They can be rewarded with some extra sats we will call here — some routing fees.
