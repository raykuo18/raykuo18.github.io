---
layout: about
title: about
permalink: /
subtitle: >
  PhD Student, Computer Science · Stony Brook University ·
  <a href="https://paolacascante.com/lab/">SPELL Lab</a>

profile:
  align: right
  image: my_photo.jpg
  image_circular: false
  more_info: >
    <p>Advised by <a href="https://paolacascante.com/">Prof. Paola Cascante-Bonilla</a></p>
    <p>Stony Brook, NY</p>

selected_papers: true
social: true

announcements:
  enabled: false

latest_posts:
  enabled: false
---

I am a PhD student in Computer Science at Stony Brook University,
advised by [Prof. Paola Cascante-Bonilla](https://paolacascante.com/)
in the [SPELL Lab](https://paolacascante.com/lab/). Before starting
my PhD, I was an AI researcher and AI accelerator engineer at
[Inventec Corporation](https://www.inventec.com/en/) in Taipei,
working on medical image segmentation and NPU IP design. I received
my B.S. in Electrical Engineering from
[National Taiwan University](https://www.ntu.edu.tw/english/) in 2023.

I am broadly interested in fundamental research that questions
established design choices in AI. Not "how do we improve X" but
"should X exist in this form at all."

My work is currently organized around vision-language models as a
unifying thread. I first examined the vision side: are Vision
Transformers actually the right backbone for VLMs, or is this a
historical default worth revisiting? My paper on this found that SSM
backbones, under the same pretraining budget, provide substantially
stronger spatial grounding while remaining competitive on open-ended
VQA — and can match or outperform much larger ViT-based encoders on
localization benchmarks. I am now turning to the language side, asking
whether the standard tokenization pipeline is the right input
interface, particularly for writing systems it was never designed for.
Both questions share the same structure: a design choice made under
historical constraints that is worth revisiting from first principles.
And together, they point to something deeper — vision and language are
currently processed through very different pipelines and combined in
ways that feel more pragmatic than principled. I am drawn to research
that asks whether there is a more natural, unified interface for
multiple modalities, and I see vision-language as the starting point
of a longer journey toward understanding how AI systems should process
the world across any modality.

My background in hardware and systems gives me a particular lens for
identifying these opportunities. Many foundational design choices in
deep learning sit at the boundary of what was theoretically motivated
and what was computationally practical at the time, and as systems
evolve, some of those constraints quietly become legacy assumptions.
I am drawn to research at exactly this boundary: close enough to
systems to recognize where constraints came from, but standing firmly
on the AI side to propose alternatives the broader community can
build on.
