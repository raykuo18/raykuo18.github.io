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
- *Untouched:* the PyTorch front-end, the IR layer, the MLISA program format, and the lab's existing NPU pipeline RTL (scheduler, tensor manager, MFUs, scoreboard).
- *New:* a dedicated firmware variant for AIE (`starc-rt/aie/execute.c`), an ~8-line wrapper-level bypass routing AIE-tagged opcodes around the scheduler, and a parallel DMA tap. Vitis/Vivado heterogeneous-kernel integration on top.

**Why it was still hard.** Severely broken toolchain — VCK5000 documentation shared with (but actually targeting) VCK190, non-functional hardware emulation, silent failures, 8-hour bitstream compile cycles. With no working simulator, I invented an RTL-level debug methodology using a software-selectable debug-register multiplexer (`slv_reg7` selecting among 20+ internal-state taps), iterating against full bitstream rebuilds.

**The path wasn't straight.** The first integration attempt (Nov 15–17) tried to route AIE control through the existing MVM scheduler by repurposing instruction-packet bit-fields. After two attempts the cost-to-finish was too high, so I rolled back three days of work on `main` and started fresh on a new branch (`aie_ctrl_reset`) with the bypass strategy. Working state reached within four commits and one day of focused work after the rollback.

**Result.** First working end-to-end execution on this board in the lab (matmul kernel through the existing PyTorch → MLISA pipeline) — and the established integration pattern for all future MLISA-AIE work in the group.
