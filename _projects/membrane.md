---
title: "Membrane"
collection: projects
order: 6
permalink: /projects/membrane
tagline: "Bit-serial comparison inside DRAM, so most rows never leave memory"
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

The broader project pairs this in-memory filtering with schema denormalization,
since normalized schemas scatter the columns a filter needs across tables — good
database design, bad PIM workload.

*Published in ACM Transactions on Architecture and Code Optimization (TACO), 2025,
with A. Shekar, K. Gaffney, M. Prammer, K. Kiyawat, L. Wu, H. Caminal, Z. Fan, and
colleagues. Related U.S. patent application 19/233,680, with K. Skadron, L. Wu,
and A. Shekar.*
