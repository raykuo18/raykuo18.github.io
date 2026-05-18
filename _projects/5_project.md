---
layout: page
title: Adaptive Chess Tutor
description: Locally-deployable dual-LoRA TinyLlama chess tutor; original CSE 537 course project (Spring 2025) plus a 47-evaluation reproduction (May 2026) characterizing what holds up and what doesn't.
img: assets/img/chess_thumb.png
importance: 5
category: research
---

**Adaptive Chess Tutoring: Efficient LLM Reasoning via Programmatic Supervision and Cognitive Distillation.** Course project, CSE 537 Artificial Intelligence, Stony Brook University (Spring 2025); full end-to-end reproduction on the NuWulf HPC cluster, May 2026. Team of two on the original; I led the proposal, dataset synthesis, training pipeline, evaluation, writing, and poster. Instructor: Niranjan Balasubramanian.

A unified, locally-deployable AI chess tutor that combines move prediction *and* human-like explanation in a single compact LLM — avoiding the misalignment of hybrid cloud stacks where the explainer has no access to the move-decider's internal state.

**Technical design.**
- *Dual-branch LoRA architecture.* Two LoRA adapters on TinyLlama-1.1B — one for chess foundations (Policy), one for explanation — trained independently to prevent catastrophic forgetting between the two skills.
- *Phase 1 — programmatic supervision.* Fine-tuned on ~60K rule-grounded samples generated from Lichess PGN games via `python-chess` as a programmatic verifier (every label provably correct against chess rules).
- *Phase 2 — cognitive distillation.* Distilled explanation behavior from a Mixtral-8x7B teacher (~10K samples) into the Explanation LoRA, layered on top of the frozen Phase 1 adapter.
- *Runtime adapter blending.* Tunable α/β coefficients weight the two adapters at inference via PEFT's `add_weighted_adapter`. α and β are static for a run — this is **not** per-token adaptive inference.

**Stack.** PEFT, QLoRA 4-bit (bitsandbytes), Paged AdamW, Hugging Face Transformers, python-chess, Stockfish, BERTScore. SLURM on H200 / B40 GPUs.

**What the 47-evaluation reproduction confirmed (NuWulf, May 2026).** Across two training recipes, six adapter-merge strategies, 17 α/β operating points, and two BERTScore backbones:

- **Phase 1 reproduces strongly.** The programmatic-supervision adapter lifts `can_piece_move` accuracy from **2.9 % (base TinyLlama) → 94.2 %** (Phase 1). `is_square_attacked` 31.8 % → 49.7 %. `list_legal_moves` F1 0.000 → 0.230. The model demonstrably learned rule-grounded chess facts the base did not know.
- **The runtime α/β trade-off reproduces.** A clean 17-point monotone curve: BERTScore F1 drops 0.480 → 0.357 as α grows 0.25 → 2.0; Stockfish Score Delta spreads ~3× in the opposite direction. The architecture genuinely lets a user dial between *better moves* and *more reference-similar explanations* at inference.

**Honest contribution statement (post-reproduction).** A dual-LoRA architecture for combining a programmatic-SFT chess foundation adapter with a Mixtral-distilled chess-explanation adapter, with a reproducible runtime α/β trade-off between move quality and explanation similarity. Phase 1 improves chess rule-probe accuracy by **~91 points** over base TinyLlama, supported by 47 evaluations across the relevant axes of variation.

**Honest disclosure — what did not reproduce.** The original writeup's headline claim was that Phase 2 distillation lifts BERTScore F1 from 0.4744 → **0.5891**. Across all 47 evaluations, peak F1 is **0.4801** (vs base 0.4773) — 1.5 points above base, not 11.5. Backbone choice, merge strategy, and training length were each ruled out as the explanation. The most likely cause is undocumented differences in the original test set, aggregation, or hyperparameter setup that the committed scripts don't capture. The honest statement of the project's contribution centers on the trade-off curve rather than the BERTScore-improvement number.

**Methodology + engineering findings worth circulating.**
- *BERTScore backbone choice shifts absolute F1 by ~0.34.* `deberta-xlarge-mnli` scores the same outputs at F1≈0.48 that `roberta-large` scores at F1≈0.81. Any future chess-commentary publication using BERTScore should specify the backbone.
- *PEFT TIES / DARE merges collapse to weight-independent outputs* at TinyLlama's small LoRA r=16 scale (F1 sticks at exactly 0.4199 regardless of α/β). Sparsification wipes the LoRA delta on explanation-relevant attention modules.
- *PEFT version sensitivity.* `PeftModel.add_weighted_adapter` exists at the instance level through PEFT ~0.13; later versions removed the `__getattr__` delegation. Code written for the older API breaks silently in newer PEFT.
