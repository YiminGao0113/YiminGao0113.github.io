---
title: "Edge-MPQ"
collection: projects
order: 3
permalink: /projects/edge-mpq
tagline: "Mixed-precision inference units built into a RISC-V pipeline, and a search that knows what the hardware can do"
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
