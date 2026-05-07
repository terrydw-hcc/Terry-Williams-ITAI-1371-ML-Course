# Terry Williams — ITAI 1371 Machine Learning Portfolio

A semester-long collection of labs, projects, and reflections from **ITAI 1371: Introduction to Machine Learning**, taught by Dr. Sina Nazifi as part of the Houston Community College *Artificial Intelligence & Robotics, B.A.T.* program (Spring 2026).

---

## About Me

I'm Terry Williams, a student in the AI & Robotics program at Houston Community College with a background in full-stack web development. My day-to-day work is in PHP, MySQL, and the kind of pragmatic system design that comes from building real applications — most recently an event management platform with admin tooling, reporting, and email systems. ITAI 1371 is where I started moving from "writing software that processes data" to "writing software that learns from data." The two mindsets are surprisingly different, and this portfolio is a record of that transition.

What drew me to machine learning specifically was the same thing that drew me to engineering generally: the satisfaction of building systems that actually work in the messy real world. The labs in this course pushed me from "I can call `model.fit()`" toward "I understand why a 99% accuracy score can be a red flag, why a single train/test split lies to you, and why the most important question in a fairness audit is *which mistake is more expensive?*" That shift in framing is what I'm proudest of from this course.

---

## Course Summary

Across 14 modules (Spring 2026), this course covered the full machine learning workflow from data preparation through ethical deployment:

| Module | Topic | Notebook |
|---|---|---|
| 02 | Machine Learning Tools | [L02_TerryWilliams_ITAI1371.ipynb](./L02_TerryWilliams_ITAI1371.ipynb) |
| 03 | ML Workflow & Types of Learning | [L03_TerryWilliams_ITAI1371.ipynb](./L03_TerryWilliams_ITAI1371.ipynb) |
| 04 | Working with Data & EDA | [L04_TerryWilliams_ITAI1371.ipynb](./L04_TerryWilliams_ITAI1371.ipynb) |
| 05 | Data Preparation & Feature Engineering | [L05_TerryWilliams_ITAI1371.ipynb](./L05_TerryWilliams_ITAI1371.ipynb) |
| 06 | Regression & Classification | [L06_TerryWilliams_ITAI1371.ipynb](./L06_TerryWilliams_ITAI1371.ipynb) |
| 07 | Evaluating Machine Learning Models | [L07_TerryWilliams_ITAI1371.ipynb](./L07_TerryWilliams_ITAI1371.ipynb) |
| 08 | Overfitting, Underfitting, Regularization | [L08_TerryWilliams_ITAI1371.ipynb](./L08_TerryWilliams_ITAI1371.ipynb) |
| 09 | Ensemble Methods | [L09_TerryWilliams_ITAI1371.ipynb](./L09_TerryWilliams_ITAI1371.ipynb) |
| 10 | Unsupervised Learning | [L10_TerryWilliams_ITAI1371.ipynb](./L10_TerryWilliams_ITAI1371.ipynb) |
| 11 | Hyperparameter Tuning & AutoML | [L11_TerryWilliams_ITAI1371.ipynb](./L11_TerryWilliams_ITAI1371.ipynb) |
| 12 | Ethics, Fairness, and Bias | [L12_TerryWilliams_ITAI1371.ipynb](./L12_TerryWilliams_ITAI1371.ipynb) |

---

## Major Projects

### 🏈 Midterm Project — Predicting Weekly Fantasy Football Player Performance
📁 [MidTerm_TerryWilliams_ITAI1371.ipynb](./MidTerm_TerryWilliams_ITAI1371.ipynb)

A regression project predicting **weekly fantasy football points** for NFL players using 2024 weekly performance data combined with 2023 season-summary statistics.

**Approach:** Engineered weekly **lag features** (previous-week points, lag-2 points, rolling averages) and merged in prior-season summary stats. Trained and compared three models:

| Model | RMSE | MAE | R² |
|---|---|---|---|
| **Random Forest** | **6.48** | 4.80 | **0.388** |
| Gradient Boosting | 6.50 | 4.78 | 0.385 |
| Linear Regression | 6.66 | 4.86 | 0.354 |

**Key takeaways:**
- Recent player performance dominates — lag features (previous-week points, season-to-date) were the most important predictors.
- Prior-season context still added meaningful signal.
- The two ensemble models tied each other within noise but both clearly beat Linear Regression, which lines up with what Module 09 taught about ensembles reducing variance on noisy real-world data.

---

### ⛳ Final Project — Golf Swing Quality Classification Using IMU Sensor Data
📁 [Final_TerryWilliams_ITAI1371.ipynb](./Final_TerryWilliams_ITAI1371.ipynb)

A multi-class classification project for the **FTY swing-quality classifier**, designed to score youth golf swings in real time from IMU sensor data. Predicts one of three categories: **Good**, **Needs Work**, or **Poor**.

**Approach:** Generated a synthetic dataset of 2,000 swings using the FTY firmware spec (FTY-ARCH-001 §4.2) labeling rules, with 12% inter-rater label noise added to simulate the kind of disagreement real coaching rubrics produce near class boundaries. Engineered 12 swing features per shot and trained six classifiers — Decision Tree, Random Forest, XGBoost, Logistic Regression, KNN, and SVM — with a stratified 70/15/15 train/val/test split to preserve class proportions.

**Reported metrics:** Accuracy, macro-F1, confusion matrix, and per-class precision/recall/F1.

**Why this design:** This is a stand-in until the FTY pilot collects real youth-athlete swings (Phase 2). Building the full pipeline against synthetic-but-rule-consistent data lets us validate the modeling approach end-to-end and identify which feature set works best, before the real data collection effort begins.

---

## What I Learned (Big Picture)

Five takeaways stand out across the whole course:

**1. Accuracy alone lies.** The single most important habit shift was learning to never trust a single accuracy number. By Module 12 I was checking subgroup accuracy against group base rates; by Module 07 I was checking confusion matrices to see *which* mistakes a model was actually making. "85% accuracy" is a starting point for analysis, not a finish line.

**2. Cross-validation is the referee.** A single train/test split is one pop quiz; cross-validation is a real evaluation. Once I internalized this from Module 07, I started seeing it everywhere — in hyperparameter search (Module 11), in ensemble comparisons (Module 09), and in fairness audits (Module 12).

**3. Bias and variance pull in opposite directions.** Module 08 made this concrete with polynomial regression. Every modeling choice afterward — model complexity, regularization strength, ensemble method, even how much data to collect — became a deliberate choice about where to land on the bias-variance curve, instead of a vague feeling.

**4. Ensembles aren't magic — they're decorrelation.** Module 09's lesson stuck: a hundred identical trees are no better than one. The whole game is encouraging diversity (different bootstrap samples, different feature subsets) so the errors cancel rather than compound. I saw this play out for real in the Midterm Project — Random Forest and Gradient Boosting both beat Linear Regression on noisy weekly NFL data.

**5. Fairness is a property of the system, not the algorithm.** Module 12 was the most uncomfortable lesson. A mathematically excellent model can still ship discriminatory outcomes, and dropping the protected attribute doesn't fix it. The hardest takeaway: some problems shouldn't be solved with ML at all, and recognizing that early is more responsible than shipping a flawed model with a long disclaimer.

---

## Per-Lab Highlights

### Lab 02 — ML Tools
Set up the core Python ML stack (NumPy, Pandas, Matplotlib, scikit-learn) and built first visualizations on the Iris dataset. Coming from a PHP/MySQL background, pandas felt remarkably like SQL with different syntax — `df[df['col'] > 5]` is just `WHERE col > 5` — which made the learning curve much faster.

### Lab 03 — ML Workflow on Wine Dataset
Walked through the complete 6-step workflow on the Wine classification dataset. Trained both Logistic Regression (88.9% accuracy) and Decision Tree (83.3%); learned that the right algorithm choice depends on dataset shape and size, not which is "best." Biggest lesson: the discipline of splitting data *before* exploration to prevent leakage.

### Lab 04 — EDA on Titanic
Detective work on the Titanic dataset. Built histograms, count plots, box plots, and FacetGrids to surface the survival patterns: class and gender dominate; age shows a child-survival bump; fare is mostly a proxy for class. The "always plot first" rule comes from labs like this.

### Lab 05 — Data Preparation
Built the preprocessing pipeline: median imputation for `Age`, one-hot encoding for `Sex` and `Embarked`, `StandardScaler` for the numeric columns. Internalized why tree-based models *don't* need scaling but distance-based models definitely do.

### Lab 06 — Regression & Classification
First "real" modeling lab. Linear Regression to predict Titanic `Fare` from `Age` and `Pclass`, then Logistic Regression to predict survival from `Age`, `Pclass`, and `Sex` (74.83% accuracy). Learned to read coefficients to understand *why* a model is predicting what it's predicting — the interpretability win that becomes critical in Module 12.

### Lab 07 — Better Model Evaluation
The lab that taught me to distrust accuracy as a single number. Confusion matrix, precision (the "Boy Who Cried Wolf" metric), recall (the "Missing Child" metric), and Stratified K-Fold cross-validation. Learned the **"Pro Way"** of reporting performance: baseline + mean ± std + the business metric that matters.

### Lab 08 — Bias-Variance Tradeoff
Made overfitting visually obvious. Plotted polynomial regressions at degree 1 (line through a sine wave = underfit), degree 4 (just right), and degree 15 (zigzags through every noisy point = overfit). Learning curves taught me to read the *gap* between train and CV scores, not the absolute level of either.

### Lab 09 — Ensemble Methods
Single tree vs. Random Forest on Iris. Both scored 100% on a single split (Iris is small and easy), but cross-validation revealed the real story: Random Forest 96.7% ± 2.1% vs. single tree 95.3% ± 3.4%. Ensembles aren't magic — they're a structural fix for variance via decorrelation.

### Lab 10 — Unsupervised Learning
K-Means with the Elbow Method on synthetic blobs, and PCA on Iris. PC1 alone captured 92.5% of the variance; PC1+PC2 captured 97.8%. PCA had never seen the species labels, but the species clustered cleanly anyway in PC space — proving the labels reflect real structure in the measurements.

### Lab 11 — Hyperparameter Tuning & AutoML
Grid Search vs. Random Search vs. AutoGluon on Iris. All three approaches hit 100% test accuracy because Iris is too small to differentiate them — which is itself the lesson (Slide 22 of the deck: tiny datasets can overfit the validation process). AutoGluon's ensembling-of-strongest-models is the AutoML extra over plain hyperparameter tuning.

### Lab 12 — Ethics, Fairness & Bias
Audited a Logistic Regression on the UCI Adult dataset for sex-based disparate impact. Found a 14-point opportunity gap that the headline 85% accuracy completely hid. Walked through why "fairness through unawareness" (just dropping the `sex` column) doesn't work — `relationship` literally has values "Husband" and "Wife" that re-encode sex with near-perfect fidelity.

---

## Tools and Stack

The labs and projects use the standard Python ML stack: **scikit-learn**, **pandas**, **numpy**, **matplotlib**, **seaborn**, plus **AutoGluon** for the AutoML lab and **XGBoost** for the Final Project. Notebooks were developed in Jupyter and Google Colab.

---

## Course Info

- **Course:** ITAI 1371 — Introduction to Machine Learning
- **Program:** Artificial Intelligence & Robotics, B.A.T.
- **Institution:** Houston Community College
- **Instructor:** Dr. Sina Nazifi
- **Term:** Spring 2026

---

*Thanks for visiting. If anything here is useful to a future student or curious developer, I'm glad — that's a big part of why I'm publishing this publicly.*
