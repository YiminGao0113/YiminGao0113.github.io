---
title: "FlexPosit"
collection: projects
order: 1
permalink: /projects/flexposit
tagline: "Tunable fractional precision for LLM inference accelerators"
status: "MICRO 2026"
keywords: ["posit arithmetic", "LLM inference", "bit-serial", "accelerator design"]
excerpt: "A precision-scalable posit accelerator that lets you dial in exactly as many fraction bits as a layer actually needs."
---

Running a large language model is mostly an exercise in moving numbers around. The
multiplies are cheap; the bandwidth and energy spent hauling weights out of memory
are not. That makes the choice of number format one of the highest-leverage
decisions in the whole accelerator.

The trouble is that the usual options are coarse. FP16 is safe but wasteful. INT8
is fast but needs careful calibration, and it spends its precision uniformly
across a range that neural network weights don't actually use uniformly. Every
layer gets the same format whether it wants it or not.

Posits are a better starting point, because their accuracy is *tapered* — they
carry the most precision near ±1, which is where most weights and activations
actually live. FlexPosit builds on that idea and makes the fraction width itself
tunable, so precision becomes a knob rather than a fixed property of the datapath.
The hardware is bit-serial, which means the cost of a given operation scales with
the precision you asked for instead of the worst case you provisioned for.

The result is an accelerator that can trade accuracy for throughput and energy
continuously, and do it per layer, rather than forcing one global format on the
entire model.

*To appear at the IEEE/ACM International Symposium on Microarchitecture
(MICRO) 2026. Work with L. Dai, J. Yin, X. Guo, and M. R. Stan.*
