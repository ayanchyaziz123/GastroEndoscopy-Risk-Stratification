# Beyond Binary: Four-Class Risk Stratification from Gastrointestinal Endoscopy Using Asymmetric-Cost CNN-Transformer Learning and Demographic Equity Analysis

**Deep Transfer Learning aligned with ACG/ESGE Clinical Practice Guidelines**

> **Author:** Azizur Rahman
> **Affiliation:** Indiana Wesleyan University · RadTH Technologies
> **Target Venue:** Computers in Biology and Medicine

---

## Why This Matters

Gastrointestinal cancers account for over 3.5 million deaths annually. Early-stage lesions are missed in up to **26% of endoscopic procedures** due to subtle mucosal changes and operator fatigue. Existing AI systems reduce this nuanced clinical decision to a binary output — lesion present or absent — that does not map to any actionable endoscopic classification system.

This paper presents the **first CNN-vs-Transformer benchmark** for four-class GI lesion risk stratification, directly aligned with ACG/ESGE clinical practice guidelines.

---

## 4-Class Clinical Risk Stratification Schema (ACG/ESGE Guideline-Aligned)

| Class | Label | HyperKvasir Sources | Clinical Action |
|---|---|---|---|
| 0 | Normal | normal-cecum, normal-pylorus, normal-z-line, retroflex-stomach, retroflex-rectum, ileum, bbps-2-3 | Routine surveillance interval |
| 1 | Inflammatory / Low-Risk | esophagitis-a, ulcerative-colitis-0-1, ulcerative-colitis-1, hemorrhoids | Medical management + annual follow-up |
| 2 | Pre-malignant / Moderate-Risk | barretts, barretts-short-segment, esophagitis-b-d, polyp, ulcerative-colitis-1-2, ulcerative-colitis-2 | Biopsy required + 3–6 month surveillance |
| 3 | High-Risk / Immediate Intervention | ulcerative-colitis-2-3, ulcerative-colitis-3, dyed-lifted-polyps, dyed-resection-margins | Resection / oncology referral |

---

## Key Contributions

1. **ACG/ESGE-aligned label schema** — First CNN-Transformer benchmark trained on four clinical risk tiers derived from published society guidelines
2. **Asymmetric Endoscopy Loss (AEL)** — High-Risk class penalized 5× more; reduces missed-intervention rate
3. **CNN vs Transformer comparison** — DenseNet-121, EfficientNet-B4, ViT-B/16, Swin-T benchmarked on identical task
4. **Cross-dataset generalization** — Train on HyperKvasir (110K images); validate on Kvasir-v2
5. **GradCAM explainability** — Localizes mucosal pit patterns, vascular irregularities, and ulcerated margins per risk tier
6. **MC Dropout uncertainty** — Flags Pre-malignant/High-Risk lesions for mandatory endoscopist review
7. **AEL ablation study** — AEL vs Cross-Entropy vs Focal Loss comparison
8. **Endoscopist workload simulation** — Quantifies burden reduction with zero missed High-Risk lesions
9. **CD-CTEI fairness** — Equity analysis across age and sex demographic subgroups

---

## Dataset

### Primary: HyperKvasir
- **110,079 images**, 23 GI finding classes
- Download: [osf.io/mkzcq](https://osf.io/mkzcq/)
- Place at: `data/HyperKvasir/labeled-images/<class-folder>/`

### External Validation: Kvasir-v2
- **8,000 images**, 8 classes
- Download: [datasets.simula.no/kvasir](https://datasets.simula.no/kvasir/)
- Place at: `data/Kvasir-v2/<class-folder>/`

---

## Project Structure

```
GastroEndoscopy-Risk-Stratification/
├── GastroEndoscopy_Risk_Stratification.ipynb   # Main notebook
├── GastroEndoscopy_Paper.docx                  # Full paper
├── README.md
├── requirements.txt
├── generate_paper.py                           # Generates paper docx
├── checkpoints/
│   ├── densenet121/best.pt
│   ├── efficientnet_b4/best.pt
│   ├── vit_b16/best.pt
│   └── swin_t/best.pt
└── data/
    ├── HyperKvasir/
    │   └── labeled-images/
    │       ├── normal-cecum/
    │       ├── polyp/
    │       ├── barretts/
    │       └── ... (23 folders)
    └── Kvasir-v2/
        ├── esophagitis/
        ├── polyps/
        └── ... (8 folders)
```

---

## Notebook Sections

| # | Section |
|---|---------|
| 1 | Environment Setup |
| 2 | Dataset Loading & 4-Class Label Mapping |
| 3 | Data Augmentation & DataLoader (CLAHE) |
| 4 | Model Architecture (DenseNet-121, EfficientNet-B4, ViT-B/16, Swin-T) |
| 5 | Asymmetric Endoscopy Loss (AEL) |
| 6 | Training with Transfer Learning |
| 7 | AEL Ablation Study |
| 8 | Cross-Dataset Evaluation (Kvasir-v2) |
| 9 | ROC-AUC Curves |
| 10 | GradCAM Explainability |
| 11 | Monte Carlo Dropout Uncertainty |
| 12 | Endoscopist Workload Simulation |
| 13 | Cross-Demographic Equity (CD-CTEI) |
| 14 | Results Summary & Paper Tables |

---

## Quick Start

```bash
# 1. Install dependencies
pip install -r requirements.txt

# 2. Download HyperKvasir from osf.io/mkzcq and place in data/HyperKvasir/
# 3. Download Kvasir-v2 and place in data/Kvasir-v2/

# 4. Run notebook
jupyter notebook GastroEndoscopy_Risk_Stratification.ipynb
```

---

## Requirements

```
torch>=2.0.0
torchvision>=0.15.0
timm>=0.9.0
scikit-learn>=1.3.0
pandas numpy matplotlib seaborn tqdm
grad-cam opencv-python pillow
```
