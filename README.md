# Dual-Stream Spatial-Frequency Network for Data-Efficient Deepfake Detection

## 📌 Abstract
Detecting deepfakes typically requires massive datasets. In this project, we address the challenge of **"low-data" detection** (using only 5% of the training data). We propose a novel **Dual-Stream Network** that fuses:
1.  **Spatial Stream:** An Xception backbone analyzing RGB data.
2.  **Frequency Stream:** A custom CNN analyzing the Discrete Cosine Transform (DCT) to detect high-frequency artifacts invisible to the naked eye.

This architecture achieves **93.01% Accuracy** and **0.9725 AUC**, significantly outperforming a standard Xception baseline and aggressive augmentation techniques like CutMix.

## 📊 Key Results

| Model | Technique | Test Accuracy | Test AUC | Observation |
| :--- | :--- | :---: | :---: | :--- |
| **Baseline** | Xception (Transfer Learning) | 92.46% | - | Strong baseline. |
| **Method 1** | Xception + CutMix | 87.87% | 0.9379 | **Performance Drop.** Proved the model was signal-starved, not overfit. |
| **Method 2 (Ours)** | **Dual-Stream (Spatial+Freq)** | **93.01%** | **0.9725** | **SOTA Performance.** Frequency domain adds critical signal. |
| **Ensemble** | 5-Fold Average | 91.91% | 0.9696 | High variance in low-data regimes suggests single-best model deployment. |

## 🧠 Architecture
The model processes the image in two domains simultaneously:
- **RGB Input** -> Xception -> Global Average Pooling
- **DCT (Frequency) Input** -> Log-Scale Transformation -> Custom CNN -> Global Average Pooling
- **Fusion** -> Concatenation -> Dense Layers -> Sigmoid

## 📂 Dataset
We used the **Deepfake and Real Images** dataset from Kaggle.
- **Constraint:** Only the first **5%** of the dataset was used to simulate a data-scarce environment (approx 7,000 training images).
- **Preprocessing:** Faces were cropped using MTCNN with 20% padding.

## 🚀 How to Run
1. Open `02_Proposed_Dual_Stream_Network.ipynb` in Google Colab.
2. Upload your `kaggle.json` key.
3. Run the cells to download the dataset, preprocess images, and train the dual-stream model.

## 🏆 Contribution
This project demonstrates that in low-data regimes, **adding a new signal modality (Frequency)** is more effective than regularization techniques (Augmentation) for Deepfake detection.

## 🛡️ License & Citation

The code in this repository is licensed under the MIT License. 
If you use this code or model in your research, **you must cite the following:**

> V, Karthik. (2025). "Dual-Stream Spatial-Frequency Network for Data-Efficient Deepfake Detection." GitHub Repository. https://github.com/YourUsername/Dual-Stream-Deepfake-Detection
