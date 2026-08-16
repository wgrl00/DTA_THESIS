# Master's Thesis

This repository contains the data-preparation workflows, experiments, and results associated with my master's thesis, **_Exploring parameter-efficient fine-tuning techniques for multi-label topic classification in energy infrastructure consultation responses_**.

The study compares classical machine learning, prompt-based large language models, full fine-tuning (FFT), and parameter-efficient fine-tuning (PEFT) for multi-label topic classification on two datasets:

- **AAPD** — a benchmark multi-label dataset of scientific paper abstracts.
- **Scot-BESS** — a dataset developed for this thesis from written responses concerning battery energy storage system (BESS) planning applications in Scotland.

## Methods

The experimental comparison includes:

- TF-IDF with LinearSVC
- Retrieval-augmented in-context classification with Llama and Qwen
- Full fine-tuning of DistilBERT and ModernBERT
- Parameter-efficient fine-tuning:
  - LoRA
  - Houlsby adapters
  - Pfeiffer adapters
  - BitFit
- Learning-curve experiments comparing selected FFT and PEFT approaches at different training-set sizes

## Repository structure

```text
DTA_THESIS/
├── README.md
│
├── data/
│   ├── aapd/
│   │   ├── aapd.zip
│   │   ├── mlb.joblib
│   │   ├── label_descriptions/
│   │   │   ├── aapd_label_descriptions_prompt_friendly.json
│   │   │   ├── acm.txt
│   │   │   ├── arxiv_label_descriptions.xlsx
│   │   │   └── arxiv_label_descriptions_expanded.json
│   │   └── retrieval/
│   │       ├── aapd_test_gold_labels.json
│   │       ├── aapd_test_top_k_llm_input_data.jsonl
│   │       ├── aapd_validation_gold_labels.json
│   │       ├── aapd_validation_greedy_llm_input_data.jsonl
│   │       └── aapd_validation_top_k_llm_input_data.jsonl
│   │
│   └── scotbess/
│       ├── SCOTBESS_DATASET.csv
│       ├── SCOTBESS_labels_definitions.xlsx
│       ├── scotbess_mlb.joblib
│       └── retrieval/
│           ├── scotbess_test_gold_labels.json
│           ├── scotbess_test_top_k_llm_input_data.jsonl
│           ├── scotbess_validation_gold_labels.json
│           └── scotbess_validation_top_k_llm_input_data.jsonl
│
├── data_preparation/
│   ├── aapd/
│   │   ├── AAPD_label_descriptions.ipynb
│   │   └── AAPD_retrieval_embeddings.ipynb
│   │
│   └── scotbess/
│       ├── 01_collection/
│       ├── 02_extraction/
│       ├── 03_text_cleaning/
│       ├── 04_deduplication/
│       ├── 05_masking/
│       ├── 06_topic_exploration/
│       ├── 07_annotation/
│       │   └── results/
│       ├── 08_data_splitting/
│       └── SCOTBESS_embeddings_topk.ipynb
│
└── experiments/
    ├── aapd/
    │   ├── SVC/
    │   │
    │   ├── LLMs/
    │   │   ├── LLAMA/
    │   │   ├── QWEN/
    │   │   └── retrieval_size_selection/
    │   │
    │   ├── FFT/
    │   │   ├── DistilBERT/
    │   │   └── ModernBERT/
    │   │
    │   ├── PEFT/
    │   │   ├── BitFit/
    │   │   │   └── DistilBERT/
    │   │   ├── LoRA/
    │   │   │   ├── DistilBERT/
    │   │   │   └── ModernBERT/
    │   │   └── adapters/
    │   │       ├── Houlsby/
    │   │       │   ├── DistilBERT/
    │   │       │   └── ModernBERT/
    │   │       └── Pfeiffer/
    │   │           ├── DistilBERT/
    │   │           └── ModernBERT/
    │   │
    │   └── learning_curve/
    │
    └── scotbess/
        ├── SVC/
        │
        ├── LLMs/
        │   ├── LLAMA/
        │   └── QWEN/
        │
        ├── FFT/
        │   ├── DistilBERT/
        │   └── ModernBERT/
        │
        ├── PEFT/
        │   ├── BitFit/
        │   │   └── DistilBERT/
        │   ├── LoRA/
        │   │   ├── DistilBERT/
        │   │   └── ModernBERT/
        │   └── adapters/
        │       ├── Houlsby/
        │       │   ├── DistilBERT/
        │       │   └── ModernBERT/
        │       └── Pfeiffer/
        │           ├── DistilBERT/
        │           └── ModernBERT/
        │
        └── learning_curve/
```

## Data

### AAPD

The repository contains the AAPD data used in the experiments together with its fitted `MultiLabelBinarizer`, label-description resources, and fixed retrieval inputs used for the prompt-based LLM experiments.

The label descriptions were prepared from the source taxonomy and converted into a prompt-friendly format in `data_preparation/aapd/AAPD_label_descriptions.ipynb`.

### Scot-BESS

Scot-BESS was developed specifically for this study from written responses associated with Scottish BESS planning applications.

The final experiment-ready dataset contains the processed and masked response text, multi-label annotations, and the predefined dataset split.


**Privacy note.** The experiments were run on an internal version of Scot-BESS containing additional collection metadata, namely project identifiers. This metadata was not used as an input to the models and has been removed from the publicly released dataset to reduce the risk of identifying the source planning applications.

Raw unmasked consultation material and intermediate dataset versions are not distributed in this repository.

## Scot-BESS data preparation

The Scot-BESS construction workflow is documented under `data_preparation/scotbess/`.

### 01 — Collection

Consultation responses were collected from the Scottish Energy Consents Unit and local planning authority portals using dedicated scraping workflows.

### 02 — Extraction

Relevant response text was extracted from the collected material using rule-based processing and LLM-assisted extraction depending on the source format.

### 03 — Text cleaning

Residual boilerplate and non-response text were removed and document-length checks were applied.

### 04 — Deduplication

Near-duplicate responses were removed in two stages:

1. lexical similarity using TF-IDF and cosine similarity;
2. semantic similarity using sentence embeddings and clique-based grouping.

### 05 — Masking

Potentially identifying information was detected and masked using an LLM-assisted procedure supplemented with rule-based processing. The masking output was subsequently reviewed and finalized.

### 06 — Topic exploration

BERTopic was used as an exploratory aid during development of the Scot-BESS topic inventory. The resulting topics were reviewed manually rather than being converted automatically into the final label set.

### 07 — Annotation

A manually labelled pilot sample was used to compare candidate LLM annotation configurations.

The selected annotation configuration was then applied to the complete Scot-BESS dataset. The folder also contains annotation-quality-control outputs, model-comparison results, stability checks, and disagreement analysis.

### 08 — Data splitting

The annotated dataset was divided into training, validation, and test subsets for the downstream classification experiments.

## Retrieval-based LLM classification

The LLM baseline uses semantically retrieved training examples as in-context demonstrations.

BGE-M3 embeddings are used for retrieval. Fixed retrieval inputs are stored under the corresponding `data/<dataset>/retrieval/` directories so that the exact demonstrations supplied to the LLMs can be reproduced without storing the full embedding matrices.

On AAPD, validation experiments were used to compare retrieval strategies and the number of retrieved examples. The selected retrieval configuration was subsequently used for test evaluation and transferred to Scot-BESS.

The evaluated local instruction-tuned models are organized under:

```text
experiments/<dataset>/LLMs/
├── LLAMA/
└── QWEN/
```

## Full fine-tuning

FFT experiments are provided for:

```text
FFT/
├── DistilBERT/
└── ModernBERT/
```

Where applicable, experiment folders contain:

- the experimental notebook;
- hyperparameter search results;
- the selected configuration;
- per-seed test results;
- aggregated test-result summaries.

## Parameter-efficient fine-tuning

The PEFT experiments are organized by method:

```text
PEFT/
├── LoRA/
├── BitFit/
└── adapters/
    ├── Houlsby/
    └── Pfeiffer/
```

LoRA and adapter experiments are evaluated with DistilBERT and ModernBERT backbones. BitFit experiments use DistilBERT.

The same general experimental methodology is used for FFT and PEFT to support direct comparison of predictive performance and computational efficiency.

## Learning curves

Learning-curve experiments examine how the relative performance of FFT and selected PEFT approaches changes as the amount of available training data increases.

The AAPD experiments compare DistilBERT FFT with Pfeiffer adapters, while the Scot-BESS experiments compare ModernBERT FFT with Houlsby adapters.

Each learning-curve folder contains the experimental notebooks together with per-run and aggregated results.

## Results

Model-specific results are stored alongside the corresponding experimental notebooks.

For fine-tuning experiments, the principal result files are typically:

```text
search_results.csv
best_config.json
*_test_results.csv
*_test_results_summary.csv
```

The reported evaluation includes predictive-performance metrics such as Micro-F1 and Macro-F1 together with computational measures used to compare the efficiency of the different fine-tuning approaches.
