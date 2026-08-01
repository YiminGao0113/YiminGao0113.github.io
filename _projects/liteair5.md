---
title: "LiteAIR5"
collection: projects
order: 3
permalink: /projects/liteair5
tagline: "A system-level framework for designing and modeling AI-extended RISC-V cores"
status: "IEEE SOCC 2023"
keywords: ["RISC-V", "system-level modeling", "design space exploration", "AI extensions"]
excerpt: "Answering \"what happens if I bolt this accelerator onto a RISC-V core?\" without taping out to find out."
---

Adding AI acceleration to a RISC-V core sounds like a local decision and almost
never is. A new instruction or a tightly-coupled unit changes the memory traffic,
the pipeline pressure, and the software stack all at once, and the interesting
question — is this worth the area? — can't be answered by looking at the
accelerator in isolation.

LiteAIR5 is the framework I wanted to exist while trying to answer that question.
It models AI-extended RISC-V cores at the system level, so you can vary how the
acceleration is attached and see the consequences propagate through the whole
design rather than just the datapath you changed.

The point is to make the exploration cheap enough to actually do. Building one
configuration properly is expensive; comparing a dozen of them is what tells you
which one to build.

*Published at the IEEE International System-on-Chip Conference (SOCC), 2023. Work
with S. Mosanu, M. N. Sakib, V. Verma, X. Guo, and M. R. Stan.*
