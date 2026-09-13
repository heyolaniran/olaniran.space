---
layout: post
title: "Why Lightning payments fail — and what happens next"
description: "Dead channels, low capacity, wrong fees, expired HTLCs: the real reasons Lightning payments fail, with examples from routing a payment."
tags: [lightning, seminar, routing]
lang: en
---

A Lightning payment can die for boring reasons — a node went offline, a channel ran dry, a fee was too low. I collected the failure modes I kept running into, so you can recognize them faster than I did.

## Channel disabled

To make a payment in the Lightning Network we need a channel that we can use to transfer data between two or more partners (routing payments).
Since the Lightning Protocol is a hot system which requires all concerned nodes to be online to process an operation (unlike Bitcoin):

```
The fact that (i.e. in a routing payment),
any channel can go offline during the payment can be a cause of failure in that payment processing.
```

![Channel Disabled]({{ '/assets/images/lpd/topic-003-img1.png' | relative_url }})

## Temporarily disabled channel

Temporarily disabling a channel is similar to our previous cause: channel disabled.

```
In this case it is marked as temporary, so the node might come back online soon and the channel will be available again (i.e. hardware maintenance).
```

![Temporarily Channel Disabled]({{ '/assets/images/lpd/topic-003-img2.png' | relative_url }})

## Permanent node failure

This is the most severe failure in the Lightning Protocol.

```
Firstly, Lightning doesn't have an explicit notion of wallet and backup. For this reason, if your node goes down for any reason, there is a chance you could lose most of your funds.

From another point of view, every other node that had a channel with you will see its funds locked in the channel for a certain time (the to_self_delay property).
```

![Permanent channel disabled]({{ '/assets/images/lpd/topic-003-img3.png' | relative_url }})

## Insufficient channel capacity

This is the most common source of failure in a payment channel.

```
That means the channel doesn't have enough funds to process the payment.
```

Let's say we want to pay a 25_000-sat invoice.
We have opened a channel with enough capacity (`1_000_000 sats`) with node B,
and node B has opened a channel with `20_000 sats` to our destination.

`20_000 sats is less than 25_000 sats, so node B doesn't have enough satoshis to forward our payment to node C.`

![channel capacity]({{ '/assets/images/lpd/topic-003-img4.png' | relative_url }})

## Incorrect payment details

This is a common cause of payment failure between two people.

```
It occurs when, in a payment — routing payment — channel, the recipient gets the wrong hash or amount instead of the ones expected.
```

## Insufficient payment fees

The fee set is not enough for a node to process a payment. This can be fixed by increasing the fee for the payment.

![insufficient_fee]({{ '/assets/images/lpd/topic-003-img5.png' | relative_url }})

## Expired HTLC

In the Lightning Network, the Hash Timelocked Contract is one of the most resilient mechanisms to handle complex routing payment failures.

```
If the payment is not processed before the HTLC timeout expires, the payment fails and the funds are refunded to each owner in the routing payment system.
```

You can read more about [HTLCs here]({% post_url 2025-03-09-hash-timelocked-contract %}).

![HTLC_timeout]({{ '/assets/images/lpd/topic-001-htlc-img3.png' | relative_url }})

## Required node feature missing

This failure occurs when a payment requires a specific protocol feature that a node in the routing path doesn't support.

The `Required Node Feature Missing` error in the Lightning Network is an important but relatively technical routing failure.

```
When a Lightning Network payment is being routed, it needs to pass through multiple nodes to reach its destination.
Each node might support different features or capabilities, as the Lightning Network protocol has evolved over time with various upgrades and improvements.
```

For example:

- Multi-part payments (MPP) require nodes to understand how to handle payment fragments
- HODL invoices require specific timelock handling
- TLV (Type-Length-Value) extension fields for additional payment data
- Anchor outputs for more flexible fee management
- Newer hash functions or cryptographic primitives

`This can result from incompatibilities between the versions of the Lightning implementations run by nodes.`

![RNF]({{ '/assets/images/lpd/topic-003-img6.png' | relative_url }})
