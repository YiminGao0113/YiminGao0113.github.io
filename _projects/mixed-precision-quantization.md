---
title: "Edge-MPQ"
collection: projects
order: 3
permalink: /projects/edge-mpq
tagline: "Mixed-precision inference units built into a RISC-V pipeline, and a search that knows what the hardware can do"
accent: "#3b82f6"
status: "IEEE Transactions on Computers 2024"
keywords: ["mixed-precision quantization", "RISC-V", "ISA co-design", "INT2–INT8", "14nm"]
excerpt: "Layer-wise mixed precision beats uniform quantization — but the search has to know what the hardware supports, and the hardware has to actually support it."
---

Layer-wise mixed-precision quantization strikes a better accuracy-efficiency
balance than giving every layer the same bitwidth. The catch is that existing MPQ
strategies tend to either ignore hardware entirely or cost so much to run that you
can't deploy them at the edge. And researchers usually commit up front to either
post-training quantization or quantization-aware training, based on the target
bitwidth or the hardware, and then live with that choice.

Edge-MPQ attacks both halves.

The hardware
======

Versatile MPQ inference units supporting **INT2–INT8 and INT16**, built on a
hierarchical multiplier architecture and integrated tightly into a RISC-V
processor pipeline through micro-architecture and ISA co-design. The underlying
move is re-architecting a conventional 16-bit integer multiplier into a SIMD
mixed-precision dot-product unit via hardware reuse and shift-add composition —
so the low-precision modes reuse the same silicon rather than demanding their own.

<figure class="project-figure">
<svg viewBox="0 0 680 220" role="img" aria-labelledby="pf-mpq-t pf-mpq-d">
  <title id="pf-mpq-t">One multiplier, reconfigured by precision</title>
  <desc id="pf-mpq-d">The same 16-bit multiplier array shown in three modes: one INT16 lane, two INT8 lanes, or eight INT2 lanes, obtained by hardware reuse and shift-add composition rather than separate units.</desc>

  <text class="pf-text-hd" x="340" y="28" text-anchor="middle">The same silicon, recomposed</text>

  <text class="pf-text-sm" x="20" y="76">INT16</text>
  <rect class="pf-box" x="80" y="56" width="560" height="28"/>
  <text class="pf-text-sm" x="360" y="75" text-anchor="middle">1 lane</text>

  <text class="pf-text-sm" x="20" y="124">INT8</text>
  <rect class="pf-fill-strong" x="80"  y="104" width="276" height="28"/>
  <rect class="pf-fill-strong" x="364" y="104" width="276" height="28"/>
  <rect class="pf-box" x="80" y="104" width="276" height="28"/>
  <rect class="pf-box" x="364" y="104" width="276" height="28"/>
  <text class="pf-text-sm" x="360" y="123" text-anchor="middle">2 lanes</text>

  <text class="pf-text-sm" x="20" y="172">INT2</text>
  <g>
    <rect class="pf-accent" x="80"  y="152" width="62" height="28"/>
    <rect class="pf-accent" x="150" y="152" width="62" height="28"/>
    <rect class="pf-accent" x="220" y="152" width="62" height="28"/>
    <rect class="pf-accent" x="290" y="152" width="62" height="28"/>
    <rect class="pf-accent" x="360" y="152" width="62" height="28"/>
    <rect class="pf-accent" x="430" y="152" width="62" height="28"/>
    <rect class="pf-accent" x="500" y="152" width="62" height="28"/>
    <rect class="pf-accent" x="570" y="152" width="70" height="28"/>
  </g>
  <text class="pf-text-sm" x="360" y="200" text-anchor="middle">8 lanes — hardware reuse and shift–add composition, not eight separate units</text>
</svg>
<figcaption>A conventional 16-bit integer multiplier, re-architected so the low-precision modes reuse the same silicon instead of demanding their own.</figcaption>
</figure>

Synthesized in **14nm**, it delivers **15.5×–47.7×** speedup over the baseline
RV64IMA core on a single convolution layer kernel, reaching **2.86 GOPS** and
**20.51 TOPS/W** — ahead of contemporary state-of-the-art edge MPQ hardware.

The search
======

Alongside it, an MPQ search algorithm that folds in both hardware awareness and
*training necessity* — whether a given layer actually needs QAT or can get away
with PTQ, rather than deciding once for the whole network. It samples layer-wise
sensitivities using a set of new metrics and runs a heuristic search, landing
**2.2%–6.7%** higher inference accuracy than state-of-the-art MPQ strategies under
comparable hardware constraints.

Expanding the search space with a dynamic programming strategy — finer-grained
accuracy intervals and multi-dimensional search — adds a further **1.3%+** over
greedy search.

*Published in IEEE Transactions on Computers, 2024, with earlier design space
exploration at GLSVLSI 2023. Work with X. Zhao, R. Xu, V. Verma, M. R. Stan, and
X. Guo.*
