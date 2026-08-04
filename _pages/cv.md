---
layout: archive
title: "CV"
permalink: /cv/
author_profile: true
redirect_from:
  - /resume
---

{% include base_path %}

[Download CV (PDF)](/files/Yimin_Gao_CV.pdf) &nbsp;·&nbsp; [yg9bq@virginia.edu](mailto:yg9bq@virginia.edu) &nbsp;·&nbsp; +1 (434) 257-3458 &nbsp;·&nbsp; Charlottesville, VA

PhD student specializing in AI/ML accelerators and computer architecture, with
full-stack experience across RTL design, NPU/SoC system integration, and
compilers/runtimes on FPGA. Skilled in hardware–software co-design,
mixed-precision quantization, cycle-accurate simulation, and end-to-end ML
inference on custom hardware.

Education
======
* **Ph.D., Electrical Engineering** — University of Virginia, 2023 – May 2027 (expected)
  * Advisor: Prof. Mircea R. Stan
* **M.S., Electrical Engineering** — University of Virginia, 2021 – 2022
* **B.E., Electrical Engineering** — University of Cincinnati & Chongqing University, dual degree program, 2015 – 2020

Experience
======
* **Research Assistant** — High-Performance Low-Power (HPLP) Lab, University of Virginia, 2022 – present
  * Research in AI hardware, quantization, and hardware security
* **Teaching Assistant** — Department of Electrical and Computer Engineering, University of Virginia
  * Computer Architecture and Design, Advanced Embedded Systems, AI Hardware

Selected projects
======

**[FlexNPU — full-stack FPGA AI accelerator platform](/projects/edgescope)** (compiler, runtime, RTL)
* Built an end-to-end AI accelerator on a Xilinx Kria KV260 (Zynq SoC): custom compiler backend, custom C/C++ runtime, and a double-buffered RTL shell with AXI DMA
* Wrote custom MLIR/IREE passes lowering ML operators (GEMM, softmax, depthwise) onto accelerators, plus an ARM-host runtime and register/DMA interface that swaps RTL tiles without recompiling
* Up to 31× end-to-end MobileBERT INT8 speedup over the on-chip ARM CPU

**[Precision-scalable bit-serial LLM accelerator with mixed-precision quantization](/projects/flexposit)** (FlexPosit)
* Designed and verified a bit-serial systolic array in Verilog supporting per-kernel precision switching in a single datapath
* Built a mixed-precision post-training quantization pipeline in Python (PyTorch) for LLM weights, matched to the hardware's supported precisions
* Built a custom cycle-accurate simulator with memory and energy modeling (CACTI, Ramulator) to profile end-to-end LLM inference and guide design decisions
* Near-FP16 accuracy at sub-5-bit precision with up to 1.8× throughput and 2.0× energy reduction across LLaMA, OPT, Phi, and Yi
* Currently being taped out in GlobalFoundries 12nm

**[Mixed-precision AI acceleration on a custom RISC-V SoC](/projects/edge-mpq)** (Edge-MPQ, LiteAIR5)
* Re-architected a 16-bit integer multiplier into a SIMD mixed-precision dot-product unit supporting INT2–INT8 and INT16 through hardware reuse and shift–add composition, integrated into a RISC-V core via ISA and microarchitecture co-design
* 15.5–47.7× speedup and up to 20.5 TOPS/W on quantized CNN kernels over a baseline RISC-V core
* Integrated the AI-extended core into a full FPGA-based SoC and evaluated quantized GEMM under memory-constrained conditions, reaching up to 37× speedup by cutting instruction count and memory traffic

**[ML-resilient PUFs for resource-constrained devices](/projects/cryptopuf)** (CryptoPUF)
* Combined a weak PUF with a cryptographic encryption core for intrinsic key generation without on-chip key storage, resisting LR, SVM, and MLP modeling attacks
* Designed and simulated delay-based CMOS PUF circuits at the transistor level in Cadence Virtuoso/ADE with Monte Carlo variability analysis
* Currently being taped out in GlobalFoundries 12nm

Skills
======
* **Hardware / RTL:** Verilog, SystemVerilog, Vivado, ModelSim, Synopsys DC/ICC2
* **Programming:** C/C++, Python, RISC-V assembly, CUDA, Tcl, Bash
* **ML / compilers:** PyTorch, MLIR/LLVM, IREE, model quantization, cycle-accurate simulation
* **Tools:** Git, Make, Cadence Virtuoso (ADE, Spectre)

Publications
======
  <ul>{% for post in site.publications reversed %}
    {% include archive-single-cv.html %}
  {% endfor %}</ul>
