---
title: "FlexPosit"
collection: projects
order: 1
permalink: /projects/flexposit
tagline: "Precision as a continuously tunable hardware resource"
accent: "#f59e0b"
status: "MICRO 2026 · GF12 tapeout ongoing"
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

Our insight is to stop treating precision as a width fixed at design time and start
treating it as a **tunable fractional hardware resource** — a knob, set at runtime,
that trades accuracy, throughput, and energy on demand. FlexPosit realizes that
with algorithm-hardware co-design built on posit arithmetic.

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

<figure class="project-figure">
<svg viewBox="0 0 680 250" role="img" aria-labelledby="pf-fp-t pf-fp-d">
  <title id="pf-fp-t">Precision scales in time, not in space</title>
  <desc id="pf-fp-d">A fixed systolic array feeds a timeline. Each layer occupies a span proportional to its bit width — four, six, five, eight, four bits — so cheaper layers finish sooner on the same unchanged array.</desc>

  <text class="pf-text-hd" x="20" y="34">One array, unchanged</text>
  <rect class="pf-box" x="20" y="48" width="120" height="120"/>
  <g class="pf-line-soft">
    <line x1="50" y1="48" x2="50" y2="168"/><line x1="80" y1="48" x2="80" y2="168"/>
    <line x1="110" y1="48" x2="110" y2="168"/>
    <line x1="20" y1="78" x2="140" y2="78"/><line x1="20" y1="108" x2="140" y2="108"/>
    <line x1="20" y1="138" x2="140" y2="138"/>
  </g>
  <text class="pf-text-sm" x="80" y="188" text-anchor="middle">bit-serial systolic array</text>
  <text class="pf-text-sm" x="80" y="204" text-anchor="middle">fully regular dataflow</text>

  <path class="pf-accent-line" d="M152 108 L192 108"/>
  <path class="pf-accent-line" d="M184 102 L192 108 L184 114"/>

  <text class="pf-text-hd" x="210" y="34">Time per layer = precision</text>
  <line class="pf-line" x1="210" y1="168" x2="660" y2="168"/>

  <rect class="pf-accent" x="210" y="96" width="60"  height="56"/>
  <text class="pf-text-sm" x="240" y="188" text-anchor="middle">4 bit</text>
  <rect class="pf-fill-strong" x="274" y="96" width="90" height="56"/>
  <text class="pf-text-sm" x="319" y="188" text-anchor="middle">6 bit</text>
  <rect class="pf-fill-strong" x="368" y="96" width="75" height="56"/>
  <text class="pf-text-sm" x="405" y="188" text-anchor="middle">5 bit</text>
  <rect class="pf-fill-strong" x="447" y="96" width="120" height="56"/>
  <text class="pf-text-sm" x="507" y="188" text-anchor="middle">8 bit</text>
  <rect class="pf-accent" x="571" y="96" width="60" height="56"/>
  <text class="pf-text-sm" x="601" y="188" text-anchor="middle">4 bit</text>

  <text class="pf-text-sm" x="210" y="82">layer 1</text>
  <text class="pf-text-sm" x="571" y="82">layer n</text>
  <text class="pf-text-sm" x="435" y="222" text-anchor="middle">Sensitive layers get more bits; the rest finish sooner. Average lands below 5.</text>
</svg>
<figcaption>Precision is spent in cycles rather than in silicon, so a layer that needs fewer bits simply takes less time — and the array never changes shape.</figcaption>
</figure>

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

The design is currently being taped out in GlobalFoundries 12nm.

*To appear at the IEEE/ACM International Symposium on Microarchitecture
(MICRO) 2026. Work with L. Dai, J. Yin, X. Guo, and M. R. Stan.*
