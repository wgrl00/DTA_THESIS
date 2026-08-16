# Exploring Parameter-Efficient Fine-Tuning Techniques for Multi-Label Topic Classification

This repository contains the code, data-preparation workflows, experiments, and results associated with my master's thesis, Exploring Parameter-Efficient Fine-Tuning Techniques for Multi-Label Topic Classification.


The project compares several approaches to multi-label topic classification on two datasets:

AAPD — a benchmark dataset of scientific paper abstracts with multiple subject labels.

Scot-BESS — a dataset developed for this thesis from Scottish planning consultation responses concerning battery energy storage system (BESS) developments.


## Repository Structure

```
DTA_THESIS/
├── README.md                               # This file
│
├── data_preparation/                       # Data preprocessing and preparation workflows
│   ├── scotbess/                           # SCOTBESS dataset preparation
│   │   ├── 06_topic_exploration/
│   │   │   └── BERTopic_topic_exploration.ipynb
│   │   └── 07_annotation/
│   │       └── SCOTBESS_ANNOTATION_MODEL_EXPLORATION.ipynb
│   ├── aapd/                               # AAPD dataset preparation
│   └── SCOTBESS_embeddings_topk.ipynb      # Embedding generation and retrieval
│
└── experiments/                            # Model experiments and comparisons
    ├── scotbess/                           # SCOTBESS experiments
    │   ├── FFT/                            # Full Fine-Tuning experiments
    │   │   └── ModernBERT/
    │   │       └── SCOTBESS_ModernBERT.ipynb
    │   ├── PEFT/                           # Parameter-Efficient Fine-Tuning
    │   │   └── adapters/
    │   │       └── Houlsby/
    │   │           └── DistilBERT/
    │   │               └── SCOTBESS_DistilBERT_Houlsby.ipynb
    │   ├── LLMs/                           # Large Language Model experiments
    │   │   └── QWEN/
    │   │       └── SCOTBESS_QWEN_Ollama.ipynb
    │   ├── learning_curve/
    │   │   └── SCOTBESS_LC_visualisation.ipynb
    │   └── embeddings/                     # Embedding-based approaches
    │
    └── aapd/                               # AAPD experiments
        ├── FFT/                            # Full Fine-Tuning experiments
        │   └── DistilBERT/
        │       └── AAPD_DistilBERT.ipynb
        ├── PEFT/                           # Parameter-Efficient Fine-Tuning
        │   └── LoRA/
        │       └── DistilBERT/
        │           └── AAPD_DistilBERT_LoRa.ipynb
        ├── LLMs/                           # Large Language Model experiments
        │   ├── LLAMA/
        │   │   └── AAPD_LLAMA_Ollama.ipynb
        │   └── QWEN/
        │       └── AAPD_QWEN_Ollama.ipynb
        └── learning_curve/
            └── SCOTBESS_LC_visualisation.ipynb
```

