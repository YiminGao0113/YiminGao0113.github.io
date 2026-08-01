---
permalink: /
title: "Yimin Gao"
author_profile: true
redirect_from:
  - /about/
  - /about.html
---

I'm a PhD student in [Electrical and Computer Engineering](https://engineering.virginia.edu/departments/electrical-and-computer-engineering) at the [University of Virginia](https://www.virginia.edu/), where I work with [Prof. Mircea R. Stan](https://engineering.virginia.edu/faculty/mircea-r-stan).

Most of my work comes back to the same stubborn question: **how much precision does a computation actually need, and where should it happen?** We tend to answer both by habit — 16 bits because that's the default, in the processor because that's where computation goes. Neither is usually right. A neural network layer might be fine at 4 bits while its neighbor falls apart below 8. A database filter that discards 99% of what it reads has no business dragging all that data across a memory bus first.

Chasing that question has taken me through low-precision number formats, quantization, AI accelerator architecture, processing-in-memory, and — by a route I did not anticipate — hardware security. The through-line is co-design: the algorithm and the silicon are one system, and the interesting wins live in the space between them, where neither field alone tends to look.

Lately I've been focused on making large language model inference cheaper, which is where [FlexPosit](/projects/flexposit) came from.

What I work on
======
- **AI accelerator architecture** — building datapaths that match how models actually compute
- **Hardware-aware quantization** — choosing precision with the hardware cost in view, not after the fact
- **Hardware–software co-design** — treating the boundary as a design variable rather than a given
- **Hardware security** — lightweight primitives for devices with nothing to spare

[See what I'm working on &rarr;](/projects/)

Selected publications
======
1. **Y. Gao**, et al. "FlexPosit: Tunable Fractional Precision for LLM Inference Accelerators." *IEEE/ACM International Symposium on Microarchitecture (MICRO)*, 2026. (to appear)
1. X. Zhao, R. Xu, **Y. Gao**, V. Verma, M. R. Stan, and X. Guo. "[Edge-MPQ: Layer-wise Mixed-Precision Quantization with Tightly Integrated Versatile Inference Units for Edge Computing](https://ieeexplore.ieee.org/document/10633877)." *IEEE Transactions on Computers*, 2024.
1. **Y. Gao**, J. Chilaka, E. Pantoja, R. Klenke, and M. R. Stan. "[CryptoPUF: A Lightweight and ML-Resilient Strong PUF Based on a Weak PUF and Crypto Core](https://ieeexplore.ieee.org/document/10965172)." *IEEE International Conference on RFID Technology and Applications (RFID-TA)*, 2024.
1. **Y. Gao**, S. Mosanu, M. N. Sakib, V. Verma, X. Guo, and M. R. Stan. "[LiteAIR5: A System-Level Framework for the Design and Modeling of AI-Extended RISC-V Cores](https://ieeexplore.ieee.org/document/10257058)." *IEEE International System-on-Chip Conference (SOCC)*, 2023.

[Full publication list &rarr;](/publications/)

Patent
======
- K. Skadron, L. Wu, A. Shekar, and **Y. Gao**. "[Membrane: Accelerating Database Analytics with DRAM-PIM Filtering](https://patents.google.com/patent/US20250377803A1/en)." U.S. Patent Application 19/233,680, 2025.

Get in touch
======
Always happy to talk about number formats, accelerators, or why your quantized model lost three points of accuracy. Reach me at [yg9bq@virginia.edu](mailto:yg9bq@virginia.edu).
