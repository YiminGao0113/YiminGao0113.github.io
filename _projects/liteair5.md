---
title: "LiteAIR5"
collection: projects
order: 4
permalink: /projects/liteair5
tagline: "An AI-extended RISC-V core, and the end-to-end framework to design one"
status: "IEEE SOCC 2023"
keywords: ["RISC-V", "ISA extensions", "SoC generation", "FPGA emulation", "edge AI"]
excerpt: "Traditional edge AI hardware either isn't fast enough or costs too much power and area. A third option needs tooling that sees the whole system."
---

Machine learning at the edge has outgrown what general-purpose embedded cores can
do, but the usual alternatives aren't satisfying either: traditional edge AI
hardware tends to either fall short on performance or pay for its performance in
power and area.

LiteAIR5 starts from a RISC-V core with ISA extensions aimed at the workloads that
actually matter, reaching up to **37× speedup on a GEMM kernel** over a baseline
RISC-V core — largely by cutting instruction count and memory traffic rather than
by brute force. I built it inside a full FPGA-based SoC on an open-source
platform, evaluated under the tight memory constraints a real embedded system
imposes rather than in a vacuum.

The framework
======

The core is the demonstration; the framework is the point. LiteAIR5 covers
system-level modeling of ISA-extended RISC-V cores, SoC generation, compiler
support, and FPGA emulation — end to end.

That matters because adding an accelerator to a core is never a local change. A
new instruction shifts memory traffic, pipeline pressure, and the software stack
all at once, and the question you actually care about — is this worth the area? —
can't be answered by looking at the datapath alone. LiteAIR5 lets you develop
optimized AI hardware while seeing the effects ripple through the whole system.

*Published at the IEEE International System-on-Chip Conference (SOCC), 2023. Work
with S. Mosanu, M. N. Sakib, V. Verma, X. Guo, and M. R. Stan.*
