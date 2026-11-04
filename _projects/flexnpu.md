---
title: "FlexNPU"
collection: projects
order: 2
permalink: /projects/flexnpu
redirect_from:
  - /projects/edgescope
tagline: "An open, end-to-end NPU research platform, from PyTorch to RTL on an FPGA"
status: "Running end-to-end on FPGA · open-source release planned"
keywords: ["NPU", "RISC-V", "systolic array", "vector unit", "MLIR / IREE", "PyTorch", "custom quantization", "cycle-accurate simulation"]
excerpt: "An NPU that keeps ML operators off the host CPU: a matrix engine for GEMM, a vector unit for reductions, and a RISC-V core for the rest, with one flow from PyTorch down to RTL on an FPGA."
featured: true
---

An NPU is only as fast as the operators it can't run. Every operator that falls
back to the host CPU costs a round trip: data out to the CPU, compute on a core
that was never meant for it, data back. On an edge SoC, those fallbacks can end
up dominating the whole model.

FlexNPU's goal is to run the full ML operator set on the accelerator, so a model
never has to go back to the CPU. The other goal is to expose the whole stack,
from the PyTorch model down to the RTL, so other researchers can build on it.

Full operator coverage
======

Each class of operator has a home on the NPU.

<figure class="project-figure">
<svg viewBox="0 0 680 300" role="img" aria-labelledby="pf-cov-t pf-cov-d">
  <title id="pf-cov-t">Every operator class maps to a unit on the NPU</title>
  <desc id="pf-cov-d">Three operator classes on the left map to three units inside the NPU: GEMM and convolution to the matrix engine, reductions such as softmax and normalization to the vector unit, and everything else to the RISC-V core. The host CPU is drawn faded at the bottom with a crossed-out fallback path.</desc>

  <text class="pf-text-hd" x="20" y="34">ML operators</text>
  <rect class="pf-fill" x="20" y="50"  width="190" height="44" rx="4"/>
  <text class="pf-text" x="34" y="77">GEMM · convolution</text>
  <rect class="pf-fill" x="20" y="110" width="190" height="44" rx="4"/>
  <text class="pf-text" x="34" y="137">softmax · norms · reductions</text>
  <rect class="pf-fill" x="20" y="170" width="190" height="44" rx="4"/>
  <text class="pf-text" x="34" y="197">control · everything else</text>

  <rect class="pf-box" x="330" y="20" width="330" height="214" rx="6"/>
  <text class="pf-text-hd" x="346" y="42">FlexNPU</text>
  <rect class="pf-accent" x="370" y="50"  width="270" height="44" rx="4" opacity="0.9"/>
  <rect class="pf-accent" x="370" y="110" width="270" height="44" rx="4" opacity="0.65"/>
  <rect class="pf-accent" x="370" y="170" width="270" height="44" rx="4" opacity="0.45"/>
  <text x="505" y="77"  text-anchor="middle" style="fill:#fff;font:700 12.5px 'Ubuntu Mono',monospace">matrix engine (systolic)</text>
  <text x="505" y="137" text-anchor="middle" style="fill:#fff;font:700 12.5px 'Ubuntu Mono',monospace">vector unit (reduction path)</text>
  <text x="505" y="197" text-anchor="middle" style="fill:#fff;font:700 12.5px 'Ubuntu Mono',monospace">RISC-V core</text>

  <path class="pf-accent-line" d="M214 72 L362 72"/><path class="pf-accent-line" d="M354 66 L362 72 L354 78"/>
  <path class="pf-accent-line" d="M214 132 L362 132"/><path class="pf-accent-line" d="M354 126 L362 132 L354 138"/>
  <path class="pf-accent-line" d="M214 192 L362 192"/><path class="pf-accent-line" d="M354 186 L362 192 L354 198"/>

  <rect class="pf-box" x="20" y="250" width="190" height="34" rx="4" stroke-dasharray="4 4" opacity="0.3"/>
  <text class="pf-text-sm" x="115" y="271" text-anchor="middle">host CPU</text>
  <path class="pf-line-soft" d="M330 230 L214 262" stroke-dasharray="4 4"/>
  <path class="pf-accent-line" d="M264 236 L280 256 M280 236 L264 256"/>
  <text class="pf-text-ac" x="300" y="280">no fallback</text>
</svg>
<figcaption>GEMM goes to the matrix engine, reductions to the vector unit, and the rest to the RISC-V core, so nothing has to go back to the host CPU.</figcaption>
</figure>

The **matrix engine** is a systolic array for GEMM and convolution. The **vector
unit** provides the reduction path, for operators like softmax and normalization.
A **RISC-V core** inside the NPU handles control and the remaining operators that
fit neither. Data moves through on-chip scratchpad memory with dedicated load and
store DMA engines.

Several ML models already run end-to-end on the FPGA. Coverage isn't at 100% yet,
and closing that gap is the current work.

From PyTorch to RTL
======

FlexNPU is one flow, not a hardware demo and a software demo side by side. A
**PyTorch front end** feeds custom **MLIR/IREE** passes that lower each operator
onto its unit. A C/C++ runtime on the Zynq's ARM host launches the compiled program.
The design itself is RTL running on a Xilinx Kria KV260. **Custom quantization**
is supported through the whole flow.

The compiler reaches the hardware through a register and DMA interface rather
than a fixed tile size. You can swap an RTL datapath variant without rebuilding
the compiler or recompiling the model, so a single design change can be measured
end-to-end in isolation.

Built to be tuned
======

The platform exposes knobs at every layer, and it lets you see what they do:

- **Hardware performance counters** measure compute and data movement inside the
  NPU in real time, on the board.
- A **cycle-accurate simulator** models the same architecture, so you can sweep
  the design space without building every configuration in hardware.

NPU design space exploration
======

With counters on the board and a simulator next to it, FlexNPU supports design
space exploration of the whole NPU and its host. Tools like Timeloop and MAESTRO
model the accelerator in isolation and leave the host out. One thing whole-system
exploration shows: growing the matrix engine can shift the bottleneck somewhere
else, so the best use of area interleaves sizing the array with widening operator
coverage.

*Running end-to-end on FPGA. Ongoing project; open-source release planned.*
