---
title: "CryptoPUF"
collection: projects
order: 5
permalink: /projects/cryptopuf
tagline: "A weak PUF and a crypto core, each covering the other's weakness"
status: "IEEE RFID-TA 2024"
keywords: ["hardware security", "PUF", "ML-resilient", "IoT", "RFID"]
excerpt: "Strong PUFs fall to machine learning. Crypto cores resist ML but have no intrinsic key. Put them together and each one's weakness is the other's strength."
---

IoT security has an awkward economics problem: the devices that most need
protecting — battery-powered sensors, UHF RFID tags — are the ones with the least
area and energy to spend on it. Physical unclonable functions are an appealing
answer, since they derive a unique "digital fingerprint" from fabrication
variation rather than from a key you have to store.

The problem is that machine learning got good. Modern ML models can learn the
challenge-response behavior of conventional strong PUFs from collected CRPs, which
defeats the point. Cryptographic algorithms don't have this weakness — you can't
regress your way through a block cipher — but they have the opposite one: no
intrinsic key, so you're back to storing secrets on chip.

CryptoPUF puts a **weak PUF together with a cryptographic encryption core** so each
covers for the other. Read one way, it's a crypto-enhanced PUF: the crypto core
shields the weak PUF from direct exposure while massively expanding the number of
usable CRPs. Read the other way, it's a PUF-enhanced crypto core with intrinsic key
generation, which removes the need for on-chip key storage entirely.

Against Logistic Regression, Support Vector Machine, and Multilayer Perceptron
attacks it holds at **near-ideal 50% prediction accuracy** — attackers do no better
than guessing — while keeping resource utilization low. Compared to published
alternatives, it's the **most compact ML-resilient PUF** we're aware of.

Reliability
======

A PUF is only useful if it gives the same answer every time, across temperature
and voltage corners and over the device's life, and raw PUF bits don't. My related
circuit work designs delay-based CMOS PUFs at the transistor level with Monte
Carlo variability analysis, and screens for the cells that stay stable — cheaply,
and in a fully digital way.

*Published at the IEEE International Conference on RFID Technology and
Applications (RFID-TA), 2024. Work with J. Chilaka, E. Pantoja, R. Klenke, and
M. R. Stan.*
