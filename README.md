# TumorNet
Automated tumor detection and classification system built with CNN for early diagnosis support. Leveraging deep learning (CNN) to detect tumors and classify their types from medical images.
# 🧠 TumorNet — Brain Tumor Detection & Classification using CNN

> CNN-based deep learning model for tumor detection and multi-class classification from medical MRI images.

---

## 📌 Overview

This project uses a **Convolutional Neural Network (CNN)** to automatically detect and classify brain tumors from MRI scan images. The model is trained to identify four categories:

- 🔴 **Glioma**
- 🟠 **Meningioma**
- 🟡 **Pituitary Tumor**
- 🟢 **No Tumor**

Early and accurate tumor classification can assist radiologists and support faster clinical decision-making.

---

## 📂 Dataset

| Detail | Info |
|---|---|
| **Source** | [Brain Tumor MRI Dataset — Kaggle](https://www.kaggle.com/datasets/masoudnickparvar/brain-tumor-mri-dataset) |
| **Classes** | Glioma, Meningioma, Pituitary, No Tumor |
| **Format** | MRI scan images (JPG/PNG) |
| **Split** | Training / Validation / Testing |

---

## 🏗️ Model Architecture

- Input Layer — MRI image (resized to fixed dimensions)
- Multiple **Conv2D + MaxPooling** layers for feature extraction
- **Flatten** → **Dense** layers for classification
- Output Layer — **Softmax** (4 classes)
- Optimizer: **Adam**
- Loss: **Categorical Crossentropy**

---

## 🚀 How to Run

### 1. Clone the repository
```bash
git clone https://github.com/your-username/tumor-detection-cnn.git
cd tumor-detection-cnn
```

### 2. Install dependencies
```bash
pip install -r requirements.txt
```

### 3. Download the dataset
Download from [Kaggle](https://www.kaggle.com/datasets/masoudnickparvar/brain-tumor-mri-dataset) and place it in the `data/` folder:
```
data/
├── Training/
│   ├── glioma/
│   ├── meningioma/
│   ├── pituitary/
│   └── notumor/
└── Testing/
    ├── glioma/
    ├── meningioma/
    ├── pituitary/
    └── notumor/
```

### 4. Train the model
```bash
python train.py
```

### 5. Evaluate / Predict
```bash
python predict.py --image path/to/mri_image.jpg
```

---

## ⚠️ Difficulties Faced & Solutions

### 1. 🔥 Overfitting

**Problem:**
The model performed very well on training data but poorly on validation data. Training accuracy kept rising while validation accuracy plateaued or dropped — a classic sign of overfitting.

**What caused it:**
- CNN model was too deep/complex for the dataset size
- Model was memorizing training images instead of learning general patterns

**Solutions applied:**
- ✅ Added **Dropout layers** (rate: 0.4–0.5) after Dense layers to randomly disable neurons during training
- ✅ Applied **Data Augmentation** (rotation, flipping, zoom, brightness shift) using `ImageDataGenerator` to artificially expand the training set
- ✅ Used **Early Stopping** callback to halt training when validation loss stopped improving
- ✅ Added **L2 Regularization** to penalize large weights
- ✅ Reduced model complexity by removing excess Conv layers

---

### 2. 🗂️ Dataset Preprocessing Issues

**Problem:**
Raw MRI images from Kaggle were inconsistent — different sizes, aspect ratios, and some with noise or artifacts. Feeding them directly into the CNN caused shape errors and poor learning.

**What caused it:**
- Images were not uniform in dimensions
- Some images had irrelevant borders/text overlays
- Pixel values were in range 0–255 (not normalized)

**Solutions applied:**
- ✅ Resized all images to a fixed size (e.g., `224x224`) using OpenCV/PIL
- ✅ Normalized pixel values to `[0, 1]` by dividing by 255
- ✅ Used `ImageDataGenerator` with `rescale=1./255` for automatic normalization
- ✅ Applied grayscale conversion where needed to reduce noise
- ✅ Verified dataset folder structure to ensure correct class labeling

---

## 📊 Results

| Metric | Score |
|---|---|
| Training Accuracy | ~99.47% |
| Test Accuracy | ~95% |

> 📝 Update the table above with your actual model results after training.

---

## 🛠️ Tech Stack

- **Language:** Python
- **Deep Learning:** TensorFlow / Keras
- **Image Processing:** OpenCV, PIL
- **Data Handling:** NumPy, Pandas
  

---

## 📁 Project Structure

```
tumor-detection-cnn/
│
├── data/                  # Dataset (not included, download from Kaggle)
├── models/                # Saved model files (.h5 / .pkl)
├── notebooks/             # Jupyter notebooks for EDA & training
├── train.py               # Model training script
├── predict.py             # Inference script
├── requirements.txt       # Python dependencies
└── README.md              # Project documentation
```

---

## 🔮 Future Improvements

- [ ] Try **Transfer Learning** with VGG16 / ResNet50 for better accuracy
- [ ] Build a simple **web app** using Streamlit for live predictions
- [ ] Extend to detect more tumor types
- [ ] Add **Grad-CAM** visualization to highlight tumor regions in MRI

---

## 🙏 Acknowledgements

- Dataset: [Kaggle — Brain Tumor MRI Dataset](https://www.kaggle.com/datasets/masoudnickparvar/brain-tumor-mri-dataset)
- Inspired by medical imaging research in deep learning

---


