---
layout: page
title: SmallALM
description: A lightweight 135M-parameter Audio Language Model for audio and speech understanding.
img:
importance: 1
category: work
---

[SmallALM](https://github.com/hrishikeshhpillai/smallALM) is a lightweight Audio Language Model (ALM) with only 135M parameters, built around a simple and scalable design for audio and speech understanding.

The architecture combines four core components:

- **Audio Encoder** — JASPER, a self-supervised encoder producing strong representations for both audio and speech signals.
- **Downsampler** — average pooling with a factor of 8 to reduce the audio sequence length before it reaches the language model.
- **Projector** — a two-layer MLP (768 → 576) with LayerNorm and GELU activation, bridging the audio encoder and the text decoder.
- **Text Decoder** — [SmolLM2-135M](https://huggingface.co/HuggingFaceTB/SmolLM2-135M), a small language model that generates text conditioned on the projected audio representations.

By pairing a frozen, self-supervised audio encoder with a compact SLM through a lightweight projector, SmallALM aims to show that competitive audio understanding doesn't require billion-parameter models — making it practical to train and run on modest compute.

Code: [github.com/hrishikeshhpillai/smallALM](https://github.com/hrishikeshhpillai/smallALM)
