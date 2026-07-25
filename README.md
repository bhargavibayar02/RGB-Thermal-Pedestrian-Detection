# RGB-Thermal Pedestrian Detection — CBAM-Enhanced Gated Fusion in QFDet

![Python](https://img.shields.io/badge/Python-3.8-blue)
![PyTorch](https://img.shields.io/badge/PyTorch-1.10-red)
![MMDetection](https://img.shields.io/badge/MMDetection-2.28.2-green)
![MMCV](https://img.shields.io/badge/MMCV-1.6.1-orange)

**Yugma TechFest 2.0 – MedhaDrishti National-Level AI Hackathon**
Track: *AI for Multimodal RGB-Thermal Pedestrian Detection through Efficient Fusion Strategies*

---

## Overview

RGB cameras capture rich texture but fail in low light; thermal cameras are illumination-invariant but lack fine detail. Baseline **QFDet** fuses both via simple concatenation. This project replaces that with a **CBAM-enhanced gated cross-modal fusion**: channel + spatial attention (CBAM) refines each modality's features, then a lightweight gating network learns how much to trust RGB vs. thermal per scene (e.g. more RGB in daylight, more thermal at night) before fusion — a fine-tune-only improvement on the provided pretrained weights, no training from scratch.

## Dataset

VTUAV-det curated subset — single class (`pedestrian`), RGB + thermal pairs, COCO annotations.

| Split | Pairs |
|---|---|
| Train | 1200 |
| Val | 300 |
| Test | 200 |

## Architecture

**Baseline:** RGB/Thermal → ResNet50 + FPN (each) → QFDet quality-aware fusion → detection head.

**Proposed:** same backbones, with two additions before fusion:
1. **CBAM** on each modality's features (channel attention → spatial attention).
2. **Gated fusion** — global pooling + a small MLP produces per-channel RGB/thermal gates that scale each modality before concatenation, replacing plain concat.

## Results (test set)

| Model | mAP | mAP50 | mAP75 | mAP_S | mAP_M | mAP_L |
|---|---|---|---|---|---|---|
| RGB-only | 0.041 | – | – | – | – | – |
| Thermal-only | 0.232 | – | – | – | – | – |
| QFDet (baseline) | 0.299 | 0.674 | 0.227 | 0.129 | 0.299 | 0.554 |
| Proposed – Run 1 | 0.284 | – | – | – | – | – |
| **Proposed – Run 2 (best)** | **0.326** | **0.712** | **0.251** | **0.130** | **0.311** | **0.572** |

Best model beats the baseline on every metric — the fix was a 10× learning-rate multiplier on the new gating layers so they train fast enough within the fine-tuning budget.




## Future Work

- Transformer / cross-attention fusion
- Knowledge distillation for a lighter model
- Real-time UAV edge deployment

## Acknowledgements

Built on **QFDet** (OpenMMLab / MMDetection / PyTorch) and the **VTUAV-det** dataset.

## Team

**Team SriVerse** — Yugma TechFest 2.0 Hackathon Submission

## References

1. Zhang et al., *Drone-based RGB-Thermal Tiny Person Detection*, ISPRS Journal of Photogrammetry and Remote Sensing, 2023.
2. MMDetection Documentation — OpenMMLab
3. VTUAV-det Dataset
4. QFDet GitHub Repository

---
*Academic/hackathon use only — see original QFDet and VTUAV-det licenses before any commercial use.*
