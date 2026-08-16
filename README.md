# DTA_THESIS

A research project comparing large language models (LLMs) and fine-tuned transformer models for multi-label document classification on two benchmark datasets: **SCOTBESS** (environmental impact assessments) and **AAPD** (arXiv papers).

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

## Project Overview

This thesis compares different approaches to multi-label document classification:

### Datasets
- **SCOTBESS**: Environmental impact assessment documents
- **AAPD**: arXiv papers with academic subject labels

### Modeling Approaches

#### 1. **Full Fine-Tuning (FFT)**
- Traditional end-to-end training of transformer models
- Models: DistilBERT, ModernBERT
- `experiments/[dataset]/FFT/`

#### 2. **Parameter-Efficient Fine-Tuning (PEFT)**
- Adapter-based methods (Houlsby adapters)
- LoRA (Low-Rank Adaptation)
- `experiments/[dataset]/PEFT/`

#### 3. **Large Language Models (LLMs)**
- Ollama-based inference with open-source models
- Models tested: QWEN, LLAMA
- In-context learning with label definitions
- Greedy and Top-K retrieval strategies
- `experiments/[dataset]/LLMs/`

### Key Notebooks

**Data Preparation:**
- `BERTopic_topic_exploration.ipynb` - Topic modeling and exploration
- `SCOTBESS_ANNOTATION_MODEL_EXPLORATION.ipynb` - Annotation workflow with LLM validation
- `SCOTBESS_embeddings_topk.ipynb` - Embedding generation for retrieval-augmented approaches

**Experiments (Dataset-specific):**
- `*_DistilBERT.ipynb` - Full fine-tuning with DistilBERT
- `*_DistilBERT_LoRa.ipynb` - LoRA fine-tuning
- `*_DistilBERT_Houlsby.ipynb` - Adapter-based fine-tuning
- `*_ModernBERT.ipynb` - Modern transformer architecture
- `*_Ollama.ipynb` - LLM experiments (QWEN, LLAMA)
- `*_LC_visualisation.ipynb` - Learning curve visualizations

## Workflow

1. **Preparation Phase** (`data_preparation/`)
   - Dataset loading and preprocessing
   - Topic exploration and analysis
   - Label definition and annotation validation
   - Embedding generation for retrieval approaches

2. **Experimentation Phase** (`experiments/`)
   - Fine-tuned models (FFT, PEFT) trained on each dataset
   - LLM inference with various prompting strategies
   - Learning curve analysis
   - Results collection and evaluation

3. **Evaluation**
   - Metrics: F1-score, precision, recall, classification reports
   - Comparison across approaches per dataset
   - Learning curve analysis for sample efficiency

## Technology Stack

- **Language**: Python (Jupyter Notebooks)
- **Deep Learning**: `transformers`, `torch`, `datasets`
- **Parameter Efficiency**: `peft` (adapters, LoRA)
- **LLM Inference**: `Ollama` with open-source models
- **Topic Modeling**: `BERTopic`
- **Evaluation**: `sklearn.metrics`
- **Data Processing**: `pandas`, `numpy`
- **Storage**: Google Drive integration (via Colab)

## Key Libraries & Frameworks

- `transformers` - HuggingFace models and training
- `peft` - Parameter-Efficient Fine-Tuning techniques
- `datasets` - Dataset loading and processing
- `torch` - PyTorch backend
- `sklearn` - Metrics and evaluation
- `bertopic` - Topic modeling
- `ollama` - Local LLM inference
- `google-colab` - Cloud environment integration

## Running Experiments

Most notebooks are designed to run on Google Colab and include:

1. **Google Drive mounting** for data and results storage
2. **GPU/TPU** resource configuration
3. **Environment setup** (library installations, API keys)
4. **Hyperparameter definitions** at the top of each notebook
5. **Results export** to Google Drive

### General Setup
```python
# Common setup in all notebooks
from google.colab import drive
drive.mount('/content/drive')

# Load data
SPLIT_PATH = "/content/drive/MyDrive/thesis_results/..."
output_dir = "/content/drive/MyDrive/thesis_results/..."
```

## Notes

- All experiments are documented in individual Jupyter Notebooks
- Results are stored in Google Drive with organized directory structure
- Learning curves and visualizations are generated for model comparison
- Multi-label classification with scikit-learn's MultiLabelBinarizer
- Random seeds fixed for reproducibility (SEED = 42)

## Project Scope

This thesis systematically evaluates:
- **Fine-tuning efficiency**: FFT vs PEFT approaches
- **Model scalability**: Parameter count vs performance
- **LLM capabilities**: Prompt engineering and in-context learning
- **Dataset characteristics**: Domain-specific (environmental) vs general-purpose (academic)
- **Sample efficiency**: Learning curves across different training set sizes

---

**Status**: Active Research  
**Created**: August 2026  
**Author**: wgrl00
