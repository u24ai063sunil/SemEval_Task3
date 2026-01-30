# Dimensional Aspect-Based Sentiment Analysis (DimABSA)

This repository contains my solution for the **Dimensional Aspect-Based Sentiment Analysis (DimABSA)** task, covering **Subtask-1 (DimASR)** and **Subtask-2 (DimASTE)** with full **development and test-phase pipelines**.

The implementation supports **multilingual data**, with a strong focus on **Chinese**, and follows a **precision-first, interpretable approach**.

---

## 📌 Task Overview

### 🔹 Subtask-1: DimASR (Aspect-level VA Regression)
- Input: Text + Aspect
- Output: Valence–Arousal (VA) score in the format `V#A`
- Evaluation metric: **RMSE**

### 🔹 Subtask-2: DimASTE (Aspect–Opinion–VA Triplet Extraction)
- Input: Raw text
- Output: Triplets `{Aspect, Opinion, VA}`
- Evaluation metric: **continuous F1 (cF1)**

---

## 🧠 Approach Summary

### 🔸 Subtask-1 (VA Regression)
- Pretrained model: `hfl/chinese-roberta-wwm-ext`
- Aspect-aware input using special markers:
# Dimensional Aspect-Based Sentiment Analysis (DimABSA)

This repository contains my solution for the **Dimensional Aspect-Based Sentiment Analysis (DimABSA)** task, covering **Subtask-1 (DimASR)** and **Subtask-2 (DimASTE)** with full **development and test-phase pipelines**.

The implementation supports **multilingual data**, with a strong focus on **Chinese**, and follows a **precision-first, interpretable approach**.

---

## 📌 Task Overview

### 🔹 Subtask-1: DimASR (Aspect-level VA Regression)
- Input: Text + Aspect
- Output: Valence–Arousal (VA) score in the format `V#A`
- Evaluation metric: **RMSE**

### 🔹 Subtask-2: DimASTE (Aspect–Opinion–VA Triplet Extraction)
- Input: Raw text
- Output: Triplets `{Aspect, Opinion, VA}`
- Evaluation metric: **continuous F1 (cF1)**

---

## 🧠 Approach Summary

### 🔸 Subtask-1 (VA Regression)
- Pretrained model: `hfl/chinese-roberta-wwm-ext`
- Aspect-aware input using special markers:
- Regression head predicting Valence and Arousal jointly
- Loss: Smooth L1 Loss
- Output VA values clipped to `[1.00, 9.00]` and rounded to 2 decimals

### 🔸 Subtask-2 (Triplet Extraction)
A **two-stage pipeline**:

1. **BIO Tagging (Neural)**
 - Labels: `B-ASP`, `I-ASP`, `B-OPN`, `I-OPN`, `O`
 - Model: Chinese RoBERTa + token-level classifier
 - Class-weighted loss to improve recall

2. **Heuristic Triplet Construction**
 - Linguistic constraints using **Stanza (Chinese POS tagging)**
 - Aspect constraints:
   - Noun / Proper noun / Verb
   - Noun-phrase expansion
 - Opinion constraints:
   - Adjective / Adverb / Verb
   - Single-token adjective relaxation
   - Fallback opinion search in a small context window
 - Conservative pairing to maintain precision

3. **VA Prediction**
 - Reuses the trained Subtask-1 VA regression model
 - Aspect-conditioned VA inference

---

## 🧪 Development vs Test Phase

### ✔ Development Phase
- Gold annotations available
- Used for:
- Training
- Hyperparameter tuning
- Error analysis
- Local evaluation using:
- RMSE (Subtask-1)
- cF1 (Subtask-2)
- **Chinese-specific normalization applied only for local evaluation**

### ✔ Test Phase
- No gold labels available
- Strictly inference-only
- Outputs generated in **Codabench-compliant JSONL format**
- No normalization applied to predictions

---

## 📁 Repository Structure
- Regression head predicting Valence and Arousal jointly
- Loss: Smooth L1 Loss
- Output VA values clipped to `[1.00, 9.00]` and rounded to 2 decimals

### 🔸 Subtask-2 (Triplet Extraction)
A **two-stage pipeline**:

1. **BIO Tagging (Neural)**
 - Labels: `B-ASP`, `I-ASP`, `B-OPN`, `I-OPN`, `O`
 - Model: Chinese RoBERTa + token-level classifier
 - Class-weighted loss to improve recall

2. **Heuristic Triplet Construction**
 - Linguistic constraints using **Stanza (Chinese POS tagging)**
 - Aspect constraints:
   - Noun / Proper noun / Verb
   - Noun-phrase expansion
 - Opinion constraints:
   - Adjective / Adverb / Verb
   - Single-token adjective relaxation
   - Fallback opinion search in a small context window
 - Conservative pairing to maintain precision

3. **VA Prediction**
 - Reuses the trained Subtask-1 VA regression model
 - Aspect-conditioned VA inference

---

## 🧪 Development vs Test Phase

### ✔ Development Phase
- Gold annotations available
- Used for:
- Training
- Hyperparameter tuning
- Error analysis
- Local evaluation using:
- RMSE (Subtask-1)
- cF1 (Subtask-2)
- **Chinese-specific normalization applied only for local evaluation**

### ✔ Test Phase
- No gold labels available
- Strictly inference-only
- Outputs generated in **Codabench-compliant JSONL format**
- No normalization applied to predictions

---

## 📁 Repository Structure

- Regression head predicting Valence and Arousal jointly
- Loss: Smooth L1 Loss
- Output VA values clipped to `[1.00, 9.00]` and rounded to 2 decimals

### 🔸 Subtask-2 (Triplet Extraction)
A **two-stage pipeline**:

1. **BIO Tagging (Neural)**
 - Labels: `B-ASP`, `I-ASP`, `B-OPN`, `I-OPN`, `O`
 - Model: Chinese RoBERTa + token-level classifier
 - Class-weighted loss to improve recall

2. **Heuristic Triplet Construction**
 - Linguistic constraints using **Stanza (Chinese POS tagging)**
 - Aspect constraints:
   - Noun / Proper noun / Verb
   - Noun-phrase expansion
 - Opinion constraints:
   - Adjective / Adverb / Verb
   - Single-token adjective relaxation
   - Fallback opinion search in a small context window
 - Conservative pairing to maintain precision

3. **VA Prediction**
 - Reuses the trained Subtask-1 VA regression model
 - Aspect-conditioned VA inference

---

## 🧪 Development vs Test Phase

### ✔ Development Phase
- Gold annotations available
- Used for:
- Training
- Hyperparameter tuning
- Error analysis
- Local evaluation using:
- RMSE (Subtask-1)
- cF1 (Subtask-2)
- **Chinese-specific normalization applied only for local evaluation**

### ✔ Test Phase
- No gold labels available
- Strictly inference-only
- Outputs generated in **Codabench-compliant JSONL format**
- No normalization applied to predictions

---
