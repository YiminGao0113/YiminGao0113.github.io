---
permalink: /
title: "Yimin Gao"
author_profile: true
redirect_from:
  - /about/
  - /about.html
---

I'm a PhD student in [Electrical and Computer Engineering](https://engineering.virginia.edu/departments/electrical-and-computer-engineering) at the [University of Virginia](https://www.virginia.edu/), working with [Prof. Mircea R. Stan](https://engineering.virginia.edu/faculty/mircea-r-stan) on efficient and secure hardware for edge AI.

I like building the whole stack rather than one slice of it — architectural exploration, RTL, FPGA system integration, and silicon-aware modeling. That end-to-end habit is deliberate. A design can look great in a spreadsheet and then lose badly on real hardware to something the model never accounted for, and you usually only find that out by building it and measuring.

What I'm working on now
======

**[FlexPosit](/projects/flexposit)** — an LLM inference accelerator that treats precision as a continuously tunable resource rather than a fixed property of the datapath. Posit-based algorithm–hardware co-design: distribution-aware mixed-precision quantization on one side, and a unified bit-serial systolic array that tunes precision from 4 to 8 bits without giving up regular dataflow on the other. Near-FP16 accuracy below 5 bits average, and up to 1.8× throughput and 2× lower energy at matched accuracy. Appearing at MICRO 2026.

**[EdgeScope](/projects/edgescope)** — full-stack profiling and design space exploration for edge NPUs. Most DSE tools model the accelerator alone and leave the host CPU out of the design space. On real workloads the host is often the thing actually holding you back, so EdgeScope models compute, memory, dispatch, and host together, and it's calibrated against an FPGA platform rather than against assumptions.

Before those, I worked on mixed-precision quantization and the inference units to run it ([Edge-MPQ](/projects/edge-mpq)), a framework for exploring AI-extended RISC-V cores ([LiteAIR5](/projects/liteair5)), ML-resilient PUFs ([CryptoPUF](/projects/cryptopuf)), and processing-in-memory for database analytics ([Membrane](/projects/membrane)).

What I work on
======
- **AI accelerator architecture**
- **Hardware–software co-design**, including hardware-aware quantization
- **Hardware security**

[More on all of it &rarr;](/projects/)

Selected publications
======
1. **Y. Gao**, L. Dai, J. Yin, X. Guo, and M. R. Stan. "FlexPosit: Tunable Fractional Precision for LLM Inference Accelerators." *IEEE/ACM International Symposium on Microarchitecture (MICRO)*, 2026. (to appear)
1. X. Zhao, R. Xu, **Y. Gao**, V. Verma, M. R. Stan, and X. Guo. "[Edge-MPQ: Layer-wise Mixed-Precision Quantization with Tightly Integrated Versatile Inference Units for Edge Computing](https://ieeexplore.ieee.org/document/10633877)." *IEEE Transactions on Computers*, 2024.
1. **Y. Gao**, J. Chilaka, E. Pantoja, R. Klenke, and M. R. Stan. "[CryptoPUF: A Lightweight and ML-Resilient Strong PUF Based on a Weak PUF and Crypto Core](https://ieeexplore.ieee.org/document/10965172)." *IEEE International Conference on RFID Technology and Applications (RFID-TA)*, 2024.
1. **Y. Gao**, S. Mosanu, M. N. Sakib, V. Verma, X. Guo, and M. R. Stan. "[LiteAIR5: A System-Level Framework for the Design and Modeling of AI-Extended RISC-V Cores](https://ieeexplore.ieee.org/document/10257058)." *IEEE International System-on-Chip Conference (SOCC)*, 2023.

[Full publication list &rarr;](/publications/)

Patent
======
- K. Skadron, L. Wu, A. Shekar, and **Y. Gao**. "[Membrane: Accelerating Database Analytics with DRAM-PIM Filtering](https://patents.google.com/patent/US20250377803A1/en)." U.S. Patent Application 19/233,680, 2025.

Get in touch
======
I'm always up for talking about accelerators, number formats, or why the profile doesn't match the model. Reach me at [yg9bq@virginia.edu](mailto:yg9bq@virginia.edu).
