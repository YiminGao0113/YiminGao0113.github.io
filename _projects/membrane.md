---
title: "Membrane"
collection: projects
order: 6
permalink: /projects/membrane
tagline: "Bit-serial comparison inside DRAM, so most rows never leave memory"
accent: "#06b6d4"
status: "ACM TACO 2025 · US patent pending"
keywords: ["processing-in-memory", "DRAM", "bit-serial", "database analytics"]
excerpt: "Analytical queries read enormous amounts of data and discard most of it. Better to discard it before it crosses the bus."
---

Analytical database queries have a wasteful shape. A scan pulls gigabytes out of
memory, a filter throws almost all of it away, and only a small fraction of what
moved was ever going to matter. Membrane pushes that filter into DRAM itself, so
rows are rejected in place and never cross the memory bus.

My contribution was the **bit-serial comparison circuit** in the data buffers.
Comparison runs MSB to LSB, one bit position at a time, across the full width of
the memory band. Two things fall out of doing it that way. It's very cheap in area,
since a bit-serial comparator is small and you need one per column rather than a
full-width datapath. And it often finishes early: most comparisons are decided in
the high-order bits, so once a row's fate is determined there's no reason to keep
walking down to the LSB.

<figure class="project-figure">
<svg viewBox="0 0 680 250" role="img" aria-labelledby="pf-mb-t pf-mb-d">
  <title id="pf-mb-t">MSB-first comparison decides most rows early</title>
  <desc id="pf-mb-d">Six rows are compared one bit position at a time from most significant to least significant. Most rows are resolved within the first few bit positions and stop, so the comparison rarely walks all the way down to the least significant bit.</desc>

  <text class="pf-text-hd" x="20" y="30">Bit position</text>
  <text class="pf-text-ac" x="92" y="52">MSB</text>
  <text class="pf-text-sm" x="600" y="52">LSB</text>
  <path class="pf-accent-line" d="M120 44 L560 44"/>
  <path class="pf-accent-line" d="M553 38 L560 44 L553 50"/>

  <g class="pf-text-sm">
    <text x="20" y="82">row 1</text><text x="20" y="110">row 2</text><text x="20" y="138">row 3</text>
    <text x="20" y="166">row 4</text><text x="20" y="194">row 5</text><text x="20" y="222">row 6</text>
  </g>

  <g>
    <rect class="pf-accent" x="90" y="68" width="52" height="18"/>
    <rect class="pf-line-soft" x="150" y="68" width="470" height="18" fill="none"/>
    <text class="pf-text-sm" x="385" y="82" text-anchor="middle">resolved — stop</text>

    <rect class="pf-accent" x="90" y="96" width="52" height="18"/>
    <rect class="pf-accent" x="150" y="96" width="52" height="18"/>
    <rect class="pf-line-soft" x="210" y="96" width="410" height="18" fill="none"/>
    <text class="pf-text-sm" x="415" y="110" text-anchor="middle">resolved — stop</text>

    <rect class="pf-accent" x="90" y="124" width="52" height="18"/>
    <rect class="pf-line-soft" x="150" y="124" width="470" height="18" fill="none"/>
    <text class="pf-text-sm" x="385" y="138" text-anchor="middle">resolved — stop</text>

    <rect class="pf-accent" x="90" y="152" width="52" height="18"/>
    <rect class="pf-accent" x="150" y="152" width="52" height="18"/>
    <rect class="pf-accent" x="210" y="152" width="52" height="18"/>
    <rect class="pf-line-soft" x="270" y="152" width="350" height="18" fill="none"/>
    <text class="pf-text-sm" x="445" y="166" text-anchor="middle">resolved — stop</text>

    <rect class="pf-accent" x="90" y="180" width="52" height="18"/>
    <rect class="pf-line-soft" x="150" y="180" width="470" height="18" fill="none"/>
    <text class="pf-text-sm" x="385" y="194" text-anchor="middle">resolved — stop</text>

    <rect class="pf-fill-strong" x="90"  y="208" width="52" height="18"/>
    <rect class="pf-fill-strong" x="150" y="208" width="52" height="18"/>
    <rect class="pf-fill-strong" x="210" y="208" width="52" height="18"/>
    <rect class="pf-fill-strong" x="270" y="208" width="52" height="18"/>
    <rect class="pf-fill-strong" x="330" y="208" width="52" height="18"/>
    <rect class="pf-fill-strong" x="390" y="208" width="52" height="18"/>
    <rect class="pf-fill-strong" x="450" y="208" width="52" height="18"/>
    <rect class="pf-fill-strong" x="510" y="208" width="52" height="18"/>
    <rect class="pf-fill-strong" x="570" y="208" width="50" height="18"/>
  </g>

  <text class="pf-text-sm" x="340" y="244" text-anchor="middle">Only the rare ambiguous row walks the full width.</text>
</svg>
<figcaption>A bit-serial comparator is small enough to place per column, and starting at the MSB means most rows are decided long before the last bit.</figcaption>
</figure>

The broader project pairs this in-memory filtering with schema denormalization,
since normalized schemas scatter the columns a filter needs across tables — good
database design, bad PIM workload.

*Published in ACM Transactions on Architecture and Code Optimization (TACO), 2025,
with A. Shekar, K. Gaffney, M. Prammer, K. Kiyawat, L. Wu, H. Caminal, Z. Fan, and
colleagues. Related U.S. patent application 19/233,680, with K. Skadron, L. Wu,
and A. Shekar.*
