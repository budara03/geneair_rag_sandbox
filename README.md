# 🧬 GeneAir RAG Sandbox (`geneair-rag-sandbox`)

> **Experimental Prototype & Development Sandbox**  
> *Context-Aware, Genotype-Grounded Corrective RAG (CRAG) Asthma Management Assistant*

[![Python](https://img.shields.io/badge/Python-3.11-blue.svg)](https://www.python.org/)
[![Vector DB](https://img.shields.io/badge/ChromaDB-Local-orange.svg)](https://www.trychroma.com/)
[![LLM](https://img.shields.io/badge/Ollama-Mistral--7B-green.svg)](https://ollama.com/)
[![Status](https://img.shields.io/badge/Status-Experimental_Sandbox-yellow.svg)]()

## 📌 Overview
This repository serves as an isolated development and testing environment for **Component 3** of the **GeneAir** research project (SLIIT - IT4010 Research Project). 

Before integrating with the main multi-member GeneAir platform, this sandbox is used to build, test, and benchmark the **Genotype-Grounded Clinical RAG Pipeline**. The assistant answers clinician and patient queries grounded in curated asthma guidelines (GINA), SNP-asthma association studies (*ORMDL3*, *ADRB2*, *IL-13*, *GATA3*, *ADAM33*), and pharmacogenomic (PGx) drug-response records (ClinPGx/CPIC/DPWG), running 100% on-premises to preserve genomic data privacy.

---

## 🏗️ Sandbox Objectives
1. **Knowledge Base Pipeline (Offline):** Test PDF/HTML cleaning, section-aware chunking, metadata tagging, and hybrid indexing (ChromaDB vector store + BM25 lexical index).
2. **Genotype Context & Intent Routing:** Prototype the JSON schema normalizer for patient SNP profiles and selectively route genetic context based on query intent.
3. **Hybrid & Corrective Retrieval (CRAG):** Experiment with semantic + keyword retrieval, source-authority weighting, and self-correction loops when initial retrieval is weak or conflicting.
4. **Local LLM Inference & Safety:** Test prompt engineering, inline citation verification, emergency escalation routing, and abstention guardrails using **Ollama (`Mistral-7B`)**.
5. **RAGAS & Ablation Benchmarking:** Evaluate Context Precision@K, Recall@K, Faithfulness, Citation Correctness, and Counterfactual Consistency against baseline RAG setups.

---

## 🛠️ Tech Stack
* **Language:** Python 3.11
* **Vector Database:** ChromaDB (Persistent local storage)
* **Lexical Search:** `rank-bm25` (Exact matching for rsIDs, alleles, gene symbols, and drug names)
* **Embeddings:** Sentence Transformers (`all-MiniLM-L6-v2` / `nomic-embed-text`)
* **Local LLM Runtime:** Ollama serving `Mistral-7B`
* **Evaluation:** RAGAS, NumPy/SciPy (Bootstrap confidence intervals)
* **API Framework (for main repo integration):** FastAPI

---

## 📂 Repository Structure
```text
geneair_rag_sandbox/
├── data/
│   ├── raw/                  # Sample GINA PDFs, PubMed SNP studies, ClinPGx records
│   ├── processed/            # Section-chunked & metadata-tagged JSON files
│   └── synthetic_profiles/   # Mock patient genotype & clinical JSON profiles
├── db/
│   ├── chroma_db/            # Local ChromaDB vector store (git-ignored)
│   └── bm25_index.pkl        # Serialized BM25 lexical index
├── src/
│   ├── indexing/             # Document loader, section chunker, hybrid indexer
│   ├── routing/              # Genotype normalizer & query intent classifier
│   ├── retrieval/            # Hybrid search, reranker, & CRAG evaluator
│   ├── generation/           # Ollama client, grounded prompts, & safety verifier
│   └── api/                  # FastAPI endpoints for team integration testing
├── notebooks/                # Jupyter notebooks for step-by-step experiments
├── evaluation/               # RAGAS scripts, ablation runners, & test queries
├── corpus_metadata.json      # Corpus version tracking & manifest
├── requirements.txt          # Python dependencies
└── README.md
