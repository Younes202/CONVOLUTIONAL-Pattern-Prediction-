# Financial Pattern Recognition CNN: Comparative Study

This project implements a **Convolutional Neural Network (CNN)** to classify financial market patterns (**Bullish/Bearish**) using image data. It evolved from a **basic research model** to an **optimized version designed for quantitative analysis**.

---

## 📊 Dataset Overview

- **Total Images:** 1,644  
- **Training Set:** 1,281 images  
- **Validation Set:** 363 images  
- **Image Resolution:** 250 × 250 pixels (RGB)  
- **Classes:**  
  - `Down` (Bearish)  
  - `Up` (Bullish)

---

## 🛠 Model Evolution

### Version 1: Initial Research Model (Baseline)

This version focused on **basic feature extraction** but suffered from **severe overfitting**.

**Architecture**
- 3 Convolutional layers  
  - 16 filters  
  - 32 filters  
  - 64 filters  
- Followed by a **Dense 512-neuron head**

**Optimizer**
- RMSprop

**Performance**
- **Training Accuracy:** 92.74%  
- **Validation Accuracy:** 56%

**Key Issue**

The model failed to **generalize**, effectively guessing the majority class (**"Down"**) for all unseen data, resulting in a **0.00 recall for the "Up" class**.

---

### Version 2: Optimized Quant Model (Current)

This version introduced several **regularization and stabilization techniques** to force the model to learn **actual market signals rather than memorizing noise**.

#### Key Enhancements

- **Data Augmentation**
  - `RandomFlip`
  - `RandomRotation`
  - `RandomZoom`

- **BatchNormalization**
  - Integrated after each `Conv2D` layer to stabilize gradients and speed up convergence.

- **L2 Regularization**
  - Applied to Dense layers to penalize overly complex weights.

- **Adam Optimizer**
  - Learning rate set to **0.0001** to help the model escape local minima.

- **EarlyStopping**
  - Monitors `val_loss`
  - Restores the best performing weights.

---

## 📈 Final Performance (Unseen Data)

- **Overall Accuracy:** 61%  
- **Precision (Up Class):** 69%  
- **Recall (Up Class):** 0.23  

This indicates the model **successfully identified bullish signals for the first time**.

---

## 📈 Analysis of Results

The transition from **Version 1** to **Version 2** moved the model from a **"biased guesser"** to a **"statistically significant filter."**

While the overall accuracy is **61%**, the **69% Precision** on `"Up"` predictions indicates that the model provides a **reliable signal when it identifies a bullish pattern**.

The **low recall (0.23)** suggests the model is **highly conservative**—only predicting `"Up"` when it is extremely certain.  

This behavior is often **preferred in quantitative trading**, as it helps **avoid false positives**.

---
