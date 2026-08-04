---
title: "EdgeScope"
collection: projects
order: 2
permalink: /projects/edgescope
tagline: "Host-aware design space exploration for edge NPUs"
status: "In submission · formerly FlexNPU"
keywords: ["NPU", "design space exploration", "FPGA", "full-stack profiling", "host bottleneck"]
excerpt: "Most DSE tools model the accelerator alone and treat the host CPU as somebody else's problem. On real edge workloads, the host is often what's actually slowing you down."
---

If you want to know how big to make your NPU, you reach for a design space
exploration tool. Almost all of them model the accelerator in isolation: compute
throughput against memory bandwidth, with the host processor sitting outside the
design space entirely.

That's a bad fit for edge NPU systems. The host CPU isn't a spectator — it
sequences the accelerator through a compiled operator stream and does real
per-operator work along the way. On actual workloads that host work frequently
dominates end-to-end latency. It's a bottleneck the existing tools structurally
cannot see, because the host isn't in their model.

EdgeScope puts it in. It models four resources — **compute, memory, dispatch, and
host** — and, given a fixed area budget, automatically recommends how to spend it.

The part I care most about is that it's grounded in real silicon rather than
assumptions. EdgeScope is built on the FlexNPU platform, an FPGA system where
every configuration runs one unchanged compiled binary. That means any single
design change can be measured end-to-end in isolation, and the model's predictions
are calibrated and validated against hardware across six models.

Two axes, and you need both
======

EdgeScope explores two coupled axes: **sizing** (making the operators you already
offload run faster) and **coverage** (moving whole operator classes onto the
accelerator to relieve the host).

The interesting finding is that these don't decompose. For MobileBERT, the optimum
is a larger array *combined with* an on-array rescale unit, reaching **2.86×** —
and neither axis alone gets there. Enlarging the array by itself just exposes a
host bottleneck, which the coverage unit is then what relieves. Optimize either
one on its own and you'll stop short of the real answer.

It also knows when to say no. EdgeScope recommends coverage on the workloads where
coverage helps and declines to spend silicon where it doesn't, and its automated
allocator matches exhaustive search — in wall-time — on all six workloads.

*In submission. Previously FlexNPU.*
