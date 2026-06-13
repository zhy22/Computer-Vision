<!-- ===== HEADER BANNER ===== -->
<div align="center">

![Header](https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=12,20,24,30&height=240&section=header&text=Book%20Page%20Digitisation%20Pipeline&fontSize=38&fontColor=ffffff&animation=fadeIn&fontAlignY=38&desc=Scanned%20Pages%20→%20OCR%20→%20Vision-Language%20Models%20→%20Spoken%20Audio%20🔊&descAlignY=58&descSize=15)

[![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white)](https://pytorch.org/)
[![Hugging Face](https://img.shields.io/badge/🤗%20Hugging%20Face-FFD21E?style=for-the-badge)](https://huggingface.co/)
[![EasyOCR](https://img.shields.io/badge/EasyOCR-1E90FF?style=for-the-badge)](https://github.com/JaidedAI/EasyOCR)
[![DVC](https://img.shields.io/badge/DVC-945DD6?style=for-the-badge&logo=dvc&logoColor=white)](https://dvc.org/)
[![Colab](https://img.shields.io/badge/Google%20Colab-F9AB00?style=for-the-badge&logo=googlecolab&logoColor=white)](https://colab.research.google.com/)
[![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](#)

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=600&size=20&pause=1000&color=945DD6&center=true&vCenter=true&width=720&lines=Custom+CNN+orientation+classifier;EasyOCR+%2B+LLaVA-1.6+text+extraction;CSM-1B+neural+text-to-speech;Fully+reproducible+with+DVC+%2B+Git+" alt="Typing animation" />

</div>

---

## 🧠 What It Does

A **multi-modal AI pipeline** that transforms scanned book pages into spoken audio — combining computer vision, OCR, large vision-language models, and text-to-speech synthesis into a single reproducible workflow.

> 🎯 **One command in, one `.wav` file out.** From a static scanned page to a fully narrated audio clip via `dvc repro`.

<table>
<tr>
<td width="50%">

### 1️⃣ Orient
Detect image orientation using a custom-trained **CNN classifier** (flip / notflip).

</td>
<td width="50%">

### 2️⃣ Extract
Pull text from the corrected image with **EasyOCR** + **LLaVA-1.6** vision-language model.

</td>
</tr>
<tr>
<td width="50%">

### 3️⃣ Synthesise
Generate natural-sounding speech from the extracted text using the **CSM-1B** model.

</td>
<td width="50%">

### 4️⃣ Output
Save a final **`.wav` audio file** — turning a static page into spoken content.

</td>
</tr>
</table>

---

## 🔁 Pipeline Flow

```mermaid
flowchart LR
    A[📄 Scanned Page] -->|Input| B[CNN Flip<br/>Classifier 📐]
    B -->|Correct orientation| C[EasyOCR<br/>Text Extraction 🔍]
    C --> D[LLaVA-1.6<br/>Vision-Language 🧠]
    D --> E[CSM-1B<br/>Text-to-Speech 🔊]
    E --> F[🎧 .wav Audio]

    style A fill:#FFD700,stroke:#000,color:#000
    style B fill:#EE4C2C,stroke:#fff,color:#fff
    style D fill:#945DD6,stroke:#fff,color:#fff
    style E fill:#1E90FF,stroke:#fff,color:#fff
    style F fill:#34A853,stroke:#fff,color:#fff
```

---

## 🗂️ Project Structure
---

## 🔧 Tech Stack

<div align="center">

| Component | Tool / Framework |
|:---|:---|
| 🖼️ **Image Classification** | ![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white) Custom CNN |
| 🔍 **OCR** | ![EasyOCR](https://img.shields.io/badge/EasyOCR-1E90FF?style=flat-square) |
| 🧠 **Vision-Language Model** | ![LLaVA](https://img.shields.io/badge/LLaVA--v1.6--Mistral--7B-FFD21E?style=flat-square) (HuggingFace) |
| 🔊 **Text-to-Speech** | ![CSM-1B](https://img.shields.io/badge/CSM--1B-Sesame-9146FF?style=flat-square) (HuggingFace) |
| ⚙️ **Pipeline Versioning** | ![DVC](https://img.shields.io/badge/DVC-945DD6?style=flat-square&logo=dvc&logoColor=white) + ![Git](https://img.shields.io/badge/Git-F05032?style=flat-square&logo=git&logoColor=white) |
| 🎨 **Data Augmentation** | ![torchvision](https://img.shields.io/badge/torchvision-EE4C2C?style=flat-square) transforms |
| 📊 **Evaluation** | ![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=flat-square&logo=scikit-learn&logoColor=white) |
| ☁️ **Environment** | ![Colab](https://img.shields.io/badge/Colab-F9AB00?style=flat-square&logo=googlecolab&logoColor=white) + ![Drive](https://img.shields.io/badge/Drive-4285F4?style=flat-square&logo=googledrive&logoColor=white) |

</div>


<table>
<tr>
<td width="50%">

### ⚙️ Training Config
- **Optimiser:** Lion (`lion-pytorch`)
- **Learning rate:** `3e-4`
- **Early stopping:** patience = 2
- **Batch size:** 64
- **Image size:** 96×96
- **Max epochs:** 50

</td>
<td width="50%">

### 🎨 Augmentation
- `RandomHorizontalFlip`
- `RandomRotation`
- `ColorJitter`
- Normalisation to ImageNet stats

</td>
</tr>
</table>

---

## ⚙️ DVC Pipeline Stages

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

Reproduce the full pipeline with one command:

```bash
dvc repro
```

---

## 🚀 Getting Started

### 1️⃣ Clone the repo
```bash
git clone https://github.com/your-username/book-pipeline.git
cd book-pipeline
```

### 2️⃣ Install dependencies
```bash
pip install -r requirements.txt
```

### 3️⃣ Add your input image

---

## 🏗️ Model Architecture — Flip Classifier

A custom **4-block CNN** built in PyTorch to classify whether an input image is correctly oriented before passing it downstream.
### 4️⃣ Run the pipeline
```bash
dvc repro
```

### 5️⃣ Play the output audio

---

## ✅ Tests

Unit tests validate that OCR outputs exist and are non-empty:

```bash
python src/test_ocr.py
```

---

## 📊 Evaluation — Flip Classifier

Model performance is evaluated on a held-out test set using:

<table>
<tr>
<td width="33%" align="center">

### 📋 Classification Report
Precision · Recall · F1-score per class

</td>
<td width="33%" align="center">

### 🟦 Confusion Matrix
Seaborn heatmap of predictions vs. truth

</td>
<td width="33%" align="center">

### 📈 ROC Curve
AUC score + threshold analysis

</td>
</tr>
</table>

---

## 📋 Requirements

![torch](https://img.shields.io/badge/torch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white)
![torchvision](https://img.shields.io/badge/torchvision-EE4C2C?style=flat-square)
![transformers](https://img.shields.io/badge/transformers-FFD21E?style=flat-square&logo=huggingface&logoColor=black)
![accelerate](https://img.shields.io/badge/accelerate-FFAA00?style=flat-square)
![easyocr](https://img.shields.io/badge/easyocr-1E90FF?style=flat-square)
![lion-pytorch](https://img.shields.io/badge/lion--pytorch-9146FF?style=flat-square)
![dvc](https://img.shields.io/badge/dvc-945DD6?style=flat-square&logo=dvc&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=flat-square&logo=scikit-learn&logoColor=white)
![matplotlib](https://img.shields.io/badge/matplotlib-11557C?style=flat-square)
![seaborn](https://img.shields.io/badge/seaborn-4C72B0?style=flat-square)
![Pillow](https://img.shields.io/badge/Pillow-306998?style=flat-square)
![tqdm](https://img.shields.io/badge/tqdm-FFC107?style=flat-square)
