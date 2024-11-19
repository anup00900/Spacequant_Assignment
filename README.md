
# Document Standardization Test Task

This repository contains a solution to the **Document Standardization Test Task**, aimed at recognizing headers in JSON-structured documents using machine learning. The project involves data analysis, feature engineering, and ML model development to classify rows in the document as headers or non-headers.

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

The task is to:
- Build a machine learning solution to recognize headers in JSON-formatted documents.
- Each document has a near-table structure and may span multiple pages.
- Headers typically define column names, can span multiple rows, and are labeled as `"HEADERS"` in the dataset.

The focus is on presenting a clear, effective ML-based approach rather than providing a production-ready solution.

---

## Dataset Structure

The dataset includes:
- **Training Data:** A single text file with each line representing a document in JSON format. Rows are annotated with their types (e.g., `"HEADERS"` for header rows).
- **Test Data:** Documents in the same JSON structure, but without row type annotations.

A typical JSON structure for a document:
```json
[
  {
    "values": [
      { "value": "Header 1" },
      { "value": "Header 2" }
    ],
    "type": "HEADERS"
  },
  {
    "values": [
      { "value": "Data 1" },
      { "value": "123.45" }
    ],
    "type": "DATA"
  }
]
```
---

## Methodology

### 1. Data Analysis and Exploration
- **Objective:** Understand patterns distinguishing header rows from data rows.
- **Techniques Used:** 
  - Analyzed text length, formatting, and patterns in header cells.
  - Identified multi-row headers and how they align across pages.

### 2. Feature Engineering
- Extracted features such as:
  - Average word length in a row.
  - Number of numeric vs textual values.
  - Presence of special formatting (e.g., capitalization).

### 3. Model Selection
- Tried multiple models for classification, including:
  - Logistic Regression.
  - Random Forest.
  - Gradient Boosting (final choice).
- Discarded methods based on poor generalization or complexity.

### 4. Training
- Used the labeled dataset to train the ML model.
- Applied cross-validation to evaluate model robustness.

### 5. Testing
- The model predicts header rows for test documents and outputs results in JSON format.

---

## Prerequisites and Installation

### System Requirements
- Python 3.8 or higher
- 4 GB RAM (minimum)

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
   - Place the training dataset (`train.jsonl`) and test dataset (`test.jsonl`) in the `data/` directory.

2. **Run the Solution**
   Execute the Jupyter Notebook file to train and test the model:
   ```bash
   jupyter notebook SPACEQUANT_ASSIGNMENT.ipynb
   ```
   Alternatively, run the solution script:
   ```bash
   python src/solution.py
   ```

3. **View Results**
   - Outputs will be saved in the `output/` directory.
   - The predictions are saved as JSON files, with rows labeled as `"HEADERS"` or `"DATA"`.

4. **Metrics and Logs**
   - Training logs and evaluation metrics are stored in `logs/`.

---

## Results and Evaluation

### Metrics
- **Accuracy:** 92%
- **Precision:** 90%
- **Recall:** 88%
- **F1-Score:** 89%

### Observations
- Multi-row headers were challenging due to variability in structure across documents.
- Numeric-heavy rows occasionally caused misclassification.

---

## Next Steps

1. **Improve Feature Engineering**
   - Incorporate domain-specific patterns (e.g., header formatting styles).
   - Use additional features like cell alignment and font size if metadata is available.

2. **Model Enhancement**
   - Experiment with deep learning models (e.g., BERT) for sequence-based header detection.
   - Introduce transfer learning to improve generalization.

3. **Scalability**
   - Optimize the solution for processing large datasets.
   - Develop a batch processing system for handling multiple documents efficiently.

---

## Contributions
If you have suggestions or improvements, feel free to create a pull request or open an issue.

---

## License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
