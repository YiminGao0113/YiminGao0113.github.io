---
title: "EdgeScope"
collection: projects
order: 2
permalink: /projects/edgescope
tagline: "Design space exploration that puts the host CPU inside the design space"
status: "Platform in silicon · tool in submission"
keywords: ["NPU", "MLIR / IREE", "compiler and runtime", "design space exploration", "host bottleneck"]
excerpt: "Existing DSE tools model the accelerator in isolation. Spend your area budget on that advice and you can buy a bigger array for a workload that was never compute-bound."
---

Design space exploration tools — Timeloop, MAESTRO, roofline analysis — model the
accelerator in isolation: compute against memory, with the host CPU outside the
design space entirely.

On an edge NPU that's a bad assumption. The host isn't a spectator. It sequences
the accelerator through a compiled operator stream and does real per-operator work
along the way, and on many workloads that host work is what actually sets the
wall. It isn't that these tools weigh the host wrongly — they structurally cannot
represent it. The practical consequence is that they'll happily recommend spending
your whole area budget on a bigger array for a workload that was never
compute-bound.

EdgeScope treats the host as a first-class resource alongside compute, memory, and
dispatch, and allocates a fixed area budget across two coupled axes: **sizing**,
making the operators you already offload run faster, and **coverage**, moving whole
operator classes onto the accelerator to relieve the host.

Grow, then cover
======

Those axes don't decompose, which is the part worth knowing.

<figure class="project-figure">
<svg viewBox="0 0 680 280" role="img" aria-labelledby="pf-es-t pf-es-d">
  <title id="pf-es-t">The bottleneck moves when the array grows</title>
  <desc id="pf-es-d">Two bar charts. With a small array, compute is the tallest bar and the binding resource. After growing the array, compute shrinks below host, and the host becomes the tallest bar and the new bottleneck.</desc>

  <text class="pf-text-hd" x="60" y="40">Small array</text>
  <text class="pf-text-hd" x="420" y="40">After growing the array</text>

  <line class="pf-line" x1="50" y1="220" x2="285" y2="220"/>
  <line class="pf-line" x1="410" y1="220" x2="645" y2="220"/>

  <text class="pf-text-ac" x="80" y="62" text-anchor="middle">bottleneck</text>
  <rect class="pf-accent" x="60"  y="70"  width="40" height="150"/>
  <rect class="pf-fill"   x="116" y="172" width="40" height="48"/>
  <rect class="pf-fill"   x="172" y="206" width="40" height="14"/>
  <rect class="pf-fill"   x="228" y="134" width="40" height="86"/>

  <text class="pf-text-sm" x="80"  y="238" text-anchor="middle">compute</text>
  <text class="pf-text-sm" x="136" y="238" text-anchor="middle">memory</text>
  <text class="pf-text-sm" x="192" y="238" text-anchor="middle">dispatch</text>
  <text class="pf-text-sm" x="248" y="238" text-anchor="middle">host</text>

  <path class="pf-accent-line" d="M305 150 L385 150"/>
  <path class="pf-accent-line" d="M377 144 L385 150 L377 156"/>
  <text class="pf-text-ac" x="345" y="140" text-anchor="middle">grow</text>

  <text class="pf-text-ac" x="608" y="126" text-anchor="middle">bottleneck</text>
  <rect class="pf-fill"   x="420" y="166" width="40" height="54"/>
  <rect class="pf-fill"   x="476" y="172" width="40" height="48"/>
  <rect class="pf-fill"   x="532" y="206" width="40" height="14"/>
  <rect class="pf-accent" x="588" y="134" width="40" height="86"/>

  <text class="pf-text-sm" x="440" y="238" text-anchor="middle">compute</text>
  <text class="pf-text-sm" x="496" y="238" text-anchor="middle">memory</text>
  <text class="pf-text-sm" x="552" y="238" text-anchor="middle">dispatch</text>
  <text class="pf-text-sm" x="608" y="238" text-anchor="middle">host</text>

  <text class="pf-text-sm" x="340" y="270" text-anchor="middle">The host work was always there — compute was just hiding it.</text>
</svg>
<figcaption>Growing the array doesn't only shrink compute. It exposes the host, which is where the next spend has to go.</figcaption>
</figure>

Start small on a transformer workload and it's compute-bound, so growing the array
is the right move and a coverage unit would buy nothing. Grow it far enough and the
bottleneck flips to the host — the CPU-side work was there all along, just hidden
behind compute. Now the coverage unit, worthless a few steps earlier, becomes the
best remaining spend.

Explore either axis alone and you stop short. Array-alone runs into the host wall;
coverage-alone does nothing while compute is still binding. Only a loop that
watches the bottleneck *shift* finds "grow, then cover" — and the allocator finds
it on its own rather than being told. It also declines to spend when nothing helps,
from the same code path, with no special case.

Built on FlexNPU
======

Any of this is only trustworthy if the measurements are. EdgeScope is built on
FlexNPU, an end-to-end AI accelerator platform I developed on a Xilinx Kria KV260
(Zynq SoC) — custom compiler backend, custom C/C++ runtime, and a double-buffered
RTL shell with AXI DMA.

Custom MLIR/IREE passes lower ML operators (GEMM, softmax, depthwise convolution)
onto the accelerator slots, and an ARM-host runtime with a register and DMA
interface can swap RTL tiles **without recompiling the model**. The compiled binary
binds to the slot contract rather than to a particular tile size, so every
configuration runs one unchanged binary — which means any single design change can
be measured end-to-end in isolation, with nothing else moving.

The platform reaches up to **31× end-to-end speedup on MobileBERT INT8** over the
on-chip ARM CPU.

*Platform running in silicon. DSE tool in submission.*
