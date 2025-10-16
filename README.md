# DSA4213 Assignment 3

| Label | Description |
|:------|:------------|
| `normal` | Non-offensive, neutral content |
| `offensive` | Mild or indirect offensive remarks |
| `hatespeech` | Explicit hate or abuse toward identity groups |

# Dataset: HateXplain
**Source:** [HateXplain] (https://github.com/hate-alert/HateXplain) 

## Experimental Setup
All experiments were performed in **Google Colab (GPU runtime)** using the Hugging Face Transformers library.

### 1. Models
| Family | Fine-Tuning Method |
|:--------|:------------------|
| BERT-base | Full fine-tuning |
| BERT-base | Parameter-efficient fine-tuning (LoRA) |
| RoBERTa-base | Full fine-tuning |
| RoBERTa-base | Parameter-efficient fine-tuning (LoRA) |

### 2. Training Details
| Parameter | Value |
|:-----------|:------|
| Learning rate | 2e-5 (Full FT) / 1e-4 (LoRA) |
| Batch size | 16 (train) / 32 (eval) |
| Epochs | 3 |
| Max sequence length | 256 |
| Early stopping patience | 2 |

---

## Results
| Model | Val Accuracy | Val Macro F1 | Val Loss | Test Accuracy | Test Macro F1 | Test Loss |
|:------|-------------:|-------------:|---------:|--------------:|--------------:|----------:|
| **BERT-base (Full FT)** | 0.7019 | 0.6906 | 0.7586 | 0.6897 | 0.6729 | 0.7821 |
| **BERT-base (LoRA)** | 0.6920 | 0.6779 | 0.7247 | 0.6866 | 0.6689 | 0.7155 |
| **RoBERTa-base (Full FT)** | **0.6946** | **0.6842** | **0.7254** | **0.7053** | **0.6923** | **0.7166** |
| **RoBERTa-base (LoRA)** | 0.6967 | 0.6798 | 0.7234 | 0.6991 | 0.6821 | 0.7228 |

**Best Performing Model:** RoBERTa-base (Full Fine-Tuning)

---

## Analysis 
* **Confusion Matrix:** RoBERTa (Full Fine-Tuning) has a more balanced performance 
* **Qualitative Error Analysis:** Some misclassified examples contain sarcasm or implicit slurs showing  model limitations in contextual understanding.
* **Ethical Reflection:**
    * Dataset text includes sensitive slurs, models may reproduce biased behaviour if applied carelessly
    * Labeling bias exists

---

## Reproduction Instructions
### 1. Clone Repository
```
git clone https://github.com/ruientan/DSA4213-Assignment3.git
cd DSA4213-Assignment3
```

### 2. Create Environment
```
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

### 3. Download Dataset
Download both `dataset.json` and `post_id_divisions.json` and place them inside the project directory.

---

## Repository Structure
```
DSA4213-Assignment3/
│
├── RaineTan_Assignment3.ipynb     # Main Colab notebook (code only)
├── requirements.txt               # Dependencies
├── README.md                      # Project overview and usage
├── dataset.json                   # HateXplain dataset 
└── post_id_divisions.json
```

---
