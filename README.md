# EEG-MotorImagery-Classification-Using-Random-Forest
This repository contains the implementation of signal processing and feature extraction techniques for **Motor Imagery (MI) EEG datasets**. The project focuses on processing neural signals to identify patterns associated with imagined movements, a core component of Brain-Computer Interface (BCI) systems.

## Overview
The goal of this project is to transform raw EEG data into a structured feature matrix suitable for machine learning classification. It utilizes advanced signal processing methods to extract frequency-domain and time-domain characteristics from `.mat` files.

## Dataset Description
The data used in this project follows a specific experimental paradigm for Motor Imagery:
* **Experimental Tasks:** Imagination of movement for the **Left Hand (LH)**, **Right Hand (RH)**, and **Both Feet (F)**.
* **Paradigm Details:** * Trials begin with a blank screen ($t=2s$).
    * A visual cue (arrow) appears for a duration of 3-10 seconds, prompting the subject to perform the imagery task.
    * Data was recorded from healthy subjects using devices such as **g.tec** and **Neuroscan** at sampling rates of **250Hz - 256Hz**.
* **Data Source:** Lab. for Advanced Brain Signal Processing (RIKEN) in collaboration with Shanghai Jiao Tong University.

## Tech Stack
- **Language:** Python
- **Libraries:** - `MNE`: For EEG/MEG data handling.
  - `SciPy`: For signal processing (Welch’s method, integration).
  - `NumPy` & `Pandas`: For data manipulation.
  - `Matplotlib`: For signal visualization.

## How It Works (Technical Pipeline)
The implementation follows a structured signal processing pipeline to transform raw EEG signals into meaningful features:

### 1. Data Loading & Preprocessing
* **Format Handling:** The script loads `.mat` files containing raw EEG signals and their corresponding labels.
* **Signal Segmentation:** It identifies specific time windows (epochs) where the motor imagery tasks (LH, RH, or Feet) occurred based on the visual cues described in the experimental paradigm.

### 2. Spectral Analysis (Welch’s Method)
To analyze the power distribution of the brain waves, the project implements **Welch’s Method**:
* **Windowing:** The signal is divided into overlapping segments to reduce noise.
* **FFT (Fast Fourier Transform):** Each segment is converted from the time domain to the frequency domain.
* **PSD Estimation:** It calculates the **Power Spectral Density**, which shows which frequencies (e.g., Alpha or Beta bands) are most active during the imagery task.

### 3. Feature Extraction
Once the PSD is calculated, the code extracts quantitative features:
* **Frequency Band Integration:** It focuses on specific brain wave ranges relevant to motor movement (typically Mu and Beta bands).
* **Trapezoidal Rule Integration:** The code uses numerical integration (trapezoidal rule) to calculate the "Area Under the Curve" of the PSD. This represents the total energy/power within a specific frequency band.
* **Feature Matrix Construction:** These energy values are compiled into a structured matrix where:
    * **Rows** represent individual trials.
    * **Columns** represent features (Power of specific channels/frequencies).

### 4. Classification Readiness
* The final output is a cleaned **Feature Matrix** and a **Label Vector**, which are formatted and ready to be fed into Machine Learning classifiers (such as SVM, LDA, or Random Forest) for movement prediction.
