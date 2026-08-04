---
title: "CryptoPUF"
collection: projects
order: 5
permalink: /projects/cryptopuf
tagline: "A weak PUF and a crypto core, each covering the other's weakness"
accent: "#ef4444"
status: "IEEE RFID-TA 2024 · GF12 tapeout ongoing"
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

<figure class="project-figure">
<svg viewBox="0 0 680 240" role="img" aria-labelledby="pf-cp-t pf-cp-d">
  <title id="pf-cp-t">The weak PUF never reaches the attacker</title>
  <desc id="pf-cp-d">A challenge enters a cryptographic core, which draws its key from a weak PUF held behind a boundary. Only the challenge and the crypto core's response are observable, so a machine-learning attacker never sees the PUF's own analog mapping.</desc>

  <rect class="pf-box" x="34" y="58" width="118" height="52"/>
  <text class="pf-text" x="93" y="80" text-anchor="middle">Weak PUF</text>
  <text class="pf-text-sm" x="93" y="98" text-anchor="middle">fabrication variation</text>

  <path class="pf-accent-line" d="M152 84 L214 84"/>
  <path class="pf-accent-line" d="M207 78 L214 84 L207 90"/>
  <text class="pf-text-ac" x="183" y="72" text-anchor="middle">key</text>

  <rect class="pf-accent" x="216" y="46" width="150" height="76" opacity="0.16"/>
  <rect class="pf-box"    x="216" y="46" width="150" height="76"/>
  <text class="pf-text" x="291" y="78" text-anchor="middle">Crypto core</text>
  <text class="pf-text-sm" x="291" y="98" text-anchor="middle">not ML-learnable</text>

  <path class="pf-line-soft" d="M18 138 L378 138 L378 30 L18 30 Z" stroke-dasharray="5 4"/>
  <text class="pf-text-sm" x="24" y="156">on chip — never exposed</text>

  <path class="pf-accent-line" d="M366 84 L470 84"/>
  <path class="pf-accent-line" d="M463 78 L470 84 L463 90"/>
  <text class="pf-text-ac" x="418" y="72" text-anchor="middle">response</text>

  <rect class="pf-box" x="472" y="58" width="176" height="52"/>
  <text class="pf-text" x="560" y="80" text-anchor="middle">Attacker collects CRPs</text>
  <text class="pf-text-sm" x="560" y="98" text-anchor="middle">LR · SVM · MLP</text>

  <text class="pf-text-ac" x="560" y="150" text-anchor="middle">~50% prediction accuracy</text>
  <text class="pf-text-sm" x="560" y="170" text-anchor="middle">no better than guessing</text>

  <text class="pf-text-sm" x="340" y="212" text-anchor="middle">Read the other way: a crypto core with an intrinsic key, so nothing has to be stored on chip.</text>
</svg>
<figcaption>The crypto core shields the weak PUF from direct exposure while multiplying the number of usable challenge–response pairs.</figcaption>
</figure>

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

Follow-on silicon is currently being taped out in GlobalFoundries 12nm.

*Published at the IEEE International Conference on RFID Technology and
Applications (RFID-TA), 2024. Work with J. Chilaka, E. Pantoja, R. Klenke, and
M. R. Stan.*
