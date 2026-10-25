# Association-Guided Adaptive Data Re-Uploading for Hybrid Quantum Brain Tumor Classification

## Overview

This project proposes an **Association-Guided Priority-Based Adaptive Data Re-Uploading** approach for hybrid quantum machine learning-based brain tumor classification using MRI images.

The proposed method combines feature association analysis, feature-priority ranking, redundancy-aware feature selection, and a Variational Quantum Classifier (VQC) to reduce unnecessary quantum data-encoding operations while maintaining classification performance.

The project compares a conventional sequential data re-uploading strategy with the proposed adaptive strategy using classification metrics and quantum circuit complexity measurements.

## Objectives

- Extract numerical features from brain MRI images.
- Transform multiclass MRI categories into a binary tumor classification task.
- Develop a hybrid quantum-classical classification model.
- Analyze feature associations using Pearson correlation.
- Rank features using statistical and machine learning-based criteria.
- Adaptively select and order features to reduce redundancy.
- Compare baseline and proposed approaches in terms of predictive performance and computational complexity.

## Project Workflow

The project consists of two Jupyter notebooks.

### 1. MRI Feature Extraction — `data_extraction.ipynb`

This notebook processes MRI images and generates a structured feature dataset for classification.

**Workflow:**

1. Load and extract the MRI dataset.
2. Identify the original image categories.
3. Convert the original classes into binary labels.
4. Resize images to 224 × 224 pixels and convert them to grayscale.
5. Extract 17 numerical image features.
6. Organize the extracted features and labels into a Pandas DataFrame.
7. Handle missing and infinite feature values.
8. Save the processed dataset as a CSV file.

**Binary classification labels:**

| Label | Meaning |
|---|---|
| 0 | No Tumor |
| 1 | Tumor |

Glioma, meningioma, and pituitary tumor images are assigned label `1`, while no-tumor images are assigned label `0`.

### 2. Quantum Model and Adaptive Feature Selection — `qml_proposed.ipynb`

This notebook implements the baseline and proposed hybrid quantum machine learning pipelines.

#### Baseline: Sequential Data Re-Uploading

The baseline model uploads features sequentially according to their original index order across the quantum encoding layers.

#### Proposed: Association-Guided Priority-Based Adaptive Data Re-Uploading

The proposed approach introduces an adaptive feature selection and ordering strategy using the following components:

**Pearson Correlation-Based Association Analysis**

Analyzes pairwise relationships between features to identify strongly associated features. The configured correlation threshold is `0.60`.

**Feature Priority Ranking**

Combines four criteria to estimate feature importance:

- Variance — weight 0.10
- Mutual Information — weight 0.40
- Random Forest Feature Importance — weight 0.40
- Class Separation — weight 0.10

The individual scores are normalized before calculating the combined priority score.

**Redundancy-Aware Adaptive Scheduling**

The scheduler combines feature priority with a redundancy penalty to prioritize informative features while limiting redundant selections.

Key configuration parameters include:

- Redundancy weight: `0.35`
- Cumulative priority threshold: `0.92`
- Minimum selected features: `8`
- Maximum selected features: `16`

**Hybrid Variational Quantum Classifier**

The selected features are encoded using a parameterized quantum circuit, and quantum measurement outputs are processed by a classical linear readout layer to perform binary classification.

The baseline and proposed models use the same training framework to support a consistent comparison.

## Feature Extraction

The project extracts the following 17 numerical features from MRI images:

1. Mean
2. Variance
3. Standard Deviation
4. Entropy
5. Skewness
6. Kurtosis
7. Contrast
8. Energy
9. Angular Second Moment (ASM)
10. Homogeneity
11. Dissimilarity
12. Correlation
13. Coarseness
14. Peak Signal-to-Noise Ratio (PSNR)
15. Structural Similarity Index (SSIM)
16. Mean Squared Error (MSE)
17. DC

The extracted features represent image intensity statistics, texture characteristics, and image-quality-related measurements.

## Technologies Used

- **Programming Language:** Python
- **Quantum Machine Learning:** PennyLane, PennyLane Lightning
- **Deep Learning and Tensor Operations:** PyTorch
- **Classical Machine Learning:** Scikit-learn
- **Image Processing:** OpenCV, scikit-image, SciPy
- **Data Processing:** NumPy, Pandas
- **Visualization:** Matplotlib, Seaborn
- **Execution Environment:** Google Colab

## Experimental Configuration

The proposed notebook uses the following main settings:

| Parameter | Configuration |
|---|---|
| Quantum circuit qubits | 8 |
| Original numerical features | 17 |
| Test set proportion | 20% |
| Random seed | 42 |
| Maximum training epochs | 30 |
| Batch size | 16 |
| Early stopping patience | 5 |
| Optimizer | Adam |
| Learning rate | 0.05 |
| Loss function | Cross-Entropy Loss |

The dataset is split into training, validation, and test sets. Feature association and priority ranking are fitted using training data in the proposed pipeline.

## Evaluation Metrics

The baseline and proposed models are compared using:

- Accuracy
- Precision
- Recall
- F1-score
- ROC-AUC
- Confusion matrix
- ROC curves
- Training time
- Inference time
- Number of trainable parameters
- Quantum circuit depth
- Number of data re-uploading layers
- Peak memory usage

The notebooks generate comparison tables and visualizations to help analyze classification performance and model complexity.

## Repository Structure

```text
quantum-brain-tumor-classification/
│
├── README.md
├── data_extraction.ipynb
└── qml_proposed.ipynb
```

The Python modules used by the proposed notebook are generated from notebook cells during execution.

## How to Run the Project

The notebooks are designed for Google Colab.

### Step 1: Open the notebooks

Upload both notebooks to Google Colab or open them directly from your GitHub repository.

### Step 2: Prepare the dataset

Place the MRI dataset archive at the path expected by `data_extraction.ipynb`, or update the dataset path in the notebook to match your Google Drive location.

The extraction notebook expects a dataset archive named `balanced_dataset.zip` by default.

### Step 3: Extract the features

Run `data_extraction.ipynb` from top to bottom to process the MRI images and generate the feature CSV file.

The default output is:

```text
/content/drive/MyDrive/bd.csv
```

### Step 4: Run the quantum classification pipeline

Ensure that the generated CSV is available at the path expected by `qml_proposed.ipynb`.

Execute the proposed notebook sequentially to:

1. Load and preprocess the feature dataset.
2. Train the baseline sequential model.
3. Analyze feature associations and calculate feature priorities.
4. Generate the adaptive feature order.
5. Train and evaluate the proposed model.
6. Compare the results and generate plots.
7. Extract features from a new MRI image and run a prediction using the trained proposed model.

### Step 5: Review the results

Inspect the evaluation tables, classification metrics, training curves, confusion matrices, ROC curves, and circuit complexity comparisons produced by the notebook.

## Expected Outcome

The project aims to investigate whether association-guided priority ranking and redundancy-aware adaptive feature selection can reduce unnecessary data re-uploading and quantum circuit complexity while maintaining or improving binary brain tumor classification performance.

Actual performance should be reported using the results obtained from the executed notebooks.

## Limitations

- The classification task is binary: tumor versus no tumor.
- The model depends on the quality and representativeness of the MRI dataset.
- The notebooks require the dataset to be supplied separately.
- Results may vary with the execution environment and dataset configuration.
- The classification output is intended for research and educational purposes and is not a substitute for professional medical diagnosis.

## Author

**Nandhini Sundhar**

Master of Computer Applications (MCA)  
Vellore Institute of Technology

