# Benchmarking Monocular Depth Estimation Models

**Semester Project for the course "Advanced Artificial Intelligence"** **School of Electrical and Computer Engineering (ECE), National Technical University of Athens (NTUA)**

![Kaggle](https://img.shields.io/badge/Platform-Kaggle-20BEFF?logo=kaggle&logoColor=white)
![Python](https://img.shields.io/badge/Python-3.10%2B-blue?logo=python&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green)

---

## Overview
This repository contains the codebase and final report for a comparative study on **Monocular Depth Estimation (MDE)**. The project benchmarks state-of-the-art **Foundation Models** (e.g., Depth Anything V2, Marigold) against specialized baselines in a **Zero-Shot** setting.

The goal is to evaluate **Domain Generalization**—how well models trained on mixed datasets perform on unseen Indoor (NYU) and Outdoor (KITTI) environments without fine-tuning.

### Key Features
* **Zero-Shot Evaluation:** No fine-tuning on test sets.
* **Diverse Architectures:** Transformers (DAV2, ZoeDepth, MiDaS v3.0) and Diffusion Models (Marigold).
* **Robust Pipeline:** Includes Least-Squares Alignment for relative depth and specific cropping strategies (Eigen/Garg) for each dataset.
* **Comprehensive Metrics:** AbsRel, $\delta_1$ Accuracy, and SILog.

---

## Evaluated Models

Evaluated 7 model variants across different paradigms:

| Model Family | Variant | Type | Hugging Face |
| :--- | :--- | :--- | :--- |
| **Depth Anything V2** | `DAV2-Large` | Relative | [Link](https://huggingface.co/depth-anything/Depth-Anything-V2-Large-hf) |
| | `DAV2-Indoor-Metric` | Metric | [Link](https://huggingface.co/depth-anything/Depth-Anything-V2-Metric-Indoor-Large-hf) |
| | `DAV2-Outdoor-Metric` | Metric | [Link](https://huggingface.co/depth-anything/Depth-Anything-V2-Metric-Outdoor-Large-hf) |
| **ZoeDepth** | `ZoeDepth` | Metric | [Link](https://huggingface.co/Intel/zoedepth-nyu-kitti) |
| **MiDaS** | `MiDaS-3.0` | Relative | [Link](https://huggingface.co/Intel/dpt-large) |
| | `MiDaS-3.1` | Relative | [Link](https://huggingface.co/Intel/dpt-beit-large-512) |
| **Marigold** | `Marigold-1.1` | Relative | [Link](https://huggingface.co/prs-eth/marigold-depth-v1-1) |

---

## Datasets

The benchmarking was conducted on three heterogeneous datasets to test robustness:

| Dataset | Description | Kaggle |
| :--- | :--- | :--- |
| **IBims-1** | Indoor scenes with high-quality ground truth. Used to test edge preservation and transparency handling. | [Link](https://www.kaggle.com/datasets/patiencechewyeecheah/ibims-1) |
| **NYU Depth V2** | The standard indoor benchmark. Evaluated using **Eigen Crop**. | [Link](https://www.kaggle.com/datasets/soumikrakshit/nyu-depth-v2) |
| **KITTI** | Outdoor autonomous driving scenes. Evaluated using **Garg Crop**. | [Link](https://www.kaggle.com/datasets/artemmmtry/kitti-depth-prediction-evaluation) |

---

## Methodology & Pipeline

The evaluation pipeline follows these steps:

1.  **Preprocessing:** Resize input images to model-specific resolution (e.g., 518x518 for DAV2).
2.  **Inference:** Generate depth maps.
    * *Diffusion:* Marigold uses defined denoising steps.
    * *Transformers:* Standard forward pass.
3.  **Post-Processing:**
    * Resize predictions back to original resolution.
    * **Alignment:** Apply Least-Squares Scale & Shift alignment for Relative Depth models.
    * **Inverse:** Invert disparity maps (for MiDaS) to depth.
4.  **Evaluation:** Compute metrics only on valid pixels defined by the **validity mask** and specific **crops** (Eigen/Garg).

---

## Results
![absrel_broken](/report/images/absrel_broken.png)
![delta1](/report/images/delta1.png)
![silog](/report/images/silog.png)
![visual-ibims](/report/images/visual-ibims.png)
![domain_gap](/report/images/domain_gap.png)
