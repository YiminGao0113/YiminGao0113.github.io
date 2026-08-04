---
title: "Membrane"
collection: projects
order: 6
permalink: /projects/membrane
tagline: "Filtering database queries inside DRAM, before the data ever moves"
status: "ACM TACO 2025 · US patent pending"
keywords: ["processing-in-memory", "DRAM", "database analytics", "schema denormalization"]
excerpt: "Analytical queries read enormous amounts of data and throw most of it away. Better to throw it away early."
---

Analytical database queries have a wasteful shape. A scan pulls gigabytes off
memory, a filter discards the overwhelming majority of it, and the rows that
survive are a small fraction of what was moved. All that bandwidth is spent
transporting data whose only destiny is to be rejected.

Membrane pushes the filter down into DRAM itself. Processing-in-memory puts simple
comparison logic where the data already is, so rows can be rejected in place and
never cross the memory bus at all. What reaches the processor is closer to the
answer than to the raw table.

The second half of the idea is schema denormalization. Normalized schemas are good
database design and bad PIM workloads — joins scatter the data a filter needs
across tables that live in different places. Denormalizing puts the relevant
columns where the in-memory filter can actually reach them, which is what makes the
filtering pay off.

This is joint work with a larger team, and it's the project that most changed how I
think about where computation should live relative to data.

*Published in ACM Transactions on Architecture and Code Optimization (TACO), 2025,
with A. Shekar, K. Gaffney, M. Prammer, K. Kiyawat, L. Wu, H. Caminal, Z. Fan, and
colleagues. Related U.S. patent application 19/233,680, with K. Skadron, L. Wu,
and A. Shekar.*
