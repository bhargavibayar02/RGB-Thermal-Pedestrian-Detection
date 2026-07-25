# RGB-Thermal Pedestrian Detection using CBAM-Enhanced Gated Fusion in QFDet

<div align="center">

![Python](https://img.shields.io/badge/Python-3.8-blue)
![PyTorch](https://img.shields.io/badge/PyTorch-1.10-red)
![MMDetection](https://img.shields.io/badge/MMDetection-2.28.2-green)
![MMCV](https://img.shields.io/badge/MMCV-1.6.1-orange)
![OpenMMLab](https://img.shields.io/badge/OpenMMLab-Compatible-success)

</div>

---

# Project Overview

This project was developed for the **Yugma TechFest 2.0 – MedhaDrishti National-Level AI Hackathon** under the track:

> **AI for Multimodal RGB-Thermal Pedestrian Detection through Efficient Fusion Strategies**

The project improves the baseline **QFDet (Quality-aware RGB-Thermal Fusion Detector)** by introducing:

- CBAM (Convolutional Block Attention Module)
- Gated Cross-Modal Fusion
- Improved fine-tuning strategy using differential learning rates

The objective is to improve pedestrian detection accuracy in challenging drone environments such as:

- Low illumination
- Night scenes
- Small pedestrian detection
- Dense crowd scenarios

---

# Abstract

RGB cameras provide rich texture information but perform poorly under low-light conditions. Thermal cameras capture heat signatures and are robust to illumination changes but lack detailed appearance information.

The baseline QFDet combines both modalities using simple feature concatenation.

In this project, we propose a **CBAM-Enhanced Gated Fusion Strategy**, allowing the network to:

- Learn channel-wise attention
- Learn spatial attention
- Dynamically weight RGB and Thermal features
- Preserve useful modality-specific information before fusion

The proposed method improves detection performance while introducing only a lightweight attention mechanism.

---

# Features

✔ RGB-Thermal Multimodal Pedestrian Detection

✔ QFDet Baseline

✔ CBAM Attention Module

✔ Gated Feature Fusion

✔ Fine-tuning from Pretrained Weights

✔ MMDetection Framework

✔ Experimental Evaluation

---

# Dataset

Dataset used:

**VTUAV-det Curated Subset**

Contains

- 1200 Training image pairs
- 300 Validation image pairs
- 200 Test image pairs

Only one class:

```
Pedestrian
```

Dataset includes

- RGB images
- Thermal images
- COCO annotations

---

# Baseline Architecture

```
RGB Image
        │
        ▼
ResNet50 Backbone
        │
        ▼
FPN
        │

                QFDet Quality Estimation
                        │
Thermal Image           │
        │               │
        ▼               ▼
ResNet50 Backbone      Quality Maps
        │
        ▼
FPN
        │
        ▼
Fusion
        │
        ▼
Detection Head
```

---

# Proposed Architecture

The proposed model introduces two improvements.

## 1. CBAM Attention

Applied separately to

- RGB Features
- Thermal Features

CBAM performs

- Channel Attention
- Spatial Attention

before feature fusion.

---

## 2. Gated Cross Modal Fusion

Instead of simple concatenation,

the network learns

```
RGB Weight

Thermal Weight
```

using global pooling and a lightweight gating network.

This enables adaptive fusion according to scene conditions.

Example

- Bright scene → RGB receives higher weight

- Dark scene → Thermal receives higher weight

---

# Project Workflow

```
Dataset

↓

Dataset Exploration

↓

Dataset Analysis

↓

Baseline Benchmarking

↓

Architecture Study

↓

CBAM + Gated Fusion

↓

Implementation

↓

Fine-tuning

↓

Evaluation

↓

Final Results
```

---

# Experimental Results

| Model | mAP |
|---------|------|
| RGB Only | 0.041 |
| Thermal Only | 0.232 |
| Original QFDet | 0.299 |
| Proposed Model (Run 1) | 0.284 |
| Proposed Model (Run 2) | **0.326** |

---

## Best Model Performance

| Metric | Value |
|----------|--------|
| mAP | **0.326** |
| mAP50 | **0.712** |
| mAP75 | **0.251** |
| mAP Small | **0.130** |
| mAP Medium | **0.311** |
| mAP Large | **0.572** |

The proposed model achieved better performance than the original QFDet baseline after applying differential learning rates for the newly added fusion layers.

---

# Repository Structure

```
RGBT-Pedestrian-Detection/

│

├── configs/

├── mmdet/

├── tools/

├── checkpoints/

│      best_qfdet_cbam_gated.pth

│

├── notebooks/

│

├── report/

│      Project_Report.pdf

│

├── presentation/

│      Project_Presentation.pptx

│

├── results/

│      qualitative_results/

│      comparison_graphs/

│

├── demo/

│      demo_video.mp4

│

├── requirements.txt

├── README.md

└── LICENSE
```

---

# Installation

Clone the repository

```bash
git clone https://github.com/<YOUR_USERNAME>/RGBT-Pedestrian-Detection.git

cd RGBT-Pedestrian-Detection
```

Install dependencies

```bash
pip install -r requirements.txt
```

---

# Training

Download the pretrained QFDet checkpoint.

Place it inside

```
checkpoints/
```

Train

```bash
python tools/train.py configs/qfdet_r50_fpn_1x_vtuav.py
```

---

# Testing

```bash
python tools/test.py \
configs/qfdet_r50_fpn_1x_vtuav.py \
checkpoints/best_qfdet_cbam_gated.pth \
--eval bbox
```

---

# Demo

Run inference

```bash
python demo/image_demo.py
```

Sample qualitative outputs are available in

```
results/
```

---

# Deliverables

This repository contains

- Source Code
- Trained Model
- Presentation (PPT)
- Project Report
- Demo Video
- Experimental Results
- README
- Requirements File

---

# Future Work

Possible improvements include

- Transformer-based RGB-Thermal Fusion
- Cross Attention Fusion
- Knowledge Distillation
- Lightweight deployment for UAV edge devices
- Real-time optimization

---

# Acknowledgements

This project is based on

**QFDet: Quality-aware RGB-Thermal Fusion Detector**

implemented using

- OpenMMLab
- MMDetection
- PyTorch

Dataset

VTUAV-det Dataset

---

# Authors

**Bhargavi Bayar**

B.Tech Cyber Security & Cyber Forensics

Srinivas University Institute of Engineering and Technology

Yugma TechFest 2.0 Hackathon Submission

---

# References

1. Zhang et al., Drone-based RGB-Thermal Tiny Person Detection, ISPRS Journal of Photogrammetry and Remote Sensing, 2023.

2. MMDetection Documentation

3. OpenMMLab

4. VTUAV-det Dataset

5. QFDet GitHub Repository

---

## License

This project is developed for academic and hackathon purposes. Please refer to the original QFDet repository and VTUAV-det dataset licenses before any commercial use.
