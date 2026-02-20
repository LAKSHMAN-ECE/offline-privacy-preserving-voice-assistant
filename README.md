# Offline, Privacy-Preserving Hindi Voice Assistant on Raspberry Pi

**Team:** IDEA IGNITERS  
**Problem Statement:** 1  
**Platform:** Raspberry Pi 5  
**Toolchain:** Python 3, Vosk ASR, Piper TTS, GPIOZero, sounddevice

---

## 1. Project Overview

This project presents the design, implementation, optimization, and validation of an **offline, privacy-preserving Hindi voice assistant** deployed on the Raspberry Pi 5 platform.

**Hardware Platform:**

* Quad-core ARM Cortex-A76 CPU (2.4 GHz)
* 4GB RAM
* USB microphone and speaker
* GPIO interfaces for hardware control (LEDs,  RTC module)

**Objective:**

* Enable **real-time speech recognition and synthesis** for Hindi commands entirely offline.
* Preserve user privacy.
* Provide control over local hardware devices.

**Performance:**

* Achieves **sub-second response times**.
* Supports **10–15 Hindi commands**.

---

## 2. System Architecture

The system follows a **modular edge AI methodology**, combining audio capture, offline ASR, intent recognition, and TTS in a fully local environment.

**Processing System Responsibilities (Raspberry Pi CPU):**

* Audio acquisition from USB microphone
* Resampling to 16 kHz for ASR
* Audio streaming to Vosk ASR model
* Intent detection via Python keyword matching and logic
* GPIO control for hardware devices
* Text-to-speech generation via Piper TTS
* Session management (wake word detection, silence and active timeouts)

**Data Movement:**

* Microphone input → audio buffer → ASR → intent → TTS output → speaker
* Wake-word detection keeps CPU idle until triggered
* Optional RTC module provides accurate local time

---

## 3. Speech Recognition Module

* Uses **Vosk offline ASR** with Hindi acoustic model
* Audio captured at **48 kHz**, downsampled to **16 kHz**
* Provides **real-time speech-to-text conversion**
* Detects pre-defined Hindi commands (e.g., “सुनो,” “समय बताओ”)
* JSON output passed to **intent detection** module

---

## 4. Text-to-Speech Module

* Implemented with **Piper TTS** using ONNX Hindi voice model
* Converts text response to **natural-sounding Hindi speech**
* Generates WAV audio output played through the speaker
* Fully offline with **low-latency playback**

---

## 5. Wake Word Detection Mechanism

* Continuously listens for **wake words**: “सुनो,” “सुनो जी”
* Once detected, transitions system from **sleep mode to active mode**
* Prevents unnecessary CPU load during idle periods
* Supports **SILENCE_TIMEOUT** (1.5 s) and **ACTIVE_TIMEOUT** (30 s)

---

## 6. Intent Detection and Command Processing

* Rule-based **keyword matching** implemented in Python
* Supported commands include:

  * Time and date queries
  * Greetings and personalized responses
  * Jokes and casual conversation
  * Simple calculations
  * Hardware control (LED ON/OFF)
* Ensures **fast, predictable command execution**

---

## 7. User Personalization and Data Storage


* Allows personalization (e.g., setting user name)
* Data never leaves the device, ensuring **complete privacy**
* Supports persistent configuration across sessions

---

## 8. Real-Time Clock (RTC) Integration

* Optional **DS3231 RTC module** integrated
* Provides accurate **offline time and date**
* Enables time-based queries even without network connectivity

---

## 9. GPIO and Hardware Control

* LED connected to **GPIO17** for demonstration
* **GPIOZero library** used for safe and efficient hardware control
* Voice commands can **turn LEDs ON/OFF** and extend to other IoT devices

---

## 10. Privacy and Security Architecture

* Fully offline processing: **no cloud or external server required**
* Audio data never leaves the Raspberry Pi
* Local storage for user preferences ensures **data confidentiality**
* No personal data is transmitted over the network

---

## 11. Performance Evaluation

| Metric                   | Value      | Notes                                |
| ------------------------ | ---------- | ------------------------------------ |
| Median Response Time     | ~0.5–1.0 s | Sub-second response achieved         |
| Command Accuracy         | >90%       | For 10–15 Hindi commands             |
| CPU Load                 | Moderate   | Efficient queue-based audio handling |
| Hardware Control Latency | <200 ms    | LED ON/OFF execution time            |

* Performance meets **Problem Statement 1 requirements**
* Fully offline operation ensures **robustness**

---

## 12. Testing and Validation

* Commands tested in multiple sessions with variable pronunciation and background noise
* Wake word detection tested continuously over extended periods
* Hardware control verified using GPIO outputs (LED)
* TTS output validated for **clarity and pronunciation of Hindi**

---

## 13. Applications

* Home automation with voice-controlled devices
* Educational tools for Hindi-speaking users
* Privacy-sensitive environments (labs, offices)
* Edge AI demonstration for embedded AI systems

---

## 14. Challenges and Limitations

* Ensuring robust Hindi speech recognition for diverse accents
* Maintaining low-latency on limited Raspberry Pi CPU
* Integrating TTS with minimal lag
* Wake word mis-detection under noisy conditions
* Limited number of pre-defined commands

---

## 15. Future Enhancements

* Expand command set with NLP-based intent recognition
* Support multiple languages (e.g., English + Hindi)
* Integrate additional IoT devices (fans, relays, sensors)
* Optimize CPU usage using multi-threading or small accelerators
* Improve offline TTS naturalness with advanced models

---

## 16. Conclusion

This project demonstrates a fully **offline, privacy-preserving Hindi voice assistant** deployed on Raspberry Pi 5.

* Real-time command recognition and voice responses achieved
* User data remains **secure and local**
* Hardware control verified with GPIO devices
  
