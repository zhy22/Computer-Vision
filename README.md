# 📖 AI-Powered Book Page Digitisation Pipeline

A multi-modal AI pipeline that transforms scanned book pages into spoken audio — combining computer vision, OCR, large vision-language models, and text-to-speech synthesis into a single reproducible workflow.

---

## 🧠 What It Does

1. **Detects image orientation** using a custom-trained CNN classifier (flip/notflip)
2. **Extracts text** from the corrected image using EasyOCR and LLaVA-1.6 (a vision-language model)
3. **Synthesises speech** from the extracted text using the CSM-1B model
4. **Outputs a `.wav` audio file** — turning a static page into spoken content

---

## 🗂️ Project Structure

```
book_pipeline/
├── data/
│   ├── raw/                  # Input images (DVC-tracked)
│   └── processed/            # OCR JSON outputs (DVC-tracked)
├── src/
│   ├── run_ocr.py            # EasyOCR extraction script
│   └── test_ocr.py           # Unit tests for pipeline outputs
├── dvc.yaml                  # DVC pipeline definition
├── requirements.txt
└── README.md
```

---

## 🔧 Tech Stack

| Component | Tool / Framework |
|---|---|
| Image Classification | PyTorch (custom CNN) |
| OCR | EasyOCR |
| Vision-Language Model | LLaVA-v1.6-Mistral-7B (HuggingFace) |
| Text-to-Speech | CSM-1B (Sesame, HuggingFace) |
| Pipeline Versioning | DVC + Git |
| Data Augmentation | torchvision transforms |
| Evaluation | scikit-learn (classification report, ROC, confusion matrix) |
| Environment | Google Colab + Google Drive |

---

## 🏗️ Model Architecture — Flip Classifier

A custom 4-block CNN built in PyTorch to classify whether an input image is correctly oriented before passing it downstream.

```
Input (128×128×3)
  → Conv2d(3, 32) + BatchNorm + ReLU + MaxPool     # → 64×64×32
  → Conv2d(32, 64) + BatchNorm + ReLU + MaxPool    # → 32×32×64
  → Conv2d(64, 128) + BatchNorm + ReLU + MaxPool   # → 16×16×128
  → Conv2d(128, 256) + BatchNorm + ReLU + MaxPool  # → 8×8×256
  → Flatten → Linear(16384, 256) → ReLU → Dropout(0.5)
  → Linear(256, 1) → Sigmoid
```

**Training config:**
- Optimiser: Lion (`lion-pytorch`)
- Learning rate: `3e-4` with early stopping (patience = 2)
- Batch size: 64 | Image size: 96×96 | Max epochs: 50
- Augmentation: RandomHorizontalFlip, RandomRotation, ColorJitter

---

## ⚙️ Pipeline — DVC Stages

```yaml
stages:
  ocr:
    cmd: python src/run_ocr.py
    deps: [src/run_ocr.py, data/raw/page.jpg]
    outs: [data/processed/ocr_result.json]

  test:
    cmd: python src/test_ocr.py
    deps: [src/test_ocr.py, data/processed/ocr_result.json]
```

Reproduce the full pipeline with:

```bash
dvc repro
```

---

## 🚀 Getting Started

### 1. Clone the repo

```bash
git clone https://github.com/your-username/book-pipeline.git
cd book-pipeline
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Add your input image

Place your scanned book page at:

```
data/raw/page.jpg
```

### 4. Run the pipeline

```bash
dvc repro
```

### 5. Play the output audio

The synthesised speech will be saved to:

```
llava_ocr_speech.wav
```

---

## ✅ Tests

Unit tests validate that OCR outputs exist and are non-empty:

```bash
python src/test_ocr.py
```

Expected output:

```
All tests passed ✓
```

---

## 📊 Evaluation (Flip Classifier)

Model performance is evaluated on a held-out test set using:

- Classification report (precision, recall, F1)
- Confusion matrix (seaborn heatmap)
- ROC curve + AUC score

---

## 📋 Requirements

```
torch
torchvision
transformers
accelerate
easyocr
lion-pytorch
dvc
scikit-learn
matplotlib
seaborn
Pillow
tqdm
```

---

## 📌 Notes

- Designed and tested on **Google Colab** with GPU acceleration
- DVC remote storage configured via **Google Drive**
- LLaVA and CSM models are loaded from **HuggingFace Hub** (login required)

---

## 👤 Author

**Hongyu Zhou**  
