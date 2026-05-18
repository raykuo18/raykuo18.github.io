---
layout: page
title: AI-Powered Beamforming Antenna
description: 1st Place + Best Presentation at Inventec Hackathon 2023 — repurposing existing laptop WiFi antennas as sensors via AI, with zero hardware modifications.
img: assets/img/beamforming_thumb.png
importance: 6
category: industry
---

**AI-Powered Beamforming Antenna System.** 2023 Inventec Hackathon Competition (Taipei, Taiwan). **1st Place + Best Presentation**, out of 300+ participants and 74 teams. Project lead and main AI contributor; partnered with an electromagnetics PhD (now a professor in Taiwan) on antenna design.

**The winning move.** Inventec is a major Taiwanese laptop ODM/OEM positioning toward edge-AI on its shipping consumer lineup. The implicit ask of the hackathon was *find AI features that run on hardware Inventec already builds, not features that require new silicon.* The idea: every laptop already carries multiple WiFi antennas that nobody uses for sensing — AI can turn the multi-port signal into product-relevant state (human presence, behavior, beam direction) with **zero BOM change**.

**What we built.** Two integrated systems demonstrating the same core insight:
- *Smart Scanning (AI-driven beamforming).* Collected signals from 5 antenna ports across a range of target directions; trained a regression model to predict target location from the 5-port pattern; inference loop steers the beam to maximize signal efficiency.
- *Behavior Recognition (human sensing).* The human body perturbs antenna signal patterns in a state-dependent way. Trained a small MLP classifier on 5-port signals across labeled states (sitting, standing, walking away, someone nearby, no one present). Example application: auto-wake the screen when the user approaches the laptop.

**What this project actually signals.** Product instinct (identifying the right idea for a specific business context), cross-disciplinary integration (AI + RF / antenna), and end-to-end execution + communication (pitch slides + recorded demo clips strong enough to win Best Presentation alongside 1st Place, judged by a non-technical panel). Not a research contribution — and the "hackathon" was a multi-week internal innovation challenge, not a 24-hour sprint.
