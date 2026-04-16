#  Quantifying Dataset Leakage in Fake News Detection

### A Case Study on the ISOT Dataset

---

##  Overview

This project investigates **fake news detection as a binary text classification problem**, using the ISOT Fake News Dataset.

While prior work reports **98–99% accuracy**, this project shows that such performance is **misleading due to dataset leakage and structural biases**, rather than true language understanding.

---

##  Problem Statement

Fake news detection models are often evaluated on benchmark datasets without auditing their structure.

This leads to a critical issue:

> Models may achieve high accuracy by learning **dataset artifacts (shortcuts)** instead of **meaningful linguistic patterns**.

This project answers:

* Are models actually learning *language*?
* Or just exploiting **hidden signals like source names and metadata**?

---

## Key Contributions

* 🔍 **Systematic dataset audit** identifying leakage sources:

  * Subject-based label separation
  * Source fingerprint ("Reuters")
  * Temporal and duplication biases

* 🧪 **Three-track experimental framework**:

  * **Track A:** Raw TF-IDF (leaky baseline)
  * **Track B:** Decontaminated TF-IDF (real performance)
  * **Track C:** Linguistic features only (style-based learning)

* 📊 **Statistical evaluation + hypothesis testing**

* 🧠 **Model interpretability (coefficients + SHAP)**

* ⚠️ Clear distinction between **inflated vs genuine performance**

---

## Dataset

* **ISOT Fake News Dataset**
* 44,898 articles:

  * Fake: 23,481
  * Real: 21,417

### Identified Issues:

* ❌ Subject column perfectly predicts labels
* ❌ "Reuters" appears in ~99% of real articles
* ❌ 6,000+ duplicate entries
* ❌ Temporal inconsistencies

---

## ⚙️ Methodology

### 1. Data Audit (Critical Step)

* Duplicate detection
* Leakage detection
* Temporal bias analysis

---

### 2. Feature Engineering

| Track | Features            | Purpose                    |
| ----- | ------------------- | -------------------------- |
| A     | Raw TF-IDF          | Demonstrate leakage        |
| B     | Clean TF-IDF        | True model performance     |
| C     | Linguistic features | Style-based classification |

---

### 3. Models Used

* Logistic Regression (L1 & L2)
* Naive Bayes (Multinomial & Complement)
* Support Vector Machine (Linear)
* Random Forest
* LightGBM

---

### 4. Evaluation Strategy

* 5-fold Stratified Cross Validation

* Metrics:

  * Accuracy
  * Precision / Recall
  * F1-score (primary)
  * ROC-AUC

* Statistical testing:

  * **McNemar’s Test**
  * **Mann-Whitney U Test**
  * **Kolmogorov-Smirnov Test**

---

## Key Results

| Insight           | Finding                       |
| ----------------- | ----------------------------- |
| Leakage impact    | Minimal drop after removal    |
| True performance  | F1 > 0.98 even after cleaning |
| Best models       | Linear models (LR, SVM)       |
| Style-only models | F1 ≈ 0.88–0.93                |

---

## Key Insights

### 1. Dataset Leakage is Real

* Subject and "Reuters" alone can achieve **~99–100% accuracy**

---

### 2. But Not the Whole Story

* Even after removing leakage:

  * Models still perform **extremely well**

👉 Meaning:

> Fake vs real news differs in **actual language patterns**, not just metadata.

---

### 3. Linear Models > Complex Models

* Logistic Regression and SVM outperform tree-based models
* Indicates **linear separability in TF-IDF space**

---

### 4. Writing Style Matters (But Not Enough)

* Linguistic features capture:

  * Sentiment
  * Readability
  * Vocabulary richness

But:

> Style alone cannot fully classify fake news

---

## 🔍 Interpretability

* **Logistic Regression coefficients** reveal:

  * Real news → formal, structured language
  * Fake news → sensational, informal terms

* **SHAP analysis (Random Forest)**:

  * Sentiment, readability, punctuation influence predictions

---

## Why This Project Matters

Most fake news models:
❌ Report high accuracy
❌ Ignore dataset flaws

This project shows:

> High accuracy ≠ real intelligence

and highlights the need for:

* Dataset auditing
* Controlled experiments
* Careful evaluation

---

## 🛠️ Tools & Technologies

* Python (Pandas, NumPy, Scikit-learn)
* NLP (TF-IDF, VADER, readability metrics)
* LightGBM
* Matplotlib / Seaborn
* SHAP (interpretability)
* Overleaf (report writing)
* Generative AI (code + grammar assistance)

---

## 🚀 How to Run

1. Clone the repository
2. Install dependencies
3. Run the notebook:

```bash
pip install -r requirements.txt
jupyter notebook
```

---

## 📌 Future Work

* Extend to multi-domain datasets
* Include social media and multimodal data
* Build leakage-resistant benchmarks
* Explore deep learning models (BERT, LLMs)

---

## 👨‍💻 Authors

* Raj Purohith Arjun
* Venkateswarlu Nagineni
* Hareen Sai Vattikuti

---

