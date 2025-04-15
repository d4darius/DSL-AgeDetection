# Age Detection from Speech Signals

**Politecnico di Torino**  
**Data Science Lab Winter Project 2024/2025**

---

## 1. Project Overview

This project focuses on building a **regression pipeline** to predict the **age of a speaker** based on their vocal characteristics. The task involves analyzing spoken sentences to extract acoustic and linguistic features that correlate with the speaker's age. The target output is a single numerical value representing the estimated age of the speaker.

---

## 2. Dataset Description

The dataset consists of **3,624 samples**, divided into:

- **Development set**: 2,933 samples (with target age labels).
- **Evaluation set**: 691 samples (without target age labels).

Each sample corresponds to a spoken sentence, and the dataset includes various **acoustic and linguistic features**, such as:

- **Acoustic features**: pitch, jitter, shimmer, energy, zero-crossing rate, spectral centroid, tempo, harmonic-to-noise ratio, etc.
- **Linguistic features**: number of words, number of characters, number of pauses, silence duration.
- **Metadata**: gender, ethnicity, and file path to the audio recording.

---

## 3. Project Workflow

### 3.1 Data Exploration

- Inspected the dataset for missing values and outliers.
- Removed outliers based on the 99th percentile of the age distribution.
- Analyzed feature correlations and removed highly correlated features (e.g., `num_characters` and `silence_duration`).

### 3.2 Feature Engineering

- Extracted additional features from audio recordings, such as:
  - **MFCCs (Mel-Frequency Cepstral Coefficients)**: Reduced dimensionality using PCA.
  - **Spectral contrast and roll-off**.
- Applied **Within-Class Covariance Normalization (WCCN)** to reduce intra-class variability.
- Standardized numerical features using z-score normalization.
- Encoded categorical features (e.g., gender and grouped ethnicities) using one-hot encoding.

### 3.3 Feature Selection

- Used a Ridge regression model to identify and drop features with low importance.

---

## 4. Model Development

### 4.1 Baseline Models

- **Naive solution**: Predicted the mean age for all samples.
- **Simple linear regression**: Used basic features for prediction.

### 4.2 Advanced Models

- Tested the following regression models:
  - **Decision Tree Regressor**
  - **Random Forest Regressor**
  - **Support Vector Regressor (SVR)**
  - **Multi-Layer Perceptron (MLP) Regressor**

### 4.3 Hyperparameter Tuning

- Performed grid search to optimize hyperparameters for:
  - **SVR**: Tuned `C`, `epsilon`, and `kernel`.
  - **Random Forest**: Tuned `n_estimators`, `max_depth`, `max_features`, and `criterion`.
  - **MLP**: Tuned `hidden_layer_sizes`, `alpha`, and `learning_rate`.

---

## 5. Evaluation

### Metrics

- **R² Score**: Measures the proportion of variance explained by the model.
- **Root Mean Squared Error (RMSE)**: Measures the average prediction error.

### Results

- The best-performing models were:
  - **SVR**: Achieved the lowest RMSE with optimized hyperparameters.
  - **Random Forest**: Performed well with a balanced trade-off between accuracy and interpretability.
  - **MLP**: Demonstrated strong performance with deep learning techniques.

---

## 6. Predictions

Final predictions for the evaluation set were saved in the following files:

- `TESTS/predictions_final_SVR.csv`
- `TESTS/predictions_final_RF.csv`
- `TESTS/predictions_final_MLP.csv`

---

## 7. How to Run the Project

1. **Install dependencies**:
   Ensure you have Python installed along with the required libraries:
   ```bash
   pip install numpy pandas matplotlib scikit-learn librosa
   ```
2. **Prepare the dataset**:
   Place the dataset files (development.csv, evaluation.csv, and audio files) in the `DSL_Winter_Project_2025/ directory`.

3. **Run the notebook**:
   Open and execute the `DSL-AgeDetection.ipynb` notebook.

4. **Generate predictions**:
   The notebook will output predictions for the evaluation set in the `TESTS/ directory`.

### Contributors:
- Maretto Chiara: s339401
- Gosmar Dario: s337625
