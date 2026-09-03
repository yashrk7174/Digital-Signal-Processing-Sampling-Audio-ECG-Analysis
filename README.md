# Digital Signal Processing: Sampling, Spectral Analysis, Audio & ECG Processing

> **Engineering Project | Digital Signal Processing | Python | Audio & Biomedical Signal Processing**

A practical Digital Signal Processing project focused on understanding how continuous-time signals can be **sampled, reconstructed, analyzed in the frequency domain, manipulated, and digitally filtered**.

The project applies DSP concepts to both **synthetic signals and real-world data**, including audio recordings and ECG signals.

---

## 1. Problem Statement

The objective of this project was to investigate how digital signal-processing techniques can be used to process continuous-time signals while preserving their important information.

The main engineering challenges addressed were:

* How to select an appropriate sampling frequency without introducing aliasing.
* How to reconstruct a continuous-time signal from discrete samples.
* How to identify frequency components using FFT/DFT.
* How to reduce spectral leakage during frequency-domain analysis.
* How to extract physical information such as vehicle speed from audio using the Doppler effect.
* How to analyze time-varying audio signals using STFT.
* How to modify vocal pitch while maintaining acceptable audio quality.
* How to remove different types of noise from ECG signals without significantly distorting the waveform.

---

# 2. What I Did

The project was implemented as a series of practical DSP experiments covering the complete signal-processing workflow.

### Signal Sampling & Reconstruction

* Generated sine, square, and triangle signals.
* Investigated different sampling frequencies.
* Demonstrated undersampling and aliasing.
* Compared sampled signals with high-resolution reference signals.
* Reconstructed signals using:

  * Linear interpolation
  * Zero-Order Hold (ZOH)
  * Sinc interpolation

### Frequency-Domain Analysis

* Implemented FFT/DFT-based spectral analysis.
* Investigated fundamental and harmonic frequency components.
* Studied spectral leakage.
* Compared different window functions:

  * Rectangular
  * Hann
  * Hamming
  * Bartlett
  * Blackman
  * Kaiser

### Audio & Doppler Analysis

* Processed WAV recordings containing passing vehicles.
* Extracted dominant frequency peaks using FFT.
* Compared approaching and receding frequencies.
* Applied the Doppler effect to estimate vehicle velocity.
* Estimated the dominant source/horn frequency.

### Time-Frequency Analysis

* Implemented Short-Time Fourier Transform (STFT).
* Generated audio spectrograms.
* Investigated the time-frequency resolution trade-off.
* Applied pitch-processing techniques to vocal recordings.
* Evaluated different pitch-shifting factors.

### ECG Signal Processing

* Generated ECG signals for controlled experiments.
* Added different noise components:

  * Gaussian noise
  * Baseline wander
  * 50 Hz power-line interference
* Implemented and compared multiple denoising techniques:

  * High-Pass Filter
  * Notch Filter
  * Savitzky-Golay Filter
  * Median Filter
  * Moving Average
  * Fourier Filtering
  * LMS Adaptive Filter
  * Wavelet Denoising
* Evaluated filter performance using quantitative metrics.

---

# 3. Engineering Methodology

The overall processing workflow was:

```text
Signal Generation / Real Data
            │
            ▼
     Sampling & ADC Model
            │
            ▼
   Sampling Rate Analysis
            │
            ▼
  Reconstruction / Interpolation
            │
            ▼
    Time-Domain Analysis
            │
            ▼
       FFT / DFT Analysis
            │
            ▼
     Windowing & Filtering
            │
       ┌────┴─────┐
       ▼          ▼
    Audio        ECG
   Processing   Processing
       │          │
       ▼          ▼
 Doppler/STFT   Denoising
       │          │
       └────┬─────┘
            ▼
     Quantitative Evaluation
```

---

## 4. Sampling & Reconstruction

The sampling experiments demonstrated the practical importance of the Nyquist-Shannon sampling theorem.

For a band-limited signal:

<p align="center">
  <strong>f<sub>s</sub> ≥ 2f<sub>max</sub></strong>
</p>

where:

* `f_s` = sampling frequency
* `f_max` = maximum frequency component

When the sampling frequency was insufficient, spectral overlap occurred and the original signal could no longer be accurately recovered.

The experiments also showed that increasing the sampling frequency improves the representation of the original signal and reduces the possibility of aliasing.

---

# 5. FFT & Windowing

FFT was used to transform signals from the time domain into the frequency domain.

The experiments demonstrated:

* Fundamental frequency identification.
* Harmonic analysis.
* Spectral leakage.
* Effect of DFT-bin alignment.
* Influence of window functions on frequency resolution and spectral leakage.

### Window Comparison

| Window      | Main Engineering Characteristic                       |
| ----------- | ----------------------------------------------------- |
| Rectangular | High frequency resolution but strong spectral leakage |
| Hann        | Good general trade-off between leakage and resolution |
| Hamming     | Good amplitude-peak identification                    |
| Bartlett    | Moderate leakage suppression                          |
| Blackman    | Strong spectral leakage suppression                   |
| Kaiser      | Adjustable leakage/resolution trade-off               |

The experiments showed that **Hann and Hamming provided particularly useful compromises between spectral leakage suppression and frequency resolution**.

---

# 6. Audio & Doppler Analysis

A passing-vehicle audio recording was analyzed to estimate vehicle velocity from the Doppler frequency shift.

### Processing Approach

```text
WAV Recording
     │
     ▼
Mono Conversion
     │
     ▼
Time-Segment Selection
     │
     ▼
Windowing
     │
     ▼
FFT
     │
     ▼
Dominant Peak Detection
     │
     ▼
Approaching / Receding Frequencies
     │
     ▼
Doppler Equation
     │
     ▼
Vehicle Speed
```

### Experimental Results

| Parameter               |         Result |
| ----------------------- | -------------: |
| Approaching frequency   |         540 Hz |
| Receding frequency      |         502 Hz |
| Estimated vehicle speed |  **12.51 m/s** |
| Estimated vehicle speed | **45.03 km/h** |
| Identified musical note |         **C4** |

A second simulated vehicle recording produced an estimated speed of **28.04 m/s (100.93 km/h)** and a source frequency of approximately **503.48 Hz**.

---

# 7. STFT & Pitch Processing

A conventional FFT provides frequency information over an entire signal segment but does not directly show how frequencies evolve over time.

To address this, STFT was used to obtain a time-frequency representation.

### STFT Workflow

```text
Audio Signal
     │
     ▼
Windowing
     │
     ▼
Frame-by-Frame FFT
     │
     ▼
Magnitude / Phase
     │
     ▼
Spectrogram
```

The experiments investigated the relationship between:

* Window size
* Hop length
* FFT size
* Time resolution
* Frequency resolution

Pitch-shifting experiments were also performed on vocal recordings.

The measured vocal frequency was approximately **249 Hz**, corresponding closely to **B3**.

A pitch-shifting factor of approximately **1.10** provided a favorable result while avoiding the excessive synthetic/robotic artifacts observed with larger shifts.

---

# 8. ECG Signal Denoising

The ECG processing stage focused on removing multiple realistic noise sources while preserving the morphology of the ECG waveform.

### Noise Model

```text
Clean ECG
    │
    ├── Gaussian Noise
    │
    ├── Baseline Wander
    │
    └── 50 Hz Power-Line Interference
             │
             ▼
        Noisy ECG
             │
             ▼
      Filtering Pipeline
             │
             ▼
       Cleaned ECG
```

### Filters Investigated

| Filter         | Primary Purpose                                 |
| -------------- | ----------------------------------------------- |
| High-Pass      | Baseline-wander suppression                     |
| Notch          | 50 Hz power-line interference                   |
| Savitzky-Golay | Noise reduction while preserving waveform shape |
| Median         | Impulsive-noise suppression                     |
| Moving Average | Smoothing                                       |
| Fourier        | Frequency-domain noise removal                  |
| LMS Adaptive   | Adaptive noise cancellation                     |
| Wavelet        | Multi-scale denoising                           |

---

# 9. Key Results

### Sampling

* Demonstrated the relationship between sampling frequency and signal bandwidth.
* Successfully reproduced aliasing under insufficient sampling conditions.
* Confirmed the importance of satisfying the Nyquist criterion for reliable reconstruction.
* Compared different reconstruction techniques and their waveform characteristics.

### Spectral Analysis

* Successfully identified fundamental and harmonic components using FFT.
* Demonstrated spectral leakage in finite-length signals.
* Showed how window selection changes spectral resolution and side-lobe behavior.
* Found Hann and Hamming windows particularly effective for practical spectral analysis.

### Doppler Analysis

* Estimated vehicle velocity directly from acoustic frequency shifts.
* Obtained approximately **45.03 km/h** for one real-world recording.
* Obtained approximately **100.93 km/h** for a simulated vehicle recording.

### Audio Processing

* Identified the dominant vocal frequency around **249 Hz**.
* Classified the vocal pitch as approximately **B3**.
* Investigated pitch-shifting factors and their effect on audio quality.
* Found a shift factor around **1.10** to provide a favorable result in the tested recording.

### ECG Denoising

Three complete filtering combinations were quantitatively evaluated:

| Filter Combination                   |         MSE |         SNR |
| ------------------------------------ | ----------: | ----------: |
| High-Pass + Notch + Moving Average   | **0.00524** | **6.17 dB** |
| Wavelet + Savitzky-Golay + High-Pass |     0.00583 |     5.70 dB |
| High-Pass + Notch + LMS Adaptive     |     0.00535 |     6.08 dB |

Based on the evaluated combinations, **High-Pass + Notch + Moving Average** achieved the lowest MSE and highest SNR in the available experiment.

---

# 10. My Contribution

I was responsible for implementing and analyzing the DSP experiments using Python.

### My technical contributions included:

* Developed Python-based signal-generation and analysis workflows.
* Implemented sampling experiments and aliasing demonstrations.
* Implemented multiple signal reconstruction techniques.
* Developed FFT/DFT analysis pipelines.
* Compared multiple windowing functions.
* Implemented frequency-peak detection for audio signals.
* Developed Doppler-based vehicle-speed estimation.
* Implemented STFT-based time-frequency analysis.
* Investigated pitch-shifting behavior and audio quality.
* Designed and evaluated multi-stage ECG denoising pipelines.
* Compared filtering approaches using quantitative metrics.
* Developed interactive parameter controls using `ipywidgets`.
* Visualized and interpreted results in both time and frequency domains.

---

# 11. Technical Understanding

This project strengthened my understanding of how DSP theory translates into practical engineering implementations.

### Signal Processing

I developed practical understanding of:

* Sampling theory
* Nyquist frequency
* Aliasing
* Reconstruction
* Interpolation
* FFT and DFT
* Spectral leakage
* Window functions
* Harmonic analysis

### Time-Frequency Processing

I gained practical experience with:

* STFT
* Spectrogram interpretation
* Window-size selection
* Time-frequency resolution
* Phase-based audio processing
* Pitch shifting

### Digital Filtering

The project provided hands-on experience with:

* Frequency-selective filtering
* High-pass filtering
* Notch filtering
* Smoothing
* Adaptive filtering
* Wavelet denoising
* Multi-stage filtering pipelines

### Engineering Evaluation

Rather than relying only on visual plots, filter performance was evaluated using quantitative metrics such as:

* Mean Squared Error (MSE)
* Signal-to-Noise Ratio (SNR)
* Frequency-domain peak analysis

---

# 12. Skills Demonstrated

### Digital Signal Processing

`Sampling` `Aliasing` `FFT` `DFT` `STFT` `Windowing` `Filtering` `Interpolation` `Spectral Analysis`

### Audio Signal Processing

`Doppler Analysis` `Spectrograms` `Pitch Detection` `Pitch Shifting` `Frequency Peak Detection`

### Biomedical Signal Processing

`ECG Processing` `Noise Modeling` `Baseline Wander Removal` `Power-Line Interference Removal` `Denoising`

### Python

`NumPy` `SciPy` `Matplotlib` `Librosa` `Torchaudio` `PyWavelets` `Scikit-learn` `IPyWidgets`

### Engineering & Analysis

`Signal Modeling` `Algorithm Development` `Parameter Tuning` `Experimental Analysis` `Quantitative Evaluation` `Data Visualization`

---

# 13. Technologies & Libraries

| Technology           | Application                                                      |
| -------------------- | ---------------------------------------------------------------- |
| **Python**           | Core DSP implementation                                          |
| **NumPy**            | Numerical computation and signal generation                      |
| **SciPy**            | FFT, filtering, interpolation, peak detection, signal processing |
| **Matplotlib**       | Time-domain and frequency-domain visualization                   |
| **Librosa**          | Audio analysis and spectrogram processing                        |
| **Torchaudio**       | Audio loading, STFT and inverse spectrogram processing           |
| **PyWavelets**       | Wavelet-based ECG denoising                                      |
| **Scikit-learn**     | MSE-based quantitative evaluation                                |
| **IPyWidgets**       | Interactive DSP parameter exploration                            |
| **gdown**            | Downloading experimental audio data                              |
| **Jupyter Notebook** | Interactive experimentation and documentation                    |


```

---

# 14. Key Takeaways

This project provided hands-on experience in moving from **DSP theory to practical engineering implementation**.

The main takeaway was that effective signal processing requires more than applying an algorithm. It requires understanding:

```text
Signal Characteristics
        ↓
Sampling Requirements
        ↓
Frequency Content
        ↓
Algorithm Selection
        ↓
Parameter Selection
        ↓
Quantitative Evaluation
        ↓
Engineering Interpretation
```

The project therefore strengthened both my **DSP fundamentals** and my ability to implement, visualize, evaluate, and interpret signal-processing algorithms using Python.

---

# 15. Author

**Yash Khiste**

M.Sc. Electrical Engineering & Information Technology
Otto von Guericke University Magdeburg, Germany

**Technical Interests**

`Control Systems` • `Digital Signal Processing` • `Robotics` • `Automation` • `Signal Analysis` • `Embedded Systems`

---

## Academic Project

**Digital Information Processing Lab — 2025**
