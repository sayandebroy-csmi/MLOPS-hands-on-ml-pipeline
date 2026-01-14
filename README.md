# MLOPS Hands-On ML Pipeline

A complete MLOps pipeline for spam classification using DVC (Data Version Control) for experiment tracking and data versioning with AWS S3.

## 📋 Overview

This project demonstrates a production-ready ML pipeline that includes:
- **Data Ingestion** - Loading and splitting data into train/test sets
- **Data Preprocessing** - Text cleaning and normalization
- **Feature Engineering** - TF-IDF vectorization
- **Model Building** - Random Forest Classifier training
- **Model Evaluation** - Performance metrics tracking

## 🏗️ Project Structure

```
├── data/
│   ├── raw/              # Raw train/test data
│   ├── interim/          # Preprocessed data
│   └── processed/        # Feature-engineered data (TF-IDF)
├── src/
│   ├── data_ingestion.py
│   ├── data_preprocessing.py
│   ├── feature_engineering.py
│   ├── model_building.py
│   └── model_evaluation.py
├── models/               # Trained model artifacts
├── reports/              # Evaluation metrics
├── dvclive/              # DVC Live metrics & plots
├── logs/                 # Pipeline execution logs
├── dvc.yaml              # DVC pipeline definition
├── params.yaml           # Pipeline parameters
└── requirements.txt      # Python dependencies
```

## 🚀 Getting Started

### Prerequisites

- Python 3.8+
- DVC installed (`pip install dvc`)
- AWS CLI configured (for S3 remote storage)

### Installation

1. Clone the repository:
   ```bash
   git clone <repository-url>
   cd MLOPS-hands-on-ml-pipeline
   ```

2. Create a virtual environment:
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

4. Pull data from DVC remote:
   ```bash
   dvc pull
   ```

## ⚙️ Pipeline Configuration

The pipeline is configured via `params.yaml`:

| Parameter | Description | Default |
|-----------|-------------|---------|
| `data_ingestion.test_size` | Train/test split ratio | 0.25 |
| `feature_engineering.max_features` | Max TF-IDF features | 30 |
| `model_building.n_estimators` | Random Forest trees | 22 |
| `model_building.random_state` | Random seed | 2 |

## 🔄 Running the Pipeline

### Run the full pipeline:
```bash
dvc repro
```

### Run a specific stage:
```bash
dvc repro <stage_name>
```

Available stages:
- `data_ingestion`
- `data_preprocessing`
- `feature_engineering`
- `model_building`
- `model_evaluation`

## 📊 Model Performance

Current model metrics:

| Metric | Value |
|--------|-------|
| Accuracy | 93.27% |
| Precision | 79.88% |
| Recall | 68.95% |
| AUC | 91.43% |

## 🧪 Experiment Tracking

DVC Live is used for experiment tracking. Metrics and plots are stored in:
- `dvclive/metrics.json` - Current metrics
- `dvclive/plots/metrics/` - Training plots (accuracy, precision, recall)

### Compare experiments:
```bash
dvc exp show
```

### Run new experiment with different params:
```bash
dvc exp run -S model_building.n_estimators=50
```

## 📦 Dependencies

- numpy==2.2.6
- pandas==2.3.3
- scikit-learn==1.7.2
- nltk==3.9.2
- dvclive==3.49.0

## 📝 License

This project is licensed under the terms specified in the [LICENSE](LICENSE) file.
