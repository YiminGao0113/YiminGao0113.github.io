---
permalink: /
title: "Yimin Gao"
author_profile: true
redirect_from:
  - /about/
  - /about.html
---

I'm a PhD student in [Electrical and Computer Engineering](https://engineering.virginia.edu/departments/electrical-and-computer-engineering) at the [University of Virginia](https://www.virginia.edu/), working with [Prof. Mircea R. Stan](https://engineering.virginia.edu/faculty/mircea-r-stan) on efficient and secure hardware for edge AI.

I work across the whole stack rather than one slice of it — RTL design, NPU and SoC integration, compilers and runtimes on FPGA, and silicon-aware modeling. That's deliberate. A design can look great in a spreadsheet and then lose badly on real hardware to something the model never accounted for, and you usually only find that out by building it and measuring.

What I work on
======
- **AI accelerator architecture**
- **Hardware–software co-design**, including hardware-aware quantization
- **Hardware security**

Current projects
======
- **[FlexPosit](/projects/flexposit)** — an LLM inference accelerator that makes precision a continuously tunable knob instead of a property baked into the datapath. *MICRO 2026, taping out in GF12.*
- **[EdgeScope](/projects/edgescope)** — design space exploration that puts the host CPU inside the design space, so you stop buying silicon for a bottleneck you don't have. *Built on FlexNPU, a full-stack FPGA NPU platform — compiler, runtime, RTL.*
- **[Edge-MPQ](/projects/edge-mpq)** — mixed-precision inference units built into a RISC-V pipeline, and a search that knows what the hardware can actually do.
- **[LiteAIR5](/projects/liteair5)** — an AI-extended RISC-V core and the end-to-end framework for designing one.
- **[CryptoPUF](/projects/cryptopuf)** — a weak PUF and a crypto core covering each other's weaknesses, for devices with no area to spare. *Taping out in GF12.*
- **[Membrane](/projects/membrane)** — bit-serial comparison inside DRAM, so most rows never cross the memory bus.

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
I'm always up for talking about accelerators, quantization, or hardware security. Reach me at [yg9bq@virginia.edu](mailto:yg9bq@virginia.edu).
