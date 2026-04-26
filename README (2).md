# Skin Cancer Classification Using Deep Learning (CNN)

> **Note:** This is an academic project completed in **2023–2024** as part of a university course at **Tishreen University – Faculty of Informatics Engineering**, Department of Artificial Intelligence. The code reflects the state of the project at that time and is shared here for educational and portfolio purposes. It is not actively maintained.

---

## Overview

This project aims to classify multiple types of skin cancer from dermoscopic images using **Convolutional Neural Networks (CNN)**. The model was trained on the **HAM10000** dataset and compares different training configurations (optimizers, loss functions, epochs) to find the best-performing approach.

---

## Dataset

**HAM10000 (Human Against Machine with 10000 training images)**

| Property | Details |
|---|---|
| Source | [Kaggle – Skin Cancer MNIST: HAM10000](https://www.kaggle.com/kmader/skin-cancer-mnist-ham10000) |
| Total Images | 10,015 dermoscopic images |
| Image Format | JPEG (600×450 px) |
| Classes | 7 skin lesion categories |
| Released | 2021, by ViDIR Group – Medical University of Vienna & University of Queensland |

### Classes (7 Categories)

| Label | Description |
|---|---|
| `akiec` | Actinic Keratoses / Intraepithelial Carcinoma (Bowen's disease) |
| `bcc` | Basal Cell Carcinoma |
| `bkl` | Benign Keratosis-like Lesions (Solar Lentigines, Seborrheic Keratoses, Lichen Planus-like) |
| `df` | Dermatofibroma |
| `mel` | Melanoma |
| `nv` | Melanocytic Nevi |
| `vasc` | Vascular Lesions (Angiomas, Angiokeratomas, Pyogenic Granulomas, Hemorrhage) |

---

## Model Architecture

A **Sequential CNN** with 12 layers:

```
Input → [Conv2D → relu] * 2 → MaxPool2D → Dropout →
        [Conv2D → relu] * 2 → MaxPool2D → Dropout →
        Flatten → Dense → Dropout → Output (Softmax)
```

Key components:
- **Conv2D layers** – Extract spatial features (32 filters for early layers, 64 for deeper)
- **MaxPooling2D** – Reduce spatial dimensions and computational cost
- **Dropout** – Regularization to reduce overfitting
- **Dense + Softmax** – Final classification across 7 categories

---

## Training Configuration

| Parameter | Value |
|---|---|
| Epochs | 50 / 100 |
| Batch Size | 10 |
| Optimizer (best) | Adam |
| Loss Function | `categorical_crossentropy` |
| Metric | Accuracy |
| Platform | Kaggle Notebooks |

**Data Augmentation applied:**
- Random rotation (±10°)
- Random zoom (10%)
- Horizontal & vertical shift (10%)

---

## Results & Experiments

### Experiment 1 vs 2 — Optimizer Comparison (Adam vs Lion)

| | Exp 1 (Adam) | Exp 2 (Lion) |
|---|---|---|
| Training Accuracy | 74.58% | 66.18% |
| Validation Accuracy | 73.56% | 65.46% |
| Test Accuracy | **74.48%** | 65.90% |

### Experiment 3 vs 1 — Loss Function Comparison (50 epochs)

| | Binary CE | Categorical CE |
|---|---|---|
| Training Accuracy | 73.49% | 74.58% |
| Validation Accuracy | 71.44% | 73.56% |
| Test Accuracy | 73.04% | **74.48%** |

### Experiment 3 vs 1 — Loss Function Comparison (100 epochs)

| | Binary CE | Categorical CE |
|---|---|---|
| Training Accuracy | 76.55% | 76.14% |
| Validation Accuracy | 75.23% | 76.09% |
| Test Accuracy | **76.18%** | 74.68% |

> **Best Model:** Adam optimizer + `categorical_crossentropy` + 50 epochs → **74.48% test accuracy**

---

## Tech Stack

| Tool | Purpose |
|---|---|
| Python | Primary language |
| TensorFlow / Keras | Model building & training |
| NumPy & Pandas | Data manipulation |
| Matplotlib & Seaborn | Visualization |
| PIL (Pillow) | Image processing |
| Kaggle Notebooks | Training environment |

---

## How to Run

1. **Clone the repository**
   ```bash
   git clone https://github.com/dagher-h/skin-cancer-classification.git
   cd skin-cancer-classification
   ```

2. **Install dependencies**
   ```bash
   pip install tensorflow keras numpy pandas matplotlib seaborn pillow
   ```

3. **Download the dataset**
   - Go to [HAM10000 on Kaggle](https://www.kaggle.com/kmader/skin-cancer-mnist-ham10000)
   - Download and place the data in a `/data` folder

4. **Run the notebook**
   ```bash
   jupyter notebook project.ipynb
   ```

---

## Project Structure

```
skin-cancer-classification/
│
├── project.ipynb          # Main training notebook
├── README.md              # This file
└── data/                  # Place HAM10000 dataset here (not included)
```

---

## References

1. Esteva et al. – *Dermatologist-level classification of skin cancer with deep neural networks*, Nature 2017
2. Bevan & Atapour-Abarghouei – *Detecting Melanoma Fairly*, 2022
3. Benčević et al. – *Understanding skin color bias in deep learning-based skin lesion segmentation*, 2024
4. Kushimo et al. – *Deep learning model to improve melanoma detection in people of color*, 2023
5. [Convolutional Neural Network – TechTarget](https://www.techtarget.com/searchenterpriseai/definition/convolutional-neural-network)
6. [HAM10000 Dataset – Kaggle](https://www.kaggle.com/kmader/skin-cancer-mnist-ham10000)
7. [Skin Lesion Classification Using Deep CNNs – Medium](https://medium.com/@sid321axn/skin-lesion-classification-using-deep-cnns-a-step-wise-approach-347d47868196)
8. [Lion Optimizer – Keras](https://keras.io/api/optimizers/lion/)

---

## Academic Context

| Field | Details |
|---|---|
| University | Tishreen University, Syria |
| Faculty | Faculty of Informatics Engineering |
| Department | Artificial Intelligence |
| Supervisor | Dr. Hala Nassar |
| Academic Year | 2023–2024 |
| Project Type | Semester Project |

---

## Disclaimer

This project was built for **academic learning purposes only**. It should **not** be used as a substitute for professional medical diagnosis. Results are experimental and the model has not been clinically validated.

---

## License

This project is open for educational use. Please credit the original authors if you use or build upon this work.
