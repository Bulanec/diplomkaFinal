# Solar Radiation Forecasting with Azure Databricks

## Overview

This project automates the ingestion, processing, and prediction of solar radiation data using time series modeling. The solution is built in Python using Azure Databricks and Azure Machine Learning, and it leverages LSTM and GRU neural network models.

## Context of Use

The code was developed and applied as part of a master's thesis at the Slovak University of Technology in Bratislava, focused on forecasting solar radiation using recurrent neural networks in a cloud environment. It demonstrates the end-to-end implementation of a predictive system for solar energy forecasting, integrating data workflows and machine learning lifecycle management on Microsoft Azure.

## Project Structure

```
├── automated_training.ipynb   # Final model training, evaluation, and registration
├── gold.ipynb                 # Final feature processing and data preparation for training
├── ingestion.ipynb            # Data acquisition from a remote server and storage in the bronze layer
├── localTrainModel.ipynb      # Offline/local model training notebook
├── silver.ipynb               # Intermediate data cleaning and transformation
├── sorted_data_final.csv      # Final preprocessed dataset
```

## Pipeline Stages

### 1. Ingestion

- Checks for new CSV files on a remote server using SSH.
- Downloads and saves them in the Bronze Delta Table layer.
- Ensures ACID-compliant writes using Spark SQL.

### 2. Silver

- Loads new data from Bronze.
- Cleans and transforms it by handling missing values and extracting features.
- Outputs to the Silver Delta Table layer.

### 3. Gold

- Finalizes data processing by removing low-correlation features.
- Sorts by timestamp and saves to the Gold Delta Table.
- Keeps data human-readable for future model flexibility.

### 4. Model Training (`automated_training.ipynb`)

- Merges and normalizes data.
- Applies sliding window segmentation.
- Trains LSTM or GRU models.
- Evaluates using R² and MSE.
- Uses MLflow for experiment tracking.
- Registers the model in Azure ML if performance improves.

### 5. Local Training (`localTrainModel.ipynb`)

- Allows offline experimentation and model tuning on local machines.

## Technologies

- **Azure Databricks**
- **Azure Machine Learning**
- **Python (TensorFlow, Keras, Pandas, NumPy)**
- **MLflow** – for experiment tracking and model versioning
- **Astral** – for sun position calculations used in feature engineering

## Getting Started

1. Clone the repository and upload notebooks to your Azure Databricks workspace.
2. Configure SSH access and data paths in `ingestion.ipynb`.
3. Execute notebooks in the order:
   - `ingestion.ipynb`
   - `silver.ipynb`
   - `gold.ipynb`
   - `automated_training.ipynb`

## License

MIT License
