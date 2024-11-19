
# Document Standardization Test Task

This repository contains the solution to the **Document Standardization Test Task**, aimed at identifying header rows in JSON-structured documents using machine learning (ML). The task involves preprocessing data, implementing various ML methods, and evaluating their effectiveness. For detailed insights into the experiments, methodologies, and rationale behind the solutions, refer to the **Detailed Explanation of the Solutions and Methodologies.pdf** file included in this repository.

---

## Table of Contents

1. [Overview](#overview)
2. [Dataset Structure](#dataset-structure)
3. [Methodology](#methodology)
4. [Prerequisites and Installation](#prerequisites-and-installation)
5. [Usage Instructions](#usage-instructions)
6. [Results and Evaluation](#results-and-evaluation)
7. [Next Steps](#next-steps)

---

## Overview

The task is to create an ML solution that can automatically recognize header rows in documents formatted as JSON. Each document has a near-table structure with headers defining columns. These headers can span multiple rows, and the training data provides annotated examples where rows are labeled as "HEADERS" or other types.

---

## Dataset Structure

### Training Data
- **Format:** JSON-structured text file, with each document on a new line.
- **Labeling:** Rows labeled with `type`, e.g., `"HEADERS"`.
- **Example Structure:**
  ```json
  [
    {
      "values": [
        {"value": "Header 1"},
        {"value": "Header 2"}
      ],
      "type": "HEADERS"
    },
    {
      "values": [
        {"value": "Data 1"},
        {"value": "123.45"}
      ],
      "type": "DATA"
    }
  ]
  ```

### Test Data
- **Format:** Similar JSON structure but without `type` annotations.
- **Objective:** The model predicts which rows are headers based on patterns learned from the training data.

---

## Methodology

### 1. Data Analysis and Preprocessing
- **Loading and Parsing:** JSON files were parsed with robust error handling to skip corrupted lines.
- **Label Extraction:** Extracted header labels based on the `"type": "HEADERS"` annotation.
- **Transformation:** Transformed JSON rows into concatenated text strings for processing.

### 2. Feature Engineering
- **TF-IDF Vectorization:** Converted text into numerical format to highlight important words.
- **Feature Selection:** Used Chi-squared tests to retain impactful features, reducing dimensionality.

### 3. Models Explored
1. **TF-IDF + KMeans Clustering**:
   - **Approach:** Addressed imbalances with undersampling and oversampling.
   - **Outcome:** Struggled with high false positives and negatives due to unsupervised nature.
2. **Random Forest with SMOTE**:
   - **Approach:** Applied SMOTE for class balance and used Random Forest for robust classification.
   - **Outcome:** Improved recall but precision issues persisted.
3. **MiniLM Training**:
   - **Approach:** Fine-tuned MiniLM with mixed precision to capture contextual nuances.
   - **Outcome:** Achieved the best performance across all metrics.

---

## Prerequisites and Installation

### System Requirements
- Python 3.8+
- CUDA-enabled GPU (recommended for transformer models)

### Installation
1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/document-standardization.git
   cd document-standardization
   ```
2. Create a virtual environment and activate it:
   ```bash
   python3 -m venv venv
   source venv/bin/activate   # For Linux/macOS
   venv\Scripts\activate      # For Windows
   ```
3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

---

## Usage Instructions

1. **Prepare the Dataset**
   - Place the training and test datasets in the `data/` directory.

2. **Run the Solution**
   Execute the Jupyter Notebook or Python scripts to preprocess data, train models, and generate results:
   ```bash
   jupyter notebook SPACEQUANT_ASSIGNMENT.ipynb
   ```

3. **View Results**
   - Outputs, including predicted labels for test data, are saved in the `output/` directory.

---

## Results and Evaluation

### Metrics
- **TF-IDF + KMeans:** High false positives; unsupervised approach not suitable.
- **Random Forest with SMOTE:** Improved recall but lower precision.
- **MiniLM:** Best performance with high precision, recall, and F1-score.

### General Observations
- MiniLM outperformed traditional methods due to its ability to understand text contextually.
- KMeans struggled with high-dimensional, sparse text data.

---

## Next Steps

1. **Data Augmentation**
   - Generate synthetic examples to improve minority class representation.

2. **Advanced Models**
   - Explore transformers like BERT or T5 for richer contextual embeddings.

3. **Cross-Validation**
   - Implement stratified K-fold cross-validation to ensure robust evaluation.

4. **Graph-Based Techniques**
   - Experiment with Graph Attention Networks to model document structures.

---

## License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
