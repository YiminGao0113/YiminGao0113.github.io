---
title: "CryptoPUF"
collection: projects
order: 4
permalink: /projects/cryptopuf
tagline: "A strong PUF that machine learning can't model, built from a weak one"
status: "IEEE RFID-TA 2024"
keywords: ["hardware security", "PUF", "ML-resilient", "RFID"]
excerpt: "Strong PUFs are convenient and breakable; weak PUFs are sturdy and inconvenient. This one tries to be both."
---

Physical unclonable functions turn manufacturing variation into an identity: same
design, same mask, subtly different silicon, and that difference becomes a key you
never have to store. It's a lovely idea, and it has an awkward problem.

*Strong* PUFs accept many challenges and are convenient for authentication — but
their challenge–response behavior is a function, and functions can be learned.
Feed a machine learning model enough challenge–response pairs and it will predict
the rest, which is exactly the attack the PUF was supposed to prevent. *Weak* PUFs
resist this nicely but only offer a handful of responses, which isn't enough to
authenticate with.

CryptoPUF gets the strong-PUF interface out of weak-PUF material. A weak PUF
supplies the device-unique secret, and a crypto core stands between that secret
and the outside world, so what an attacker collects is the output of a
cryptographic function rather than a learnable analog mapping. The modeling attack
loses its foothold.

The whole thing is built to stay small, because the devices that need this most —
RFID tags, embedded sensors — are exactly the ones with no area or power to spare.

*Published at the IEEE International Conference on RFID Technology and
Applications (RFID-TA), 2024. Work with J. Chilaka, E. Pantoja, R. Klenke, and
M. R. Stan.*
