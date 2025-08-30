# Fraud-Detection-Analysis
A project to detect Fraudulent transactions on Large Bank Dataset (6M+ rows, 400MB)

Overview
- End-to-end fraud detection built for large-scale tabular data with strict RAM limits using out-of-core processing and compact dtypes.[1]
- Reads CSV in 500k-row chunks, engineers features per chunk, and writes Parquet shards; trains on a bounded sample for stability.[1]

Data pipeline
- Ingest from Google Drive, select needed columns, enforce int32/float32/int8, and drop heavy strings after deriving indicators.[1]
- Convert to Parquet via pyarrow for fast columnar reads; reservoir-style sampling assembles a capped training dataset without loading everything.[1]

Modeling
- Lightweight feature selection via mutual information on numeric predictors to pick top-K informative features.[1]
- Trains two classifiers: Logistic Regression (standardized, class-balanced) and a shallow Random Forest (regularized, class-balanced).[1]

Evaluation
- Uses ROC/AUC, Precision-Recall/AP, confusion matrix for best model, and Random Forest feature importances for interpretability.[2]

Results
- On the sampled set, Random Forest achieved higher AUC and AP than Logistic Regression, indicating superior ranking and minority-class precision.[3]

Reproducibility
- Deterministic splits and seeds; modular code cells for ingestion, feature engineering, selection, training, and evaluation.[1]

Getting started
- Mount Drive in Colab, set INPUT_CSV path, run the notebook sequentially; adjust CHUNKSIZE and SAMPLE_ROWS_FOR_TRAIN to fit RAM.[1]

