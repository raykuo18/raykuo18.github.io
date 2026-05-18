---
layout: page
title: Toward Tokenizer-Free Chinese LMs
description: Controlled comparison of Chinese character-embedding families under a fixed backbone; first milestone of a longer research program reframing tokenization as learned token construction.
img: assets/img/tokenizer_thumb.png
importance: 2
category: research
---

**Toward Tokenizer-Free Chinese Language Models.** Originated as a CSE 538 NLP final project (Spring 2026) at Stony Brook University; continuing as a PhD research direction.

A controlled comparison of three Chinese character-embedding families — char-ID lookup, IDS radical decomposition, and rendered-glyph vision encoders — under a fixed ModernBERT-small backbone. Isolates the input-representation axis from prior confounded comparisons in the Chinese-NLP-with-glyph-features literature.

**Why this matters.** The subword tokenization tradition (BPE, WordPiece, unigram LM) was designed for space-delimited alphabetic languages. For Chinese, it degenerates to character-level splitting and discards the sub-character structure (radicals, components, glyph layout) that Chinese orthography encodes. This project asks whether learned alternatives to the tokenizer + embedding lookup are principled.

**Key findings.**
- Structure-aware variants (IDS radical and glyph) match the char-ID baseline on C-MTEB (31 frozen tasks).
- Inside the glyph branch, encoders that preserve per-position features work out of the box; convolutional encoders need auxiliary structural supervision (IDS-units / IDC / pixel-reconstruction heads).
- Introduced a low-cost frozen-encoder pixel-reconstruction probe for OOV-character behavior, addressing a gap in public Chinese OOV embedding benchmarks.

**Position in the research program.** First concrete milestone of a longer PhD research thread reframing tokenization as a *learned token-construction* problem. Sister work to the VLM-SSM project on the vision side of the same input-interface thread — both re-examine the inherited architectural defaults of modern AI systems at their input boundaries.
