---
layout: archive
title: "CV"
permalink: /cv/
author_profile: true
redirect_from:
  - /resume
---

{% include base_path %}

PhD student researching efficient and secure hardware architectures for edge AI,
specializing in quantization-aware ML accelerators and hardware–software
co-design. Experienced in architectural exploration, RTL implementation,
FPGA-based system integration, and silicon-aware modeling.

Education
======
* **Ph.D., Electrical Engineering** — University of Virginia, 2023 – Dec 2026 (expected)
  * Advisor: Prof. Mircea R. Stan
* **M.S., Electrical Engineering** — University of Virginia, 2021 – 2022
* **B.E., Electrical Engineering** — University of Cincinnati & Chongqing University, dual degree program, 2015 – 2020

Experience
======
* **Research Assistant** — High-Performance Low-Power (HPLP) Lab, University of Virginia, 2022 – present
  * PhD-level research in AI hardware, quantization, and hardware security
* **Teaching Assistant** — Department of Electrical and Computer Engineering, University of Virginia
  * Computer Architecture and Design, Advanced Embedded Systems, AI Hardware

Selected projects
======

**[Precision-tunable bit-serial systolic array for LLM inference](/projects/flexposit)** (FlexPosit)
* Led the design and verification of a precision-tunable bit-serial systolic array in Verilog, enabling temporal precision scaling per GEMM kernel without introducing spatial hardware irregularity
* Developed distribution-aware, sensitivity-guided mixed-precision quantization for outlier-heavy LLM weight distributions, and co-designed the accelerator datapath to support these precision profiles natively
* Built a custom cycle-accurate simulator with integrated memory and energy modeling (CACTI, Ramulator) to validate architectural decisions and analyze end-to-end inference behavior
* Near-FP16 accuracy at sub-5-bit weight precision, with up to 1.8× throughput and 2.0× energy reduction across LLaMA, OPT, Phi, and Yi

**[Host-aware design space exploration for edge NPUs](/projects/edgescope)** (EdgeScope)
* Built an FPGA NPU platform on a Xilinx Kria KV260 with an IREE/MLIR compilation flow, where portable bytecode binds to a slot contract rather than a tile size, so every configuration runs one unchanged binary
* Developed a design space exploration tool that models the host CPU as a first-class resource alongside compute, memory, and dispatch, calibrated on silicon and validated against held-out models
* Automated allocation across two coupled axes — accelerator sizing and operator coverage — matching exhaustive search in wall-time

**[SIMD mixed-precision GEMM datapaths within a RISC-V core](/projects/edge-mpq)** (Edge-MPQ)
* Re-architected a standard 16-bit integer multiplier into a versatile SIMD mixed-precision dot-product unit supporting INT2–INT8 and INT16 through hardware reuse and shift–add composition
* Integrated the datapath into a RISC-V core via ISA and microarchitecture co-design for layer-wise mixed-precision quantized CNN workloads
* 15.5–47.7× speedup over a baseline RV64IMA core and up to 20.5 TOPS/W on convolution kernels

**[FPGA-based RISC-V SoC with AI ISA extensions](/projects/liteair5)** (LiteAIR5)
* Designed and implemented an AI-extended RISC-V core within a full FPGA-based SoC on an open-source platform, targeting low-power, memory-constrained embedded systems
* Up to 37× speedup over a baseline RISC-V processor on quantized GEMM workloads by reducing instruction count and memory traffic

**[Variability-aware CMOS circuit design for reliable PUFs](/projects/cryptopuf)**
* Designed and simulated delay-based CMOS PUF circuits at the transistor level in Cadence Virtuoso/ADE, including Monte Carlo variability analysis
* Developed a fully digital reliability screening method that substantially reduces ECC overhead for lifelong reliable PUF-based key generation

Skills
======
* **Hardware description:** Verilog, SystemVerilog
* **Programming:** C/C++, Python, RISC-V assembly, Tcl, CUDA, Bash
* **Tools:** Cadence Virtuoso (ADE, Spectre), Synopsys DC/ICC2, ModelSim, Vivado, Quartus, Git, Make

Publications
======
  <ul>{% for post in site.publications reversed %}
    {% include archive-single-cv.html %}
  {% endfor %}</ul>
