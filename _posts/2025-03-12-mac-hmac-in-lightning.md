---
layout: post
title: "How Lightning nodes trust each other: MAC and HMAC, simply explained"
description: "Where MAC and HMAC live in Lightning — message transport, onion routing, channels — and why they stop attackers from rewriting payments."
tags: [lightning, seminar, cryptography]
lang: en
---

If anyone could rewrite messages between Lightning nodes, payments would fall apart. I dug into where MAC and HMAC actually sit in the protocol, and why they matter. Here is the plain-English version.

## Where are MAC and HMAC implemented in the Lightning Protocol?

Let's start with the basics first.

### What are MAC and HMAC?

MAC stands for Message Authentication Code. It is a tag we use to prove that the message we are sending is authentic — not altered — and that it came from the right sender.
A MAC is a one-way function, meaning that it is easy to compute the MAC of a message, but it is hard to compute the message from the MAC.

Let's take an example without and with a MAC.

- *Without a MAC*

In this context, we have two nodes, Olaniran and John. Since we have an open channel, we have a way to communicate between us. Actually `Olaniran` can send a message to John, and he can respond back to `Olaniran`.

Our current configuration looks like:

![img1]({{ '/assets/images/lpd/topic-002-init.png' | relative_url }})

In this case, we are exposed to rewriting attacks, where an attacker node can intercept the message and rewrite it. This is a problem because we can't be sure if the message is authentic or not.

![img2]({{ '/assets/images/lpd/topic-002-img1.png' | relative_url }})

- *With a MAC*

To prevent this, we are going to add a kind of tag to the message. This tag is called a MAC (Message Authentication Code).

![mac]({{ '/assets/images/lpd/topic-002-img2.png' | relative_url }})
![mac]({{ '/assets/images/lpd/topic-002-img22.png' | relative_url }})

But another problem remains: how do we ensure that we pass the message and the key K in the right order so that our partner can verify the authenticity and integrity of our message?

Since `MAC(message, key)` is different from `MAC(key, message)`, we have to define an order to create the MAC tag.

![mac-msg-key-order]({{ '/assets/images/lpd/topic-002-img3.png' | relative_url }})

At this point, we can introduce `HMAC, which is a MAC implementation based on hash functions`.

![hmac-msg-key-order]({{ '/assets/images/lpd/topic-002-img4.png' | relative_url }})

HMAC is now here to provide:

- More privacy
- Message integrity and authenticity
- Key integrity and authenticity

## Why and where?

From this we can conclude that MAC and HMAC are essentially used to prove the authenticity of communications and messages between nodes.

In Lightning, it covers:

- Message transport
- Onion routing
- Payment channels (channel state)
- Hashed Timelock Contracts (HTLCs)
