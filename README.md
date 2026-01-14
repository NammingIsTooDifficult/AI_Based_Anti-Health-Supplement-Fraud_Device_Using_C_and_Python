<p align="center">
  <img src="https://img.shields.io/badge/Platform-ESP32-blueviolet?style=for-the-badge" />
  <img src="https://img.shields.io/badge/License-MIT-brightgreen?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Framework-Arduino-00979D?style=for-the-badge&logo=arduino" />
  <img src="https://img.shields.io/badge/Language-Python-3776AB?style=for-the-badge&logo=python" />
  <img src="https://img.shields.io/badge/Function-AI%20Detection-F7DF1E?style=for-the-badge" />
</p>

<h1 align="center">Elderly Health Product False Advertising Detection System</h1>
<p align="center">
  <b>✨ Portable AI Device | Offline Anti-Fraud Protection | Audio-Visual-Haptic Alerts</b>
</p>

---

<div align="center">
  <img src="https://img.shields.io/badge/Hardware-ESP32-3578E5?style=flat-square&logo=espressif" />
  <img src="https://img.shields.io/badge/Audio-I2S%20Mic-FF4500?style=flat-square" />
  <img src="https://img.shields.io/badge/AI-LLM%20Analysis-00C853?style=flat-square" />
  <img src="https://img.shields.io/badge/Alert-LED%2B Vibrator-FF6B6B?style=flat-square" />
</div>

---

## 📖 Project Overview
This project is a portable anti-fraud assistive device designed for elderly users.
Through a full pipeline of region monitoring → audio capture → AI content analysis → audio/visual/vibration alerts, the system helps elderly users quickly identify false advertising in offline scenarios (such as health product sales events), reducing the risk of fraud.


## 🚀 Workflow
1. 📍 The device automatically activates when entering a predefined high-risk area
2. 🎙️ Collects on-site conversation audio every 4 seconds
3. 📤 Transfers audio data to a computer via serial port
4. 🧠 The computer converts speech to text and uses AI to analyze content risk
5. ⚠️ If false advertising is detected: red LED + vibration. Safe scenario: green LED only.


## 🛠️ Hardware Components
- ESP32 development board (main controller)
- I2S microphone module (audio acquisition)
- WS2812 / external LED (status indication)
- Vibration motor (tactile alert)
- Power module (portable power supply)


## 🧩 Software Architecture
### Device Side (ESP32)
- Developed with Arduino framework
- Functions: audio capture, serial communication, LED & vibration control
- Dependency: `Adafruit_NeoPixel`


### Computer Side (Python)
- Functions: audio reception, speech-to-text (ASR), AI risk analysis, result feedback
- Dependencies: serial communication library, cloud ASR service, large language model API


## 📦 Installation & Configuration
### 1. Hardware Wiring (Pin Definition)
- I2S_SCK_PIN → 14
- I2S_WS_PIN → 15
- I2S_SD_PIN → 12
- WS2812_PIN → 48
- External LED_PIN → 5
- Vibration Motor_PIN → 2


### 2. Device Configuration
1. Install Arduino IDE and add ESP32 board support
2. Install dependency: `Adafruit_NeoPixel`
3. Upload `main.cpp` to ESP32


### 3. Computer Configuration
1. Install Python 3.6+
2. Install dependencies:
```bash
pip install serial requests tencentcloud-sdk-python
```

3. Configure keys in `esp32_audio_ai.py`:
- Serial port: modify `ser = serial.Serial('COM3', 115200)` to your actual port (Windows uses COM ports, Mac/Linux use `/dev/ttyUSB0`, etc.)
- Cloud ASR credentials: fill in `TENCENT_SECRET_ID`, `TENCENT_SECRET_KEY`
- LLM API credentials: fill in `DOUBAO_API_KEY`, `DOUBAO_ENDPOINT`


## 📌 Usage
1. Connect ESP32 to the computer via USB
2. Power on the ESP32 device
3. Run the computer script:
```bash
python esp32_audio_ai.py
```
4. The device enters monitoring mode automatically:
- Safe scenario: green LED, no vibration
- Risk scenario: red LED + vibration motor activated for 5 seconds

## 🔍 False Advertising Detection Features
The AI will classify a conversation as risky if two or more of the following are detected:
- Claims of “curing diseases” or “replacing medical treatment”
- Exaggerated effects (e.g., “life extension”, “miracle cure”, “instant recovery”)
- Urgency-based manipulation (e.g., “limited-time offer”, “buy now or price rises tomorrow”)
- Claims of “exclusive formula”, “secret remedy”, or “internal channels”

## ⚠️ Notes
1. This device is an assistive reminder tool; final decisions should be made based on real-world judgment
2. Cloud ASR services and LLM APIs may incur fees. Please refer to the respective platform pricing
3. If the device is unresponsive, check the serial port configuration and hardware wiring
4. For long-term use, it is recommended to power the ESP32 with a portable power bank
