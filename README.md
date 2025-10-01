# Automatic frequency response analysis and parametric EQ generation for in room speakers

This project implements a full end-to-end parametric equalizer measurement system in both **Android (Java/Kotlin + C++/JNI)** and **Python**, demonstrating cross-platform DSP skills and practical audio engineering workflows.

---

## Android Implementation

The Android app provides an on-device measurement pipeline that records Farina sweeps through the device microphone, processes the recordings natively in C++ (via JNI + KissFFT), and visualizes frequency responses relative to target curves.

### Key Features
- **Audio Recording**: Capture multi-sweep recordings directly on Android devices.
- **Native DSP (C++ with JNI)**:
  - Farina exponential sweep generation and inverse filter computation
  - Marker-based segmentation and multi-sweep detection
  - FFT-based deconvolution (using KissFFT) to extract impulse responses
  - Frequency response computation (0–20 kHz), normalized at 1 kHz
  - Averaging across multiple sweeps for robust measurements
- **Graphing and Visualization**:
  - Logarithmic x-axis (20 Hz – 20 kHz)
  - y-axis constrained to –20 dB to +20 dB
  - Overlay with pre-defined target EQ curves
- **Multi-Target Curves**: Preloaded frequency response curves (e.g., Harman) selectable in the UI.
- **JNI Integration**:
  - `dsp_native.cpp/h` handles DSP pipeline
  - `DSPProcessor.java` bridges native code to the Android UI
  - `DataStore.java` handles WAV parsing and array conversions

### Technical Highlights
- **Android Audio + JNI Integration**: Managed real-time buffers between Java and C++.
- **KissFFT on Android**: Integrated KissFFT for efficient FFT/IFFT on mobile platforms.
- **Signal Processing Pipeline**:
  - Sweep → Inverse filter → Deconvolution → Impulse response → FFT → FR averaging
- **Robustness**:
  - Multiple sweeps segmented and averaged to reduce noise
  - Processing tested against Python reference implementation for validation

---

## Python Reference Implementation

The project includes a full Python reference implementation of the Farina sweep measurement and analysis pipeline. This served as the **prototype and validation tool** for the Android port.

### Python Features
- **Sweep & Inverse Filter Generation** using NumPy
- **Marker-based Segmentation** with `scipy.signal.fftconvolve` and `find_peaks`
- **Deconvolution** using inverse filter and FFT convolution
- **Frequency Response Estimation** via FFT (`numpy.fft.rfft`)
- **Optional Smoothing** using Savitzky–Golay filtering
- **Target Curve Comparison** with CSV-loaded curves
- **Visualization** with Matplotlib (semilogx scaling)

### Example Workflow
1. Play back generated sweep through headphones/speakers.
2. Record response with a microphone.
3. Segment multiple sweeps using 1 kHz marker beeps.
4. Deconvolve sweeps, normalize, and average impulse responses.
5. Plot measured vs. target frequency response (log-scaled).

This implementation ensured mathematical correctness and validated Android results.

---

## Skills Demonstrated

- **Digital Signal Processing**: Convolution, FFT/IFFT, windowing, impulse response analysis.
- **Cross-Platform Development**: Translating Python/Numpy + SciPy logic into C++ (KissFFT) on Android.
- **JNI / NDK**: Integrating high-performance native DSP into an Android application.
- **Systems Design**: Building a reliable pipeline from raw audio recording → processing → visualization.
- **Audio Engineering**: Designing repeatable sweep measurement methods (multi-sweep averaging, 1 kHz normalization).
- **Practical Debugging**: Solved challenges in buffer alignment, FFT normalization, segmentation accuracy, and Android CMake builds.

---


## Repository Structure
```
.
├── android-app/
│   ├── java/com/ece420/parametric_eq/
│   │   ├── ProcessActivity.java
│   │   ├── DSPProcessor.java
│   │   ├── DataStore.java
│   ├── cpp/
│   │   ├── dsp_native.cpp
│   │   ├── dsp_native.h
│   │   └── kiss_fft/   # FFT engine
│   ├── res/layout/
│   │   └── activity_process.xml
│   └── CMakeLists.txt
│
├── python-reference/
│   ├── farina_processing.py
│   ├── Harmon.csv
│   └── example_recordings/
```
---

## Future Work

- **On-device smoothing**: Implement Savitzky–Golay smoothing directly in C++.
- **Parametric EQ Application**: Apply calculated EQ filters in real time to audio playback.
- **UI Enhancements**: Add live histogram in android implementation.

---

## Summary

This project demonstrates end-to-end DSP pipeline development, beginning with a **Python prototype** and culminating in a **fully functional Android app** with native C++ processing. It highlights skills in DSP, cross-platform implementation, embedded math libraries, and mobile software integration — all validated against reference data.
