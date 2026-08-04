---
title: "EdgeScope"
collection: projects
order: 2
permalink: /projects/edgescope
tagline: "Host-aware design space exploration for edge NPU systems"
status: "In submission"
keywords: ["NPU", "design space exploration", "FPGA", "host bottleneck", "IREE / MLIR"]
excerpt: "Existing DSE tools model the accelerator in isolation. On real edge workloads the host CPU is frequently what's actually setting the wall — a bottleneck those tools structurally cannot see."
---

On an edge NPU, the host CPU is not a spectator. It sequences the accelerator
through a compiled operator stream and does substantial per-operator work of its
own, and on real workloads that host work frequently dominates end-to-end latency.

Design space exploration tools don't see any of this. Timeloop, MAESTRO, roofline
analysis — they model the accelerator in isolation, compute against memory, with
the host outside the design space entirely. It isn't that they weigh the host
wrongly; they structurally cannot represent it.

That has consequences you can measure. Running the incumbent view as a fair
ablation of our own silicon-validated model, on **four of six** real workloads it
recommends spending area on a bigger array and more bandwidth, believes it is
buying roughly 4×, and delivers **1.00×** — the workloads were host-bound the whole
time. The confidence is genuine. The speedup is baseline.

EdgeScope models the host as a first-class resource alongside compute, memory, and
dispatch, and gets all six right.

Grow, then cover
======

EdgeScope explores two coupled axes: **sizing** (make the operators you already
offload run faster) and **coverage** (move whole operator classes onto the
accelerator to relieve the host). Given a fixed area budget, it allocates across
both automatically.

They don't decompose, and MobileBERT shows why. Start at a small array and the
model is compute-bound, so growing the array is the right move and a coverage unit
would buy nothing. Grow it, and at N=32 the bottleneck **flips to the host** — the
CPU-side rescale work was always there, just hidden behind compute. Now the rescale
unit, worthless three steps earlier, is the best remaining spend. Add it and the
wall drops again: **2.86×**, reachable only with both.

Explore either axis alone and you stop short. Array-alone runs into the host wall.
Coverage-alone does nothing while compute is still the bottleneck. Only a loop
watching the bottleneck *shift* finds "grow, then cover" — and the allocator finds
it rather than being told, discovering the configuration over four iterations.

It also knows when to spend nothing. On a workload where no amount of silicon
helps, it stops after one iteration and declines the budget, from the same code
path — no special case.

Grounded in silicon
======

EdgeScope is built on FlexNPU, an FPGA platform I developed on a Xilinx Kria
KV260, with slots on distinct microarchitectures — an output-stationary systolic
GEMM array, a LUT-based softmax unit, parallel MAC lanes for depthwise
convolution — and an IREE/MLIR compilation flow.

The property that makes it useful as a measurement apparatus is that portable
bytecode binds to the *slot contract* rather than to a particular tile size, so
every configuration runs one unchanged compiled binary. Any single design change
can therefore be measured end-to-end in isolation, with nothing else moving. The
cost model is calibrated on silicon anchors and validated against held-out models,
identifying the binding resource correctly on all six.

*In submission.*
