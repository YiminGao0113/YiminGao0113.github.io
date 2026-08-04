---
title: "Edge-MPQ"
collection: projects
order: 3
permalink: /projects/edge-mpq
tagline: "Layer-wise mixed-precision quantization, co-designed with the hardware that runs it"
status: "IEEE Transactions on Computers 2024"
keywords: ["quantization", "mixed precision", "edge inference", "design space exploration"]
excerpt: "Not every layer deserves the same number of bits — and the inference unit should be built to exploit that."
---

Quantization research and quantization hardware tend to be written by different
people, and it shows. Algorithm papers propose elegant per-layer bitwidth
assignments; the accelerators they run on support two or three widths, so most of
that elegance evaporates on contact with silicon.

Edge-MPQ treats the two halves as one problem. On the algorithm side, it assigns
bitwidths layer by layer, based on how much precision each layer's sensitivity
actually justifies. On the hardware side, it pairs that with versatile inference
units that are tightly integrated into the edge pipeline and genuinely support the
mixed widths the search produces — so a layer assigned 4 bits costs less than a
layer assigned 8, rather than both being padded to the same datapath.

The earlier GLSVLSI work mapped out the design space this sits in: which
combinations of bitwidth assignment and inference-unit organization are actually
reachable, and where the cliffs are. The journal version carries that through to a
full layer-wise scheme with the inference units built to match.

*Published in IEEE Transactions on Computers, 2024, with earlier design space
exploration at GLSVLSI 2023. Work with X. Zhao, R. Xu, V. Verma, M. R. Stan, and
X. Guo.*
