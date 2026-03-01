# Sentiment-Analysis-on-PC-Products-based-on-Amazon-Product-Review

**End-to-End Local NLP Pipeline for Business-Ready Insights**

> Amazon Electronics Reviews | Python | DistilBERT | Mistral 7B | RAG | Fully Local Inference

---

## 📌 Project Overview

This project builds a fully local, end-to-end sentiment analysis system for Amazon PC product reviews.

It answers two key business questions:

1. What is the overall customer attitude toward PC products?
2. Which specific product aspects drive positive or negative reactions?

The system produces:
- Fine-tuned sentiment classification model
- Aspect-level sentiment analysis
- Evidence-grounded business insights
- Visual dashboard
- RAG-styled executive report

All models run locally. No paid APIs are used.

---

## 🏗️ Architecture Overview

Raw Amazon Dataset (3.5GB)  
↓  
Data Filtering & Cleaning  
↓  
Balanced Train / Validation / Test Split  
↓  
DistilBERT Fine-Tuning (3-Class Sentiment)  
↓  
Aspect-Based Sentiment (Mistral 7B via Ollama)  
↓  
Aggregation & Visualization  
↓  
Business Report Generation  
↓  
RAG Style Injection via ChromaDB  

---

## 🚀 Pipeline Steps

### 1) Data Loading & Filtering
- Chunk-based reading of 3.5GB Amazon Customer Review TSV file (date source: https://www.kaggle.com/datasets/cynthiarempel/amazon-us-customer-reviews-dataset?select=amazon_reviews_us_PC_v1_00.tsv)
- Filter for PC category
- Early stop at 10,000 records
- Skip malformed rows

Tools: pandas

---

### 2) Data Preprocessing
- HTML cleaning
- Combine headline + body into full_text
- Star rating mapping:
  - 1–2 stars → Negative
  - 3 stars → Neutral
  - 4–5 stars → Positive
- Class balancing (over/undersampling)
- Stratified 70/15/15 split

Tools: pandas, scikit-learn, regex

---

### 3) Overall Sentiment Classification

Fine-tuned DistilBERT (distilbert-base-uncased) for 3-class classification.

Training details:
- AdamW optimizer
- Linear learning rate scheduler with warmup
- Best checkpoint saved by validation accuracy
- Confusion matrix evaluation

Tools: transformers, PyTorch, scikit-learn

---

### 4) Aspect-Based Sentiment (Zero-Shot)

Local Mistral 7B (via Ollama) extracts sentiment for 10 predefined PC aspects:

- Battery life
- Performance
- Display
- Keyboard
- Build quality
- Price
- Customer service
- Software
- Portability
- Storage

Returns structured JSON:
- Mentioned aspects
- Sentiment per aspect
- Supporting evidence quote

Temperature set to 0.0 for deterministic output.  
Results saved incrementally.

Tools: Ollama, Mistral 7B, pandas, tqdm

---

### 5) Business Insights & Dashboard

Generates:
- Overall sentiment distribution
- Aspect-level rankings
- Key findings
- Recommendations
- What Customers Love section
- Targeted Problem Strategy section

Charts:
- Pie chart
- Bar chart
- Heatmap

Outputs:
- business_insights_report.txt
- sentiment_dashboard.png

Tools: matplotlib, seaborn, pandas

---

### 6) RAG-Based Style Matching

RAG is used for writing style retrieval, not content generation.

6a) Ingestion:
- Extract text from PDF/DOCX/TXT
- 500-character chunking with overlap
- Sentence-transformer embeddings
- Store in ChromaDB
- Duplicate detection

6b) Report Generation:
- Retrieve style examples
- Combine with sentiment evidence
- Generate balanced report
- Output TXT and Markdown versions

Tools: ChromaDB, SentenceTransformers, Ollama, Mistral 7B

---


## 📁 Suggested Repository Structure

Sentiment-Analysis-on-PC-Products-based-on-Amazon-Product-Review/
│
├── Code/
│   ├── load_and_filter.py
│   ├── preprocessing.py
│   ├── overall_sentiment.py
│   ├── aspect_sentiment.py
│   ├── report.py
│   ├── ingest_template.py
│   ├── generate_report.py
│   └── requirements.txt
│
└── README.md

---

## 🛠️ Tech Stack

- pandas
- scikit-learn
- PyTorch
- HuggingFace Transformers
- Ollama
- Mistral 7B
- ChromaDB
- SentenceTransformers
- matplotlib
- seaborn
- tqdm
- regex

---

## 🎯 Key Design Decisions

- DistilBERT for classification, Mistral for generation
- Full fine-tuning (no LoRA needed)
- Prompting instead of fine-tuning for aspect extraction
- Fully local inference
- Balanced reporting grounded in real quotes

---

## 💡 Business Value

Transforms raw customer reviews into:

- Evidence-backed marketing insights
- Ranked improvement roadmap
- Executive-ready report
- Privacy-preserving local NLP pipeline

