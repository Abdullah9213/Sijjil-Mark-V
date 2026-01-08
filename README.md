# 🛡️ Sijjil Mark-V: Industrial Edge-Defense System

[![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![YOLOv8](https://img.shields.io/badge/YOLOv8-00FFFF?style=for-the-badge&logo=yolo&logoColor=black)](https://github.com/ultralytics/ultralytics)


---

## 📖 Executive Summary

**Sijjil Mark-V** (codename: *The Interceptor*) is an edge-native perimeter defense appliance built for hostile environments (smog, fog, extreme heat). All inference runs locally on embedded Edge AI hardware to guarantee low latency and data sovereignty.

This repository contains the Inference Pipeline, Thermal Management scripts, and Radar–Vision Fusion logic for deployment on NVIDIA Jetson class devices.

---

## 🏗️ Physics-First Pivot — Root Cause Analysis

The Mark-IV field trials revealed three primary failure modes. Mark-V addresses these with materials, thermal and inference engineering.

| Failure Mode (Mark-IV) | Root Cause | Mark-V Intervention |
| :--- | :--- | :--- |
| System Blindness | Steel chassis acted as a Faraday cage, blocking mmWave radar. | Material switch to die-cast aluminum (ADC12) with a polycarbonate radar window. |
| Thermal Throttling | Sealed IP66 enclosure trapped heat; CPU throttled under load. | Passive cooling: chassis serves as a large heat-sink; CPU thermally coupled to shell. |
| Inference Lag | Full FP32 models on edge hardware caused latency spikes. | Quantized INT8 models using TensorRT for ~4x faster inference with minimal accuracy loss. |

---

## ⚙️ System Architecture

<img width="1408" height="768" alt="architecture" src="https://github.com/user-attachments/assets/0f47bf3e-4206-4383-a132-1ce60c11727a" />


### Performance Benchmarks (45°C test)

| Metric | Mark-IV (Steel) | Mark-V (Aluminum) | Improvement |
| :--- | :---: | :---: | :---: |
| Core Temp (Load) | 85°C (throttled) | 62°C (stable) | −23°C |
| Inference Speed | 12 FPS | 28 FPS | +133% |
| Radar Range | 0 m (blocked) | 150 m | Restored |
| False Positives | High (fog) | Low (radar-filtered) | More reliable |

---

## 🛠️ Installation & Setup

1. Prerequisites

- NVIDIA Jetson Nano / Orin Nano (JetPack 5.1+)
- Python 3.8+
- USB or CSI camera

2. Install repository and dependencies

```bash
git clone https://github.com/Abdullah9213/Sijjil-Mark-V.git
cd Sijjil-Mark-V
pip install -r requirements.txt
```

3. Run thermal monitor (background service)

This script monitors CPU temperature and reduces inference throughput to prevent hardware damage:

```bash
python scripts/thermal_monitor.py --limit 65
```

4. Run inference

```bash
python main.py --source 0 --model weights/yolov8n_int8.engine --conf 0.5
```

---

## 📂 Repository Structure

```
Sijjil-Mark-V/
├── models/
│   ├── yolov8n.pt          # PyTorch model for training
│   └── yolov8n.engine      # TensorRT engine for deployment
├── scripts/
│   ├── thermal_monitor.py  # Physics-aware throttling logic
│   └── radar_interface.py  # UART driver and data parser for mmWave sensor
├── hardware/
│   ├── chassis_cad.step    # 3D CAD of aluminum enclosure
│   └── thermal_sim.pdf     # Thermal simulation results
├── main.py                 # Core inference loop + fusion logic
└── requirements.txt
```



---

## ⚖️ Disclaimer

This project is intended for defensive perimeter security only. Ensure local regulatory compliance for radar frequency usage and deployment.

---

## 📫 Contact

Abdullah Ghaffar — Edge AI Specialist

- LinkedIn: ttps://www.linkedin.com/in/abdullah-ghaffar--
- Email: abdullah.gheffer@gmail.com

