# ⚖️ Legal Document Summarizer & Q&A Chatbot

An AI-powered system that **summarizes Indian legal documents** and provides **question–answering capabilities** using advanced NLP models.  
It automates the tedious task of reading lengthy court judgments or legal contracts and allows users to **chat with uploaded PDFs** interactively.

> 🧾 All legal PDFs used for this project were sourced from [**IndianKanoon.org**](https://indiankanoon.org/).

---

## 🚀 Features

- 📑 **Legal PDF Summarization**
  - Extracts text directly from PDFs (with OCR fallback for scanned files).
  - Summarizes cases into structured sections: *Facts*, *Key Arguments*, and *Decision*.

- 💬 **Q&A Chatbot**
  - Users can query uploaded legal documents.
  - Answers are generated using **FLAN-T5**, grounded on retrieved passages.
  
- 🔍 **Semantic Search**
  - Uses **FAISS** with **InLegalBERT** embeddings for efficient legal text retrieval.

- 🧠 **Custom Trained Model**
  - Fine-tuned **FLAN-T5** model for legal summarization using segmented case data.

- 🎨 **Interactive Interface**
  - Built with **Gradio** for simple upload, summarize, and chat functionality.

---

## 🧩 Project Architecture


### 1. `0_extract_text.py`
- Extracts text from legal PDFs using **PyPDF2**.
- Falls back to **Tesseract OCR** if text extraction fails.

### 2. `1_segment_text.py`
- Segments raw text into sections (*Facts, Arguments, Statutes, Decision*) using **KMeans clustering** on **InLegalBERT** embeddings.

### 3. `2_build_index.py`
- Builds a **FAISS** index from segmented JSON data for semantic search.

### 4. `3_train_summarizer.py`
- Fine-tunes **FLAN-T5** (`google/flan-t5-base`) on segmented legal JSONs.
- Outputs a domain-specific summarization model (`models/flan_legal_model`).

### 5. `app.py`
- The main **Gradio** app providing two tabs:
  - **Summarizer** – upload a legal PDF and get structured summary.
  - **Chatbot** – chat with one or multiple uploaded documents.

---

## 🛠️ Tech Stack

| Component | Technology |
|------------|-------------|
| **Language** | Python 3.10+ |
| **Models** | `law-ai/InLegalBERT`, `google/flan-t5-base` |
| **Vector Store** | FAISS |
| **Frameworks** | HuggingFace Transformers, SentenceTransformers |
| **Interface** | Gradio |
| **OCR** | PyPDF2, pdf2image, pytesseract |

---


