# Data Science Lab: Process and Methods  
**Politecnico di Torino**  
**Project Assignment**  
**Winter Call, A.Y. 2024/2025**  

_Last update: January 6, 2025_

---

## 1. Project Dates  

| **Start date** | January 6, 2025 at 23:59 (CET) |
|----------------|--------------------------------|
| **Due date**   | January 28, 2025 at 23:59 (CET) |

**Note**: Due date is a strict deadline.

---

## 2. Problem Description  

Within the field of speech processing, a long-standing task of interest is estimating the age of a speaker based on their vocal characteristics. Some systems are capable of analyzing spoken sentences to extract features that correlate with the speaker's age. One such approach involves leveraging acoustic and linguistic features derived from the speech signal.

When a speaker produces a spoken sentence, various feature extraction methods are applied to analyze the acoustic properties of the speech signal. In the specific system of interest, these features include, among others, pitch, formants, energy levels, and phonetic patterns. These extracted features serve as inputs to the problem, with their properties being correlated with the speaker's age.

The process of estimating a speaker’s age from their speech is referred to as **age estimation**. The target (output) of the system is a single value representing the estimated age of the speaker.  
The goal of this project is to build a data science pipeline that predicts, for each spoken sentence, the target age of the speaker, using the available metadata as inputs, along with any other feature that can be potentially extracted from the input speech.

---

### 2.1 Dataset  

The dataset is comprised of **3,624 samples**:
- **2,933 samples** for the development set.
- **691 samples** for the evaluation set.

Each sample corresponds to a spoken sentence, and the associated speaker’s age is provided as the target label. The speech samples have been collected in controlled conditions to ensure consistent feature extraction.

For each sample, a variety of **acoustic and linguistic features** have been extracted from the speech signal. These features form the dataset and include:

- **sampling rate**: the sampling rate of the audio signal, in Hz.
- **age**: the chronological age of the speaker (target label).
- **gender**: the gender of the speaker.
- **ethnicity**: the ethnicity of the speaker.
- **mean pitch, max pitch, min pitch**: mean, maximum, and minimum pitch of the speech signal, in Hz.
- **jitter**: a measure of the variations in pitch, representing voice stability.
- **shimmer**: a measure of amplitude variations in the speech signal.
- **energy**: the overall energy of the speech signal.
- **zcr mean**: the mean zero-crossing rate, indicating the number of times the signal changes sign.
- **spectral centroid mean**: the mean spectral centroid, representing the “center of mass” of the frequency spectrum.
- **tempo**: the estimated speaking rate, in beats per minute (BPM).
- **hnr**: the harmonic-to-noise ratio, indicating voice quality.
- **num words, num characters**: the number of words and characters in the spoken sentence.
- **num pauses**: the number of pauses detected in the speech.
- **silence duration**: the total duration of silence within the speech signal, in seconds.
- **path**: the file path to the audio recording.

These features comprehensively capture the acoustic properties of the speech signal along with some linguistic metadata, but you are allowed to extract additional features from the speech signal.  
For each sample, the target variable is the speaker’s age, represented as a continuous numerical value in the **age** column of the dataset.

⚠️ **Warning**: For this project, you are not allowed to use external datasets other than the one provided. Adoption of external resources, including pre-trained models, will result in failure of the exam.

---

### Dataset Contents:
The dataset is located at [this URL](#).

- **development.csv (development set)**: A comma-separated values file containing the 2,933 samples for the development set. This portion includes the target age for each sample, which is used to train and validate your models.
- **evaluation.csv (evaluation set)**: A comma-separated values file containing the 691 samples corresponding to the evaluation set. This portion does not contain the age target.
- **sample_submission.csv**: A sample submission file.
- **audio_development/**: A folder containing the audio files corresponding to the development set.
- **audio_evaluation/**: A folder containing the audio files corresponding to the evaluation set.

---

## 2.2 Task  

You are required to build a **regression pipeline** to predict the **age of the speaker**.

---

## 2.3 Evaluation metric  

Your submissions will be evaluated in terms of the **Root Mean Square Error (RMSE)** between your predictions and the target values. RMSE is a standard metric for regression tasks that measures the **average magnitude of the error**.  

For a single prediction with target \(y_1\) and prediction \(\hat{y}_1\), the squared error is:  

\[
(y_1 - \hat{y}_1)^2
\]

For all \(n\) samples with targets \(y_1, y_2, \dots, y_n\) and predictions \(\hat{y}_1, \hat{y}_2, \dots, \hat{y}_n\), the RMSE is computed as:  

\[
\text{RMSE} = \sqrt{\frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2}
\]

This metric provides an **aggregate measure of prediction accuracy**, penalizing **larger errors** more significantly than smaller ones.
