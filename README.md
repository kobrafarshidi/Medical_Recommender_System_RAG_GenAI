
# 🩺 Personalized Medical Recommendation & RAG System

### (BioBERT + FAISS + Intent-Aware Re-ranking + Knowledge Graph + Flan-T5)

This repository presents an **end-to-end personalized medical literature recommendation system** that integrates **dense retrieval**, **user modeling**, **intent-aware re-ranking**, **knowledge-guided scoring**, and **Retrieval-Augmented Generation (RAG)** for explainable medical recommendations.

Unlike traditional medical QA systems, this project goes beyond retrieval by incorporating **personalization, user interaction history, and clinical intent**, making it a **full-fledged content-based recommender system for biomedical literature**.

---

## ✨ Key Contributions & Features

### 🔍 Retrieval & Representation

* **BioBERT-based dense embeddings** for biomedical text
* **FAISS vector index** for scalable similarity search
* Sentence-aware and chunk-based document indexing

### 🧠 Recommendation Intelligence

* 👤 **User Modeling**

  * Interaction history (clicked PMIDs)
  * Dynamic user embeddings
* 🎯 **Intent-Aware Recommendation**

  * Automatic intent classification (treatment, diagnosis, review, education)
  * Intent-specific ranking bias
* 🧬 **Knowledge-Enhanced Scoring**

  * Biomedical entity extraction (SciSpacy)
  * Entity overlap & co-occurrence graph signals
* 🔁 **Personalized Re-ranking**

  * Combines relevance, intent, personalization, and knowledge overlap

### 📚 RAG & Explainability

* **Retrieval-Augmented Generation (RAG)** using Flan-T5
* Sentence-level context selection
* **Explainable recommendations with PMIDs**
* Natural language explanations of *why* articles were recommended

### 🖥️ Interactive System

* Jupyter / Colab-based GUI
* Real-time querying and personalized recommendations
* Transparent recommendation reasoning

---

## 🧱 System Architecture

```
User Query
   ↓
Text Preprocessing
(cleaning + abbreviation expansion)
   ↓
BioBERT Encoder
(Dense Biomedical Embeddings)
   ↓
FAISS Vector Search
(Top-N Candidate Chunks)
   ↓
Intent Classification
(User Query)
   ↓
Personalized Re-ranking
 ├─ User Embedding Similarity
 ├─ Intent Bias
 ├─ Knowledge Graph Entity Overlap
 └─ Relevance Score
   ↓
Top-K Recommended Articles
(PMID-level)
   ↓
Sentence-level Context Selection
   ↓
Flan-T5 (RAG)
   ↓
Explainable Medical Recommendation
(with citations)
```

---

## 📚 Dataset

* **Source**: `slinusc/PubMedAbstractsSubset` (HuggingFace Datasets)
* **Domain**: Biomedical & clinical literature
* **Content**:

  * PubMed article titles
  * PubMed abstracts
* **Subset Size**: 1,000 abstracts (configurable)

### Document Processing Pipeline

Each document undergoes:

1. Noise removal & normalization
2. **Medical abbreviation expansion**

   * e.g., *MI → myocardial infarction*
3. Sentence segmentation
4. Chunking with maximum word constraints
5. Minimum-length filtering for semantic validity

---

## 🔬 Models & Tools

### 🔹 Retrieval Encoder

* **BioBERT**

  * `dmis-lab/biobert-base-cased-v1.1`
  * Domain-specific biomedical representation

### 🔹 Biomedical NLP

* **SciSpacy**

  * Entity extraction
  * Knowledge-aware overlap scoring
* **NetworkX**

  * Lightweight entity co-occurrence graph construction

### 🔹 Generator (LLM)

* **Flan-T5**

  * `google/flan-t5-base`
  * Context-grounded explanation generation

---

## 👤 User Modeling & Personalization

The system maintains a lightweight but effective **user profile**:

```python
user_profile = {
  user_id,
  specialty,
  intent_bias,
  clicked_pmids
}
```

### User Embedding Construction

* Aggregates embeddings of previously interacted documents
* Enables **content-based personalization**
* No collaborative data required (cold-start friendly)

---

## 🧮 Recommendation Scoring Function

Each candidate document is ranked using a composite score:

```
Final Score =
  Relevance
× Intent Weight
× Personalization Score
× Knowledge Overlap Score
```

Where:

* **Relevance**: FAISS retrieval
* **Intent Weight**: task-specific bias
* **Personalization**: user-document embedding similarity
* **Knowledge Overlap**: shared biomedical entities

---

## 🖥️ Interactive GUI

Built using `ipywidgets`, the interface allows users to:

* Enter biomedical or clinical queries
* Receive **personalized article recommendations**
* View:

  * Candidate PMIDs (before re-ranking)
  * Final recommended PMIDs
  * Natural language explanation with citations

Designed for:

* Research demos
* User studies
* Qualitative evaluation

---

## ⚙️ Installation

```bash
pip install transformers torch faiss-cpu datasets tqdm scikit-learn ipywidgets
pip install spacy scispacy networkx
```

Additional setup:

```bash
python -m spacy download en_core_sci_sm
```

**Recommended:**

* Python ≥ 3.8
* GPU (optional, improves encoding speed)

---

## 🚀 Usage

1. Clone the repository
2. Open the notebook in **Google Colab** or **Jupyter**
3. Build or load the FAISS index
4. Initialize user profile
5. Submit medical queries via the GUI
6. Inspect recommendations and explanations

---

## 🧪 Example Query

**Query**

> What treatment strategies are recommended for myocardial infarction?

**System Output**

* 📌 Personalized PubMed recommendations (PMIDs)
* 🧠 Intent-aware ranking (treatment-focused)
* 🧬 Entity-consistent evidence
* 📄 Explainable rationale generated via RAG

---

## ⚠️ Disclaimer

This system is **strictly for research and educational purposes**.
It is **not intended for clinical diagnosis or decision-making**.

---

## 📌 Future Work

* Larger-scale PubMed indexing
* Domain-specific biomedical cross-encoders
* Temporal user modeling
* Citation-aware multi-document generation
* Web-based interface (Streamlit / FastAPI)
* Multilingual medical recommendation

---

## 🙏 Acknowledgements

* HuggingFace Transformers & Datasets
* FAISS (Meta AI)
* PubMed / NCBI
* BioBERT Authors
* SciSpacy
* Google Flan-T5

---

