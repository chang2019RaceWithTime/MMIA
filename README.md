# 🔍 MMIA: Membership Inference Attacks on Multimodal Federated Learning

> **Paper:** *The Hidden Risk: Membership Inference Attacks on Multimodal Federated Learning via Modality Imbalance*

This repository contains the implementation of our paper, which reveals a privacy vulnerability in multimodal federated learning. We show that the natural imbalance between modalities (e.g., audio vs. visual) can be exploited to mount effective **Membership Inference Attacks (MIA)**.

---

## 📁 Repository Structure

```
MMIA/
├── main_multimodal.py                          # Step 1: Train multimodal model & log intermediate variables
├── training_construct_lira_opti.py             # Step 2: Build attack dataset from intermediate variables
├── attack_model_training.py                    # Step 3: Train the attack model
├── attack_models.py                            # Attack model architectures
├── crient_function.py                          # Client-side utility functions
├── experiments/                                # Federated learning experiment configs
├── models/                                     # Multimodal model definitions
├── utils/                                      # Data loading & sampling utilities
└── requirements.txt                            # Dependencies
```

---

## 🚀 Attack Pipeline

### Step 1 — Train the Multimodal Federated Model

```bash
python main_multimodal.py
```

Trains a multimodal (audio + visual) model under federated learning and logs per-sample intermediate variables (losses, gradients, confidence scores) during training.

---

### Step 2 — Construct the Attack Dataset

```bash
python training_construct_lira_opti.py
```

Builds a structured attack dataset from the logged intermediate variables, where each sample is labeled Member or Non_Member and enriched with modality-specific features including the modality gap signal (audio loss − visual loss).

---

### Step 3 — Train the Attack Model

```bash
python attack_model_training.py
```

Trains a membership inference classifier on the attack dataset. Evaluated by AUC, TPR @ low FPR, and Balanced Accuracy.

---

## ⚙️ Setup

```bash
pip install -r requirements.txt
```

| Package | Version |
|---------|---------|
| torch | 2.6.0+cu126 |
| torchvision | 0.21.0+cu126 |
| numpy | 2.4.4 |
| pandas | 3.0.2 |
| scikit-learn | 1.8.0 |
| librosa | 0.11.0 |
| opacus | 1.5.4 |
| seaborn | 0.13.2 |

## 📦 Datasets

This project is evaluated on three multimodal datasets:

- **CREMA-D** — Crowd-sourced emotional multimodal actors dataset (audio + visual) [[Paper]](https://doi.org/10.1109/TAFFC.2014.2336244)
- **AVE** — Audio-Visual Event localization dataset [[Paper]](https://www.ecva.net/papers/eccv_2018/papers_ECCV/html/Yapeng_Tian_Audio-Visual_Event_Localization_ECCV_2018_paper.php)
- **Balanced** — Balanced Audiovisual Dataset for Imbalance Analysis [[Paper]](https://arxiv.org/abs/2302.10912)

Please refer to the respective papers for download and usage instructions.

---

## 🔗 Based On

Built upon **[FedMIA](https://github.com/Liar-Mask/FedMIA)** — thanks to the authors for their open-source implementation.

---

## 📄 Citation

```bibtex
@inproceedings{
anonymous2026the,
title={The Hidden Risk: Membership Inference Attacks on Multimodal Federated Learning via Modality Imbalance},
author={Anonymous},
booktitle={Forty-third International Conference on Machine Learning},
year={2026},
url={https://openreview.net/forum?id=p3Cgr7EgTZ}
}
```
