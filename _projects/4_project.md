---
layout: page
title: MLISA AIE Backend (VCK5000)
description: Runtime-only retargeting of a PyTorch → IR → MLISA pipeline from a custom RTL NPU to AMD AI Engine cores on a VCK5000 FPGA.
img: assets/img/vck5000_thumb.png
importance: 4
category: research
---

**MLISA AIE Backend on AMD VCK5000 FPGA — Runtime-only Retargeting from a Custom RTL NPU to AI Engine Cores.** Sole engineer; carried out at COMPAS Lab, Stony Brook University (Fall 2025).

The MLISA project inserts a standardized ISA layer after the IR in the ML compilation stack — the intended consequence being that a hardware vendor can add a new backend by writing **runtime code** against a fixed contract, not a full backend compiler. My sub-project was the load-bearing demonstration of that claim: retargeting the lab's existing PyTorch → IR → MLISA → NPU pipeline to AMD's AI Engine on the VCK5000 FPGA — a hardware target nobody considered when MLISA was defined — via runtime-only modifications.

**What was untouched, and what was new.**
- *Untouched:* the PyTorch front-end, the IR layer, and the MLISA program format. Same compiled MLISA programs that already ran on the lab's custom RTL NPU.
- *New:* a runtime layer redirecting tensor-computation operations to AIE cores via Vitis/Vivado heterogeneous-kernel integration, plus a new RISC-V control program (RTL of the existing RISC-V control core was reused as a kernel).

**Why it was still hard.** Severely broken toolchain — VCK5000 documentation shared with (but actually targeting) VCK190, non-functional hardware emulation, silent failures, 8-hour bitstream compile cycles. With no working simulator, I invented an RTL-level debug methodology using configurable on-chip debug registers to expose internal state, iterating against full bitstream rebuilds.

**Result.** First working end-to-end execution on this board in the lab (matmul kernel through the existing PyTorch → MLISA pipeline) — and the established integration pattern for all future MLISA-AIE work in the group.
