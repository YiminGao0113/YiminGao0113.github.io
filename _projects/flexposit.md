---
title: "FlexPosit"
collection: projects
order: 1
permalink: /projects/flexposit
tagline: "Precision as a continuously tunable hardware resource"
status: "MICRO 2026"
keywords: ["posit arithmetic", "LLM inference", "mixed-precision quantization", "bit-serial systolic array"]
excerpt: "Mixed-precision quantization gives you rich tradeoffs in software, then wrecks the regular dataflow accelerators depend on. FlexPosit gets both."
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

Our insight is to stop treating precision as a fixed property of the datapath and
start treating it as a **tunable fractional hardware resource** — a knob that
trades accuracy, throughput, and energy on demand. FlexPosit realizes that with
algorithm-hardware co-design built on posit arithmetic.

Both halves
======

**Algorithm side:** a distribution-aware, hardware-aligned mixed-precision
quantization scheme that jointly decides per-channel scaling and
sensitivity-guided precision allocation. Jointly matters — these two decisions
constrain each other, and picking them separately leaves accuracy behind.

**Architecture side:** a unified bit-serial systolic array with lightweight
per-column decoders and a global precision controller. It tunes precision
continuously from 4 to 8 bits while keeping the systolic dataflow fully regular —
precision scales *temporally*, per GEMM kernel, so it never introduces spatial
irregularity into the array. That's what makes the software flexibility survive
contact with hardware instead of being flattened out by it.

I led the design and verification of the array in Verilog, and built a custom
cycle-accurate simulator with integrated memory and energy modeling (CACTI,
Ramulator) to check architectural decisions against end-to-end inference behavior
rather than against peak numbers.

What it gets you
======

FlexPosit reaches near-FP16 accuracy at **sub-5-bit average weight precision**. At
matched accuracy, it delivers up to **1.8× higher throughput** and **2× lower
energy** than state-of-the-art LLM inference accelerators, evaluated across LLaMA,
OPT, Phi, and Yi.

*To appear at the IEEE/ACM International Symposium on Microarchitecture
(MICRO) 2026. Work with L. Dai, J. Yin, X. Guo, and M. R. Stan.*
