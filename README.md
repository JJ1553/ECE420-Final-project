# Parametric Equalizer (ECE420 Final Project)

## Overview  
This project was developed as the final project for **ECE420: Digital Signal Processing Laboratory** at the University of Illinois Urbana–Champaign.  

The application records live audio on an Android device, saves it as a `.wav` file, and applies **real-time parametric equalization** with optional **AutoEQ filter generation** for headphone and speaker compensation.  

This project demonstrates the integration of multiple software layers and cross-domain expertise in **DSP, mobile development, and systems integration**:  
- **Android UI (Java/XML)**: Activity lifecycle, file handling, and user interface control.  
- **Native DSP (C++/NDK)**: Low-latency digital filter processing with IIR biquads.  
- **Python (Chaquopy integration)**: AutoEQ and scientific computation stack (NumPy, SciPy, Matplotlib).  
- **Systems Integration**: JNI bridging, Gradle and Chaquopy dependency management, ABI compatibility, and cross-language debugging.  

---

## Key Features
- **Live Audio Recording**: Captures microphone input and stores high-quality `.wav` files.  
- **Real-Time Equalization**: Implements parametric EQ using biquad filters in a C++ DSP engine.  
- **AutoEQ Integration**:  
  - Executes on-device via Python using the Chaquopy framework.  
  - Generates parametric EQ filters for specific headphones or speakers.  
  - Applies correction curves seamlessly to the playback pipeline.  
- **Cross-Language Architecture**:  
  - Java for Android lifecycle and UI.  
  - JNI bridge to C++ for real-time DSP.  
  - Python for AutoEQ filter design and analysis.  

---

## Technical Highlights

### Android (Java/XML)  
- Built with `AudioRecord` for raw PCM capture.  
- Manages runtime permissions (`RECORD_AUDIO`, storage).  
- Handles activity lifecycle gracefully (`onPause`, `onStop`, `onDestroy`) to release audio resources.  

### DSP Core (C++ with NDK)  
- Implements biquad IIR filters for parametric EQ.  
- Optimized for low-latency execution on ARM-based processors.  
- Compiled with CMake and Android NDK to support multiple ABIs (`arm64-v8a`, `x86`, `armeabi-v7a`).  

### Python Integration (Chaquopy)  
- Integrated scientific stack: **NumPy, SciPy, Pandas, Matplotlib**.  
- AutoEQ v4.1.2 included for automatic filter generation.  
- Filter coefficients generated in Python and passed into the native DSP engine.  
- Resolved missing dependencies and `.so` libraries (`libopenblas.so`, `libgfortran.so`, `libjpeg_chaquopy.so`) through manual wheel analysis and dependency patching.  
- Demonstrated expertise in ABI handling and library debugging within a constrained Android environment.  

---

## Skills Demonstrated
- **Digital Signal Processing**: Real-time IIR parametric EQ design and implementation.  
- **Cross-Language Development**: Seamless integration of Java, C++, and Python in a single Android app.  
- **System-Level Debugging**:  
  - Resolved Gradle and Chaquopy dependency mismatches.  
  - Identified and patched missing shared libraries in Android builds.  
  - Managed multi-architecture NDK builds.  
  - Debugged runtime loading errors (`dlopen` failures).  
- **Mobile Systems Engineering**: Designed a complete pipeline from user interface → DSP engine → AutoEQ integration.  
- **Engineering Trade-offs**: Evaluated spectrogram visualization but prioritized AutoEQ integration to maximize DSP impact.  

---

## Project Structure
app/src/main/java/com/ece420_parametric_eq/
│   start_page.java          # Recording and navigation logic
│   ProcessActivity.java     # EQ application and AutoEQ processing
│   DSPProcessor.java        # JNI bridge for C++ DSP
│
app/src/main/cpp/
│   dsp_native.cpp           # Core DSP (biquad filters, EQ engine)
│
app/src/main/python/
│   autoeq_wrapper.py        # Runs AutoEQ and passes filters to Android
│
res/layout/
│   start_page.xml           # Android layout definitions
---

## Lessons Learned
- Achieving **low-latency DSP** on mobile requires careful design and native implementation.  
- Python integration on Android requires navigating **complex ABI and dependency mismatches**.  
- JNI bridging, while powerful, requires careful management of memory and thread safety.  
- Engineering trade-offs between visualization features and real-time DSP performance are critical in mobile DSP applications.  

---

## Context
This project was completed as the **capstone final project** for **ECE420** at UIUC. It highlights:  
- Practical application of DSP theory in a mobile environment.  
- Real-world system integration across multiple languages.  
- Application of open-source DSP research tools (AutoEQ) into embedded/mobile contexts.  

---

## Future Work
- Add real-time visualization (spectrograms, frequency response).  
- Extend equalization to multiband presets and user-defined profiles.  
- Package as a publicly available Android app.  

---

## Author
**Josh Jenks**  
Computer Engineering, University of Illinois Urbana–Champaign  
Focus: Embedded Systems, DSP, and Android Development  
