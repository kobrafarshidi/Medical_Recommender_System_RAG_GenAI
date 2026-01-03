# 🩺 Medical RAG System (FAISS + BioBERT + Cross-Encoder + Flan-T5)

This repository contains an **end-to-end Medical Retrieval-Augmented Generation (RAG) system** built with **BioBERT embeddings**, **FAISS vector search**, **optional Cross-Encoder re-ranking**, and **Flan-T5** for answer generation. The project also includes **retrieval evaluation metrics** and an **interactive GUI** for querying medical questions.

---

## ✨ Key Features

* 🔍 **Dense Retrieval** using BioBERT embeddings
* ⚡ **FAISS** for fast similarity search
* 🎯 **Cross-Encoder Re-ranking** (optional) for higher precision
* 🧠 **Flan-T5** for natural language answer generation
* 📊 **Evaluation Metrics**: Precision@K, Recall@K, MRR, NDCG
* 🧩 **Medical Text Preprocessing** (abbreviation expansion, chunking)
* 🖥️ **Interactive GUI** (Jupyter / Colab widgets)

---

## 🧱 System Architecture

```
User Query
   ↓
Text Preprocessing (cleaning + abbreviation expansion)
   ↓
BioBERT Encoder (Dense Embeddings)
   ↓
FAISS Vector Search (Top-K Chunks)
   ↓
(Optional) Cross-Encoder Re-ranking
   ↓
Context Aggregation
   ↓
Flan-T5 Generator
   ↓
Final Medical Answer
```

---

## 📚 Dataset

* **Source**: `slinusc/PubMedAbstractsSubset` (HuggingFace Datasets)
* **Domain**: Biomedical & clinical literature
* **Content**: PubMed article titles and abstracts
* **Subset Size**: 1,000 abstracts (for experimentation)

Each document is:

1. Cleaned (noise removal)
2. Expanded using common **medical abbreviations** (e.g., MI → myocardial infarction)
3. Split into **sentence-based chunks**
4. Filtered by minimum length

---

## 🔬 Models Used

### 🔹 Encoder (Retrieval)

* **BioBERT**: `dmis-lab/biobert-base-cased-v1.1`
* Used to generate dense embeddings for queries and document chunks

### 🔹 Re-ranking (Optional)

* **Cross-Encoder**: `cross-encoder/ms-marco-MiniLM-L-6-v2`
* Scores (query, chunk) pairs for better ranking

### 🔹 Generator (LLM)

* **Flan-T5**: `google/flan-t5-base`
* Generates final answers based on retrieved medical context

---

## 📊 Evaluation

The system includes **retrieval evaluation** using article titles as queries and PMIDs as ground truth.

### Implemented Metrics:

* **Precision@10**
* **Recall@10**
* **MRR (Mean Reciprocal Rank)**
* **NDCG@10**

Two settings are compared:

1. **FAISS-only retrieval**
2. **FAISS + Cross-Encoder re-ranking**

This allows quantitative analysis of re-ranking effectiveness.

---

## 🖥️ Interactive GUI

An interactive interface (built with `ipywidgets`) allows users to:

* Enter medical questions (English or Persian UI text)
* Choose retrieval mode:

  * FAISS-only
  * FAISS + Cross-Encoder
* Receive **context-grounded medical answers**

Ideal for demos, experimentation, and qualitative evaluation.

---

## ⚙️ Installation

```bash
pip install transformers torch faiss-cpu datasets tqdm scikit-learn ipywidgets
```

Recommended environment:

* Python ≥ 3.8
* GPU (optional but highly recommended)

---

## 🚀 Usage

1. Clone the repository
2. Run the notebook in **Google Colab** or **Jupyter Notebook**
3. Build the FAISS index
4. Evaluate retrieval performance
5. Ask medical questions via the GUI

---

## 📁 Project Structure

```
├── Untitled12.ipynb        # Main notebook (end-to-end pipeline)
├── faiss_index/
│   ├── pubmed.index       # FAISS index
│   └── metadata.csv       # Chunk metadata (PMID, chunk text)
├── README.md
```

---

## 🧪 Example Query

**Question:**

> What cellular changes occur during myocardial infarction?

**Answer:**

> Generated using PubMed-derived context and Flan-T5 with BioBERT-based retrieval.

---

## ⚠️ Disclaimer

This project is **for research and educational purposes only**.
It is **not intended for clinical decision-making** or medical diagnosis.

---

## 🙏 Acknowledgements

* HuggingFace Transformers & Datasets
* FAISS (Facebook AI Similarity Search)
* PubMed / NCBI
* BioBERT authors
* Google Flan-T5

---

## 📌 Future Improvements

* Multi-document citation-aware generation
* Larger PubMed corpus
* Domain-specific cross-encoders (BioMed MS MARCO)
* Streamlit / Web-based UI
* Multilingual medical QA

---

If you use or build upon this work, please ⭐ the repository!
