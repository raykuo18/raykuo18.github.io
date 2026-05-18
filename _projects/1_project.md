---
layout: page
title: VLM-SSM Vision Encoders
description: Do VLMs need Vision Transformers? Controlled comparison of state space models vs ViTs as VLM vision encoders.
img: assets/img/vlm_thumb.png
importance: 1
category: research
related_publications: true
---

**Do VLMs Need Vision Transformers? Evaluating State Space Models as Vision Encoders.** A strictly controlled LLaVA-style backbone-swap study showing that pure State Space Model vision encoders (VMamba) match or beat much larger ViT-family encoders on grounding/localization while remaining competitive on open-ended VQA — at substantially smaller parameter scale.

Under review, 2026. Featured on Hugging Face Daily Papers. Poster accepted to SUNY AI Symposium 2026.

**Key findings.**
- Under strictly matched ImageNet-1K initialization with a frozen vision tower, fixed Vicuna-7B + 2-MLP connector recipe, VMamba (pure SSM, ~30–89M params) leads ViT-family backbones up to ~662M params on RefCOCO / RefCOCO+ / RefCOCOg referring-expression benchmarks.
- ImageNet classification accuracy and naive backbone scaling do not reliably predict downstream VLM performance — a result that should reshape how the field selects vision towers.
- Diagnosed "localization collapse" in some detection-pretrained checkpoints as a vision–language interface failure (not architectural); proposed simple stabilizations (3-MLP connector + square input geometry) recovering collapsed localization to near-baseline.

**Links.** [arXiv](https://arxiv.org/abs/2603.19209) · [Project page](https://lab-spell.github.io/vlm-ssm-vision-encoders/) · [Code](https://github.com/raykuo18/vlm-ssm-vision-encoders) · [HF Daily Papers](https://huggingface.co/papers/2603.19209) · [Checkpoints](https://huggingface.co/raykuo188/vlm-ssm-vision-encoders-checkpoints)
