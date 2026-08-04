---
title: "FlexNPU & EdgeScope"
collection: projects
order: 2
permalink: /projects/edgescope
tagline: "A full-stack FPGA NPU platform, and host-aware design space exploration built on top of it"
status: "Platform in silicon · DSE tool in submission"
keywords: ["NPU", "MLIR / IREE", "compiler and runtime", "design space exploration", "host bottleneck"]
excerpt: "An end-to-end accelerator platform — compiler backend, runtime, RTL — plus a DSE tool that treats the host CPU as part of the design space instead of ignoring it."
---

FlexNPU
======

FlexNPU is an end-to-end AI accelerator platform I built on a Xilinx Kria KV260
(Zynq SoC). End-to-end meaning genuinely all of it: a custom compiler backend, a
custom C/C++ runtime, and a double-buffered RTL shell with AXI DMA.

On the compiler side, custom MLIR/IREE passes lower ML operators — GEMM, softmax,
depthwise convolution — onto the accelerator slots. On the system side, an
ARM-host runtime plus a register and DMA interface that can swap RTL tiles
**without recompiling the model**. That last property is what makes the platform
useful for anything beyond a single demo: the compiled binary binds to the slot
contract rather than to a particular tile size.

It reaches up to **31× end-to-end speedup on MobileBERT INT8** over the on-chip ARM
CPU.

EdgeScope
======

Once you can swap hardware configurations without touching the binary, you can
measure each design change end-to-end in isolation — nothing else moves. That
turns the platform into a measurement apparatus, and EdgeScope is the design space
exploration tool built on it.

The problem EdgeScope addresses is that existing DSE tools — Timeloop, MAESTRO,
roofline analysis — model the accelerator in isolation, compute against memory,
with the host CPU outside the design space entirely. On an edge NPU that's a bad
assumption. The host sequences the accelerator through a compiled operator stream
and does real per-operator work along the way, and on many workloads that host
work is what actually sets the wall. It isn't that these tools weigh the host
wrongly; they structurally cannot represent it. The practical consequence is that
they can recommend spending silicon on a bigger array for a workload that was
never compute-bound to begin with.

EdgeScope treats the host as a first-class resource alongside compute, memory, and
dispatch, and allocates a fixed area budget across two coupled axes: **sizing**,
making the operators you already offload run faster, and **coverage**, moving whole
operator classes onto the accelerator to relieve the host.

Grow, then cover
------

Those axes don't decompose, which is the interesting part. Start small on a
transformer workload and it's compute-bound, so growing the array is right and a
coverage unit would buy nothing. Grow it far enough and the bottleneck **flips to
the host** — the CPU-side work was there all along, just hidden behind compute. Now
the coverage unit, worthless a few steps earlier, becomes the best remaining spend.

Explore either axis alone and you stop short. Array-alone runs into the host wall;
coverage-alone does nothing while compute is still binding. Only a loop that
watches the bottleneck *shift* finds "grow, then cover" — and the allocator finds
it on its own rather than being told. It also declines to spend when nothing helps,
from the same code path, with no special case.

*Platform running in silicon. DSE tool in submission.*
