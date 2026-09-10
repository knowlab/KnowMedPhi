# KnowMedPhi

**Expert knowledge-centred pre-training for transferable clinical language modelling**

[Model on Hugging Face](https://huggingface.co/knowlab-research/KnowMedPhi3.5-mini) · [KnowMed-PT](https://huggingface.co/datasets/knowlab-research/KnowMed-PT) · [KnowMed-IT](https://huggingface.co/datasets/knowlab-research/KnowMed-IT)

## Overview

KnowMedPhi is a family of medical language models developed using continued pre-training on a compact corpus centred on explicitly encoded biomedical and clinical knowledge, followed by medical instruction tuning.

This repository accompanies the manuscript:

> **KnowMedPhi: Expert knowledge-centred pre-training for transferable clinical language modelling**

The study investigates whether a substantially smaller, deliberately constructed biomedical and clinical knowledge corpus can provide a stronger and more transferable training signal than conventional continued pre-training on biomedical literature.

The repository provides:

- links to the released KnowMedPhi model;
- resources and documentation for the KnowMed-PT continued pre-training corpus;
- resources and documentation for the KnowMed-IT instruction-tuning corpus; and
- links to the public benchmark datasets used for evaluation.

---

## Model

The principal model presented in the study is available through Hugging Face:

### KnowMedPhi3.5-mini

**Hugging Face:**  
https://huggingface.co/knowlab-research/KnowMedPhi3.5-mini

KnowMedPhi3.5-mini is based on Phi-3.5-mini and was adapted using KnowMed-PT continued pre-training followed by KnowMed-IT medical instruction tuning.

Additional model checkpoints used in the study may be released separately.

---

## Training data

### KnowMed-PT

KnowMed-PT is the expert knowledge-centred corpus used for continued pre-training. It contains approximately **126 million tokens** assembled from biomedical and clinical knowledge resources.

| Source | Approx. tokens |
|---|---:|
| AGCT / SNOMED CT-derived data | 33.4M |
| PMC-Patients | 8.1M |
| Medical Wikipedia data | 15.9M |
| DrugBank | 4.5M |
| PathBank | 62.3M |
| MONDO | 1.2M |
| Human Phenotype Ontology (HPO) | 0.8M |
| **Total** | **126.2M** |

**KnowMed-PT:** [Dataset](https://huggingface.co/datasets/knowlab-research/KnowMed-PT)

The constituent resources remain subject to their respective licences and terms of use. Where redistribution of source-derived content is restricted, users should obtain the corresponding resource from its original provider and comply with the applicable licence.

Detailed source provenance and access information are provided in the accompanying dataset documentation.

---

### KnowMed-IT

KnowMed-IT is the medical instruction-tuning corpus used following continued pre-training. It contains **365,547 instruction examples** assembled from multiple medical instruction, question-answering, and educational resources.

| Source | Examples |
|---|---:|
| Asclepius | 158,114 |
| AlpaCare / MedInstruct | 52,002 |
| Medical-QA | 41,992 |
| MedMCQA rationales | 36,316 |
| NHS QA / OpenGPT | 29,354 |
| MedlinePlus-derived instructions | 20,891 |
| MedQuAD | 16,407 |
| MedQA rationales | 9,816 |
| NEJM-AI-Exams | 655 |
| **Total** | **365,547** |

**KnowMed-IT:** [Dataset](https://huggingface.co/datasets/knowlab-research/KnowMed-IT)

The MedlinePlus-derived instruction data were constructed as part of this work. Other constituent datasets remain subject to the licences and terms of their original sources.

Where required, only the designated training splits of benchmark-derived datasets were used for instruction tuning.

---

## Evaluation datasets

KnowMedPhi was evaluated on a collection of publicly available and controlled-access biomedical and clinical NLP benchmarks.

The evaluation datasets are **not redistributed through this repository**. Users should obtain them from the corresponding original or project-maintained sources and comply with their respective licences, access requirements, and terms of use.

### Medical question answering

| Dataset | Task | Source |
|---|---|---|
| MMLU medical subsets | Multiple-choice medical QA | [MMLU](https://huggingface.co/datasets/cais/mmlu) |
| MedQA | Multiple-choice medical QA | [MedQA](https://github.com/jind11/MedQA) |
| MedMCQA | Multiple-choice medical QA | [MedMCQA](https://github.com/medmcqa/medmcqa) |
| MedXpertQA | Medical QA | [MedXpertQA](https://huggingface.co/datasets/TsinghuaC3I/MedXpertQA) |
| MedExQA | Medical QA with explanations | [MedExQA](https://huggingface.co/datasets/bluesky333/MedExQA) |

### Biomedical named entity recognition

| Dataset | Target |
|---|---|
| BC2GM | Genes and proteins |
| BC5CDR-Chemical | Chemicals |
| BC5CDR-Disease | Diseases |
| NCBI Disease | Diseases |

Source links:

- **BC2GM:** [BigBio / BLURB](https://huggingface.co/datasets/bigbio/blurb)
- **BC5CDR:** [BigBio BC5CDR](https://huggingface.co/datasets/bigbio/bc5cdr)
- **NCBI Disease:** [NCBI Disease Corpus](https://www.ncbi.nlm.nih.gov/research/bionlp/Data/disease/)

### Additional biomedical and clinical NLP benchmarks

| Dataset | Evaluation capability | Source |
|---|---|---|
| LitCovid | Document classification | [LitCovid](https://www.ncbi.nlm.nih.gov/research/coronavirus/) |
| MedNLI | Clinical natural language inference | [MedNLI](https://physionet.org/content/mednli/1.0.0/) |
| BioASQ | Biomedical question answering | [BioASQ](https://participants-area.bioasq.org/datasets/) |
| BioHop-R | Biomedical multi-hop reasoning | [BioHop-R](https://huggingface.co/datasets/knowlab-research/BioHopR) |
| MedS-Bench | Medical language-model evaluation | [MedS-Bench](https://huggingface.co/datasets/Henrychur/MedS-Bench) |

MedNLI is distributed through PhysioNet and is subject to its corresponding access requirements and data-use conditions.

For the exact dataset subsets, evaluation settings, prompts, and metrics used in the study, please refer to the Methods section of the manuscript.

---

## Training

KnowMedPhi was trained using:

- [LLaMAFactory](https://github.com/hiyouga/LLaMA-Factory)
- [DeepSpeed](https://github.com/microsoft/DeepSpeed)

Training configurations used in the study are provided in:

```text
configs/
├── cpt/
├── instruction_tuning/
└── deepspeed/
