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
