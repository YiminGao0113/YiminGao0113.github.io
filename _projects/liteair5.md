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

<figure class="project-figure">
<svg viewBox="0 0 680 200" role="img" aria-labelledby="pf-la-t pf-la-d">
  <title id="pf-la-t">The LiteAIR5 framework loop</title>
  <desc id="pf-la-d">Four stages in sequence — system-level modeling, SoC generation, compiler support, and FPGA emulation — with measurements feeding back from emulation to modeling.</desc>

  <rect class="pf-box" x="14"  y="56" width="140" height="58"/>
  <text class="pf-text" x="84"  y="80" text-anchor="middle">System-level</text>
  <text class="pf-text" x="84"  y="98" text-anchor="middle">modeling</text>

  <rect class="pf-box" x="184" y="56" width="140" height="58"/>
  <text class="pf-text" x="254" y="80" text-anchor="middle">SoC</text>
  <text class="pf-text" x="254" y="98" text-anchor="middle">generation</text>

  <rect class="pf-box" x="354" y="56" width="140" height="58"/>
  <text class="pf-text" x="424" y="80" text-anchor="middle">Compiler</text>
  <text class="pf-text" x="424" y="98" text-anchor="middle">support</text>

  <rect class="pf-accent" x="524" y="56" width="142" height="58" opacity="0.16"/>
  <rect class="pf-box"    x="524" y="56" width="142" height="58"/>
  <text class="pf-text" x="595" y="80" text-anchor="middle">FPGA</text>
  <text class="pf-text" x="595" y="98" text-anchor="middle">emulation</text>

  <g class="pf-accent-line">
    <path d="M154 85 L182 85"/><path d="M175 79 L182 85 L175 91"/>
    <path d="M324 85 L352 85"/><path d="M345 79 L352 85 L345 91"/>
    <path d="M494 85 L522 85"/><path d="M515 79 L522 85 L515 91"/>
  </g>

  <path class="pf-line" d="M595 118 L595 152 L84 152 L84 120"/>
  <path class="pf-line" d="M78 127 L84 120 L90 127"/>
  <text class="pf-text-sm" x="340" y="170" text-anchor="middle">measured effects feed back into the model — the whole system, not just the datapath</text>

  <text class="pf-text-sm" x="14" y="36">an ISA extension changes memory traffic, pipeline pressure, and the software stack at once</text>
</svg>
<figcaption>Adding an accelerator to a core is never a local change, so the framework closes the loop rather than stopping at the datapath.</figcaption>
</figure>


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
