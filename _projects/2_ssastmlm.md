---
layout: page
title: SSAST-MLM
description: Pre-training the SSAST audio foundation model with a unified masked-prediction (MLM-style) loss.
img:
importance: 2
category: work
---

[SSAST-MLM](https://github.com/ameen-cet/ssast_mlm) pre-trains the [SSAST](https://github.com/YuanGongND/ssast) (Self-Supervised Audio Spectrogram Transformer) audio foundation model with a single, unified masked-prediction objective in place of its original two self-supervised losses.

SSAST normally pre-trains by masking patches of the input spectrogram and jointly optimizing two separate objectives:

- **MPC** (Masked Patch Classification) — a discriminative, contrastive-style loss over masked patches.
- **MPG** (Masked Patch Generation) — a generative loss that regresses the raw values of masked patches.

SSAST-MLM replaces both with a single classification loss, borrowing the masked-language-modeling recipe from BERT: each masked patch is assigned a discrete target label — a cluster ID obtained via k-means over patch features, in the style of HuBERT/BEiT — and the model learns to predict the correct label for every masked patch from its surrounding context. This turns SSAST pre-training into a masked "language" modeling task over quantized audio tokens, with one loss instead of two.

The resulting pre-trained encoder is intended as a general-purpose audio foundation model, to be fine-tuned on a range of downstream audio and speech tasks.

Code: [github.com/ameen-cet/ssast_mlm](https://github.com/ameen-cet/ssast_mlm)
