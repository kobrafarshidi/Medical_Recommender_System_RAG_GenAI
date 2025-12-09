
---
# Medical_Recommender_System_RAG_GenAI_Diffusion

## Overview

This project implements a **medical recommendation system** using **RAG (Retrieval-Augmented Generation)**, **GenAI (large language model)**, and **diffusion-enhanced embeddings**. It leverages the **PubMed 20k RCT dataset** to provide relevant medical information and educational summaries for research queries.

The system is designed for **educational purposes only** — it does **not provide medical advice**.

---

## Features

* **RAG pipeline**: Retrieves relevant paragraphs from PubMed 20k abstracts and generates coherent summaries.
* **Diffusion-enhanced embeddings**: Improves vector representations for better retrieval accuracy.
* **GPU-ready**: Embeddings, LLM inference, and vector search run on GPU for faster performance.
* **LLM integration**: Uses **BioGPT-Large** for generating natural language explanations.
* **Frontend interface**: Simple **Gradio** web UI for interactive queries.

---

## Dataset

* **PubMed 20k RCT**: A subset of PubMed 200k randomized controlled trials dataset.
* Contains abstracts from medical research papers, labeled by sentence roles.
* Dataset URL: [HuggingFace pubmed-rct20k](https://huggingface.co/datasets/armanc/pubmed-rct20k)
* The dataset is automatically downloaded and parsed in Colab.

---

## Installation & Requirements

Run in **Google Colab** with GPU enabled:

```bash
!pip install datasets sentence-transformers faiss-gpu transformers torch accelerate gradio --quiet
```

---

## Usage

1. Run the notebook cells sequentially.

2. The system will:

   * Download and parse the PubMed 20k RCT dataset.
   * Generate embeddings for abstracts using **allenai-specter**.
   * Apply diffusion to improve embeddings.
   * Build a **FAISS vector index** for similarity search.
   * Use **BioGPT-Large** to generate research summaries.
   * Launch a **Gradio UI** for interactive queries.

3. Example query:

```python
query = "Latest treatments for type 2 diabetes complications"
print(rag_medical(query))
```

---

## How It Works

1. **Query embedding** → converts your input to vector using the embedding model.
2. **Vector search** → finds top-k most similar paragraphs in PubMed dataset.
3. **Prompt preparation** → retrieved paragraphs are formatted as input to LLM.
4. **LLM generation** → BioGPT produces an educational summary.

---

## Notes

* Designed for **educational and research purposes only**.
* Requires GPU in Colab for optimal performance.
* Only the first few paragraphs are used during testing; for full-scale use, embeddings can be generated for all abstracts.
* Can be extended with **diffusion transformers**, **Qdrant or Weaviate vector DB**, or **frontend web frameworks** for production.

---

## License  

This project uses **PubMed data**; please check copyright information from [NLM](https://www.nlm.nih.gov/web_policies.html#copyright).

The code itself is **MIT License** (or specify your preferred license).



---
