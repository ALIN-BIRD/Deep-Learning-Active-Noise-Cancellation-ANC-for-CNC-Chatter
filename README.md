# 🔇 Deep Learning Active Noise Cancellation (ANC) for CNC Chatter

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![PyTorch](https://img.shields.io/badge/PyTorch-Deep%20Learning-red)
![Simulink](https://img.shields.io/badge/MATLAB-Simulink-orange)
![Status](https://img.shields.io/badge/Status-Prototype-success)

### 📉 Result: Achieved ~10.60 dB Noise Reduction on Synthetic Data

## 📝 Abstract
This project implements an **Active Noise Cancellation (ANC)** system designed to suppress **Regenerative Chatter** in high-speed CNC milling machines. 

Unlike standard noise (which is random), Chatter is a self-excited vibration caused by the interaction between the tool and the workpiece. I created a **Digital Twin** in Simulink to simulate this physics phenomenon and trained an **LSTM (Long Short-Term Memory)** Neural Network to predict and cancel the vibration in real-time.

## ⚙️ The Pipeline

### 1. Physics Simulation (Simulink)
Modeled a **Single Degree of Freedom (SDOF)** Orthogonal Cutting process.
* **Core Physics:** Mass-Spring-Damper system.
* **The Killer Feature:** Implemented **Regenerative Feedback** using Transport Delay blocks ($y(t) - y(t-\tau)$) to mimic the tool hitting its own past cut.
* **Output:** Generated "Exploding" vibration datasets where the tool transitions from stable cutting to chaotic oscillation.

### 2. The AI Model (PyTorch)
* **Architecture:** Stacked LSTM (3 Layers, 256 Hidden Units).
* **Input:** Raw vibration displacement (Time Series).
* **Objective:** Predict the next vibration step ($t+1$) to generate an inverted "Anti-Noise" signal.
* **Optimization:** Trained on Google Colab T4 GPU using MSE Loss and Adam Optimizer.

## 📊 Results

The model successfully learned the exponential growth pattern of the chatter.

| Metric | Value |
| :--- | :--- |
| **Original Noise Power** | High (Unstable) |
| **Residual Noise Power** | Low (Stabilized) |
| **Attenuation Achieved** | **10.60 dB** |

*(Insert your graph image here - The one with the Green Line)*

## 🚀 How to Run

1.  **Generate Data:**
    * Open `CNC_Chatter_Model.slx` in MATLAB/Simulink.
    * Run the simulation to generate `cnc_chatter.csv`.
2.  **Train the AI:**
    * Open `Train_ANC.ipynb` in Google Colab.
    * Upload your CSV file.
    * Run all cells to train the LSTM and visualize the noise reduction.

## 🔮 Future Improvements
* Implement **Phase Error Correction** to improve reduction beyond 15 dB.
* Test on **Real-World Audio** (converting .wav files to CSV).
* Deploy the model to an **Edge Device** (Raspberry Pi/Jetson Nano) for real-time inference.

---
*Built by [Jeevan D P] - 2nd Year Electrical Engineering Student*
