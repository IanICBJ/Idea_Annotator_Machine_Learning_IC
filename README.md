# Idea_Annotator_Machine_Learning_IC
Machine learning models for the Idea Annotator system, including BERT and T5 pipelines for automatic case-frame extraction from raw text.
Idea Annotator – Machine Learning (BERT & T5)

Machine learning development for the Idea Annotator FYP.
This module trains and evaluates models (BERT & T5) to automatically extract case-frame slots:

ACTOR

ACTION

OBJECT

LOCATION

TIME

from raw idea descriptions.

This repo contains all notebooks and datasets used across Sprint 3 and Sprint 4, including the fixed dataset split and model improvements.

Tech Stack

Python, Jupyter Notebook

HuggingFace Transformers (BERT, T5)

Pandas

SpaCy (for tokenisation support in Sprint 3)

MongoDB (initial export)

Repository Structure
Idea_Annotator_ML_Development/
│
├── Sprint_3_ML/
│   ├── Jupyter_Notebooks/
│   │    ├── FYP_Sprint_3_BERT.ipynb
│   │    └── FYP_Sprint_3_T5.ipynb
│   │
│   └── Data_Required/
│        ├── train.jsonl
│        ├── val.jsonl
│        └── test.jsonl
│
├── Sprint_4_ML/
│   ├── Jupyter_Notebooks/
│   │    ├── Sprint4_track_0_Fixed_Split.ipynb
│   │    ├── Sprint4_Track1_BERT_Improvements.ipynb
│   │    └── Sprint4_Track2_T5_Improvements.ipynb
│   │
│   └── Data_Required/
│        ├── dataset_full.jsonl
│        └── idea_annotator_sprint4_split_fixed.jsonl
│
└── README.md

Key Concept: Difference Between Sprint 3 and Sprint 4

This is one of the most important sections for your markers.
I will write it very clearly and professionally.

Sprint 3 — Prototype Stage (Clean Data, Small Scale)

Sprint 3 focused on building the first working prototype of the ML pipeline.

Dataset

350 annotated sentences exported from MongoDB

Clean, simple sentences

Data split into:

train.jsonl

val.jsonl

test.jsonl

Goal

Train small BERT and T5 models to see if automatic case-frame extraction is even feasible.

Models

BERT (BIO-tagging → JSON reconstruction)

T5 (text → JSON generation)

Outcome
Model	Slot-F1	Frame Validity
BERT	~0.35	~82%
T5	~0.37	~58%
Summary

Sprint 3 confirmed that:

BERT is more structurally reliable

T5 is more flexible but struggles with JSON formatting

Automatic extraction is possible, but not stable yet

Sprint 4 — Realistic Data + Baseline Improvements

Sprint 4 shifts from “prototype” → real-world performance.

Dataset

Sprint 4 uses raw idea descriptions (messy, long, multi-sentence).

The workflow:

dataset_full.jsonl
Exported from MongoDB (full annotated dataset)

Sprint4_track_0_Fixed_Split.ipynb
Produces the official split:
→ idea_annotator_sprint4_split_fixed.jsonl

This file becomes the gold standard for all Track 1–2–3 improvements.

Track 0 — Baseline

Rebuild BIO tags with final 5-slot schema

Create fixed train/dev/test

Re-train BERT and T5 on raw text

Results:

Model	Slot-F1	Frame Validity
BERT	~0.507	~92%
T5	0.0	0% (invalid JSON)**

T5 fails completely due to raw messy text → motivation for Track 2.

Track 1 — BERT Improvements

Improvements done WITHOUT retraining the model:

BIO tag correction

Span merging

Slot phrase cleaning

Minimal repair heuristics

Result:
Cleaner ACTOR/ACTION/OBJECT extraction even if strict F1 drops.

Track 2 — T5 Improvements

Goal: Fix JSON formatting issues.

Prompt engineering

Constrained decoding

Multi-step JSON repair pipeline

Result:

T5 still weak at slot-filling

But 100% valid JSON

Evaluation becomes possible again

Summary Table: Sprint 3 vs Sprint 4
Category	Sprint 3	Sprint 4
Data	Clean, simple sentences	Raw, messy real descriptions
Purpose	Prototype ML pipeline	Build real, stable baseline
Dataset Source	MongoDB export → cleaned	MongoDB export → raw full → fixed split
BERT Performance	Lower F1, but runs	Much higher validity
T5 Performance	Works somewhat	Completely breaks → then repaired
Outputs Used	train/val/test (old split)	idea_annotator_sprint4_split_fixed.jsonl
Focus	“Can it work?”	“Make it realistic + usable”
How to Run
For Sprint 3:

Open FYP_Sprint_3_BERT.ipynb or FYP_Sprint_3_T5.ipynb

Ensure Sprint 3 data folder is in the same structure as repo

Run all cells

For Sprint 4:

Start with Sprint4_track_0_Fixed_Split.ipynb

Then proceed to:

Sprint4_Track1_BERT_Improvements.ipynb

Sprint4_Track2_T5_Improvements.ipynb

Author

Ian Chia
Nanyang Polytechnic — Diploma in Applied AI & Analytics
Final Year Project — Idea Annotator (ML Module)
