---
title: "FlexPosit"
collection: projects
order: 1
permalink: /projects/flexposit
tagline: "Precision as a continuously tunable hardware resource"
status: "MICRO 2026 · GF12 test chip post-layout"
keywords: ["posit arithmetic", "LLM inference", "mixed-precision quantization", "bit-serial systolic array"]
excerpt: "Algorithm–hardware co-design that brings fine-grained mixed-precision quantization to LLM accelerators while preserving a regular systolic dataflow."
featured: true
---

Running an LLM at the edge, under a real compute and energy budget, asks for two
things at the same time. You want **precision tunability**, so you can land on the
right accuracy-efficiency point for whatever budget you've been handed. And you
want **high quantization accuracy** on the heavy-tailed, sensitivity-prone weight
distributions that modern LLMs actually have.

Those two rarely show up together. Mixed-precision quantization exposes genuinely
rich tradeoffs — in software. Push that fine-grained precision variation down into
hardware and it collides head-on with the regular dataflow that makes an
accelerator efficient in the first place. You can have the flexibility or you can
have the systolic array.

Our insight is to stop treating precision as a width fixed at design time and start
treating it as a **tunable fractional hardware resource** — a knob, set at runtime,
that trades accuracy, throughput, and energy on demand. FlexPosit realizes that
with algorithm-hardware co-design built on posit arithmetic.

Both halves
======

**Algorithm side:** a distribution-aware, hardware-aligned mixed-precision
quantization scheme. Each channel gets a power-of-two scale, chosen for maximum
SQNR, that shifts its weights onto the peak of posit's tapered precision —
applying it is an exponent add, not a multiply. Then the most sensitive channel
windows are upgraded from 4 to 5 bits until the bit budget is spent. Those
windows line up with array columns, so each tile still runs at one precision.

**Architecture side:** a unified bit-serial systolic array with lightweight
per-column decoders and a global precision controller. It tunes precision
continuously from 4 to 8 bits while keeping the systolic dataflow fully regular —
precision scales *temporally*, per GEMM kernel, so it never introduces spatial
irregularity into the array. That's what makes the software flexibility survive
contact with hardware instead of being flattened out by it.

The decoders run on **SerialPosit**, a sign-magnitude variant of posit with the
same value set. Conventional posit decoding needs a two's complement and a wide
leading-one detector; bit-serially, the regime boundary is a single XOR of
consecutive bits. Posit's main hardware drawback, its variable-length regime,
becomes a natural fit for a bit-serial datapath.

<figure class="project-figure project-figure--paper">
  <img src="/images/projects/flexposit/architecture.png"
       alt="FlexPosit architecture. (a) A weight buffer feeds one bit-serial posit decoder per column, each emitting a 5-bit weight-term stream into a grid of MAC clusters, with a rescale unit per column above the output buffer and a GPCU setting precision. (b) Gate-level circuit of the FlexPosit PE: an XOR for sign, shifters, muxes and a shared adder for exponent and mantissa. (c) Timing diagram: each PE processes one weight in P cycles, where P is the current precision."
       loading="lazy" width="1800" height="815">
  <figcaption>(a) Overall architecture: one bit-serial posit decoder per column, a regular grid of MAC clusters, and per-column rescale. (b) Gate-level PE. (c) Dataflow timing — each PE spends P cycles on a weight, so precision costs time, not area.</figcaption>
</figure>

I led the design and verification of the array in Verilog, and built a custom
cycle-accurate simulator with integrated memory and energy modeling (CACTI,
Ramulator 2.0) to check architectural decisions against end-to-end inference
behavior rather than against peak numbers.

What it gets you
======

FlexPosit reaches near-FP16 accuracy at **sub-5-bit average weight precision**.
Upgrading just 10% of weights to 5 bits (4.1 bits on average) cuts the accuracy
loss by more than half, and it matches BitMoD's 4-bit accuracy at 4.1–4.6 bits
while keeping hardware-friendly per-channel quantization.

At iso-area and iso-accuracy, synthesized in a commercial 16nm process, it runs
**1.8× faster with 1.2× less energy than BitMoD**, and **1.5× faster with 2.0×
less energy than OliVe**, with the lowest latency and energy across all nine
models evaluated. The posit decoders, rescale units, and precision controller
together cost under 2% of area and power.

<figure class="project-figure project-figure--paper">
  <img src="/images/projects/flexposit/pareto.png"
       alt="Perplexity versus normalized energy-delay product for GPT2-XL and Phi-2. FlexPosit's points at 4.1 to 5.0 bits form a curve in the lower left, below and left of BitMoD, OliVe a8w8, and OliVe a4w4."
       loading="lazy" width="1600" height="838">
  <figcaption>Perplexity against energy-delay product on GPT2-XL and Phi-2. Each green point is one bit budget between 4.1 and 5.0 bits; together they trace the lower-left Pareto frontier.</figcaption>
</figure>

Test chip
======

FlexPosit is being built as a test chip in GlobalFoundries 12nm, now
**post-layout**. The compute subsystem is a 16×16 FlexPosit array with sixteen
serial posit decoders, a global precision controller, and 26 KiB of on-chip
SRAM buffers. Precision and posit exponent size are both chosen per descriptor
at runtime — P from 4 to 8 bits, es from 0 to 2.

<figure class="project-figure">
  <img src="/images/projects/flexposit/layout.jpg"
       alt="Annotated post-layout view of the FlexPosit test chip. The 16 by 16 FlexPosit array fills most of the die. On the left are activation FIFOs and streamers above the SRAM buffers for activations, weights, scales and outputs, 26 KiB in total. Along the bottom are the SPI and registers, control, sixteen serial posit decoders, the global precision control unit, and ship-out. A scale bar marks 100 micrometers."
       loading="lazy" width="1400" height="1167">
  <figcaption>Post-layout view of the GF12 test chip. The array dominates the die; the decoders and precision control are a thin strip along the bottom.</figcaption>
</figure>

*To appear at the IEEE/ACM International Symposium on Microarchitecture
(MICRO) 2026.*
