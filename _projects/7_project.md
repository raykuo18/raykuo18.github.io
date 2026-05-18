---
layout: page
title: Stylus Trajectory CNN
description: Lightweight CNN (10–50K params) for stylus-trajectory regression from capacitive sensors, deployed in the panel IC of a top IC design house. Sub-2-pixel accuracy, ~50% error reduction over the prior rule-based algorithm.
img: assets/img/stylus_thumb.png
importance: 7
category: industry
---

**Lightweight CNN for stylus trajectory regression on panel-IC hardware.** Inventec Corporation, Digital Center (AI-on-Chip team), 2023 — sole ML engineer on this sub-project.

A convolution-based regression model that turns noisy capacitive-sensor readings into a stylus trajectory, replacing the existing rule-based on-chip algorithm. Deployed in the panel IC of a top IC design house. **Sub-2-pixel accuracy** at **10–50K parameters** (depending on hardware variant), **~50% error reduction** over the prior rule-based baseline that had been hand-tuned for years by domain experts.

**What this project actually shows.**
- *Lightweight ML targeting embedded hardware.* The 10–50K-parameter budget was set by the panel IC's compute and memory envelope; the model was designed working backward from that constraint, not by shrinking a research model after the fact.
- *Beating a tuned rule-based baseline in production.* ~50% error reduction over a domain-expert-tuned baseline is a meaningful applied-ML win — these baselines are usually hard to beat because they encode years of domain knowledge.
- *End-to-end ownership of a shipped product feature.* Dataset construction from real sensor traces → model design under hardware constraints → training → evaluation against the production baseline → handoff for customer-IC integration.

**Stack.** PyTorch for model design and training; a regression pipeline targeted at the pixel-accuracy metric the customer cared about; evaluation harness for apples-to-apples comparison against the on-chip rule-based algorithm.

**Context.** This project ran out of Inventec's Digital Center (AI-on-Chip team), in parallel with the [ICASSP 2024 paper](/projects/3_project/) on cross-domain augmentation for foot-ulcer segmentation that ran out of Inventec's AI Center. Customer name and customer-product details are confidential.
