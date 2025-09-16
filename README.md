# Heart-Rate Detection (Hearth-Rate-Detection)

A project to detect heart rate using a PPG sensor and an ESP32 microcontroller. The signal processing uses a modified Pan-Tompkins algorithm.  

---

## 📋 Overview

- Uses **PPG sensor** to collect optical pulse data.  
- ESP32 microcontroller is used for capturing the sensor readings.  
- Signal processing done in software (Python) using a modified Pan-Tompkins algorithm (originally for ECG) to detect peaks corresponding to heart beats.  
- A GUI component (`ECG_GUI.py`) for visualizing the waveform and detected beats.  

---

## 🔧 Components & Files

| File / Folder | Purpose |
|---------------|---------|
| `ESP32_readingCode` | Code for the ESP32 to read from the PPG sensor and send data to host. |
| `PT.py` | Pan-Tompkins based processing: filtering, peak detection, beat-interval calculations, etc. |
| `ECG_GUI.py` | Graphical interface to display the live/recorded signals, overlay detected beats, show heart rate. |
| `.gitignore` | Standard ignores (compiled files, caches, etc.). |

---

## 🛠 Dependencies

- Python 3.x  
- Python libraries: likely `numpy`, `scipy`, `matplotlib` (for plotting / GUI), maybe `pyserial` or similar to receive data from ESP32.  
- ESP32 toolchain (Arduino IDE, PlatformIO, etc.) or whatever is used to compile/upload the MCU code.  
- Hardware: PPG sensor (photoplethysmography sensor), cabling, ESP32 board.

---

## 🚀 Setup & Usage

1. **Hardware Setup**  
   - Connect the PPG sensor to the ESP32 following the pinout in the ESP32 reading code.  
   - Power sensor and ESP32 appropriately.

2. **ESP32 Code Upload**  
   - Open `ESP32_readingCode` in your MCU development environment.  
   - Configure correct board and pins.  
   - Upload to ESP32.

3. **Python Side Setup**  
   - Clone this repo:  
     ```bash
     git clone https://github.com/VuKe77/Hearth-rate-detection.git
     cd Hearth-rate-detection
     ```
   - Create a Python virtual environment (optional but recommended):  
     ```bash
     python3 -m venv venv
     source venv/bin/activate     # or Windows equivalent
     ```
   - Install required Python packages. For example:
     ```bash
     pip install numpy scipy matplotlib pyserial
     ```
     (Add/remove packages depending on what the GUI / processing scripts import.)

4. **Run the Signal Processing & GUI**  
   - With ESP32 sending data to your computer (via serial, WiFi, etc., depending on implementation), launch `ECG_GUI.py`  
     ```bash
     python ECG_GUI.py
     ```
   - The GUI should show the waveform, mark detected peaks, and compute/display heart rate.

---

## ⚠️ Troubleshooting & Tips

- **No/garbled data from ESP32**  
  - Check serial connection / baud rate.  
  - Ensure sensor is connected correctly and receiving power.  

- **Poor signal / noise**  
  - Make sure the PPG sensor is properly placed and stable.  
  - Minimize ambient light interference.  

- **False or missed peaks**  
  - Adjust thresholds in `PT.py`.  
  - Tune filter parameters (bandpass, smoothing) to match your setup.  

- **GUI doesn’t display / stalls**  
  - Check that required Python libraries are installed.  
  - Ensure GUI script is receiving data; might need to mock input if ESP32 not hooked up yet.

---

## 🎯 Possible Improvements

- Improve peak detection robustness (adaptive thresholds, machine learning methods).  
- Add logging of heart rate over time / history.  
- Support wireless data transfer (WiFi, Bluetooth).  
- Build mobile / web frontend for visualization.  
