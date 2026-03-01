# Sentiment-Analysis-on-PC-Products-based-on-Amazon-Product-Review
💻 PC Product Sentiment Analyzer

End-to-End Local NLP Pipeline for Business-Ready Insights

Amazon Electronics Reviews | Python | DistilBERT | Mistral 7B | RAG | Fully Local Inference

📌 Project Overview

This project builds a fully local, end-to-end sentiment analysis system for Amazon PC product reviews.

It answers two key business questions:

What is the overall customer attitude toward PC products?

Which specific product aspects drive positive or negative reactions?

The system processes raw review data and produces:

Fine-tuned sentiment classification model

Aspect-level sentiment analysis

Evidence-grounded business insights

Visual dashboard

RAG-styled executive report matching company writing style

⚡ No paid APIs used. All models run locally.

🏗️ Architecture Overview
Raw Amazon Dataset (3.5GB)
        ↓
Data Filtering & Cleaning
        ↓
Balanced Train / Val / Test Split
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

🚀 Pipeline Steps
1️⃣ Data Loading & Filtering

Chunk-based reading of 3.5GB TSV file

Filter for PC category

Early stop at 10,000 records

Handles malformed rows safely

Tools: pandas

2️⃣ Data Preprocessing

HTML cleaning

Combine headline + body

Star rating → sentiment mapping:

1–2 ⭐ → Negative

3 ⭐ → Neutral

4–5 ⭐ → Positive

Class balancing (over/undersampling)

Stratified 70/15/15 split

Tools: pandas, scikit-learn, regex

3️⃣ Overall Sentiment Classification

Fine-tuned DistilBERT (66M parameters) for 3-class classification.

Why DistilBERT?

Smaller and faster than generative LLMs

Ideal for classification

Trainable locally (CPU or Apple Silicon MPS)

Training details:

AdamW optimizer

Linear LR scheduler with warmup

Best checkpoint saved by validation accuracy

Confusion matrix evaluation

Tools:
HuggingFace Transformers, PyTorch, scikit-learn

4️⃣ Aspect-Based Sentiment (Zero-Shot)

Local Mistral 7B (via Ollama) extracts sentiment for 10 predefined PC aspects:

Battery life

Performance

Display

Keyboard/Trackpad

Build quality

Price/Value

Customer service

Software/OS

Portability

Storage

Returns structured JSON:

Mentioned aspects

Sentiment per aspect

Supporting evidence quote

Deterministic generation (temperature = 0.0)
Incremental saving every 50 rows

Tools: Ollama, Mistral 7B, tqdm

5️⃣ Business Insights & Dashboard

Generates:

Overall sentiment distribution

Aspect-level rankings

Key findings

Actionable recommendations

📈 Dashboard (pie chart, bar chart, heatmap)

Two core business sections:

✅ What Customers Love

Extracted positive quotes

Ranked by approval rate

Paired with leverage strategy

⚠️ Targeted Problem Strategy

Extracted negative quotes

Ranked by severity

Paired with concrete actions

All recommendations are traceable to real customer evidence.

6️⃣ RAG-Based Report Styling

Instead of using RAG for content generation, it is used for:

🎯 Writing style retrieval only

Process:

Ingest company PDF/DOCX/TXT reports

Chunk into 500-character overlapping blocks

Embed with all-MiniLM-L6-v2

Store in ChromaDB

Retrieve style examples

Inject style into final sentiment report

This ensures:

Content = driven by data

Tone & structure = aligned with company voice

Tools:
ChromaDB, SentenceTransformers, pypdf, python-docx

🛠️ Tech Stack
Tool	Purpose
pandas	Data processing
scikit-learn	Sampling, splitting, metrics
PyTorch	Model training
HuggingFace	DistilBERT fine-tuning
Ollama	Local LLM server
Mistral 7B	Aspect extraction & report generation
ChromaDB	Vector database
SentenceTransformers	Embeddings
matplotlib / seaborn	Visualizations
tqdm	Batch processing
regex	Cleaning & JSON extraction
🎯 Key Design Decisions
🔹 DistilBERT for Classification, Mistral for Generation

Encoder model for accuracy + generative model for reasoning.

🔹 Full Fine-Tuning (No LoRA)

DistilBERT is small enough for full fine-tuning locally.

🔹 Prompting Over Fine-Tuning for Aspects

No large labeled dataset required.

🔹 Fully Local Inference

No API cost

No data privacy risk

No dependency on external services

🔹 Balanced Reporting

Equal rigor on strengths and weaknesses prevents:

Removing key strengths during product updates

One-sided product decisions

📊 Example Outputs

sentiment_model/ → Fine-tuned model

confusion_matrix.png

aspect_sentiment_results.csv

aspect_summary.csv

business_insights_report.txt

sentiment_dashboard.png

final_business_report.md

💡 Business Value

This system transforms raw customer reviews into:

Evidence-backed marketing messaging

Ranked product improvement roadmap

Severity-prioritized issue detection

Executive-ready reporting

It bridges:

NLP modeling → structured insights → strategic decision support
