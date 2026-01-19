# Deep Learning for Cheque Authenticity Verification (PyTorch)

## Overview
This project presents a deep learning–based approach to verify the authenticity of bank cheques using computer vision.  
The model is trained to differentiate between **genuine cheques** and **tampered (fake) cheques** by learning visual fraud patterns from cheque images.

Since publicly available datasets rarely contain labeled fake cheques, this work adopts a **synthetic forgery generation strategy**, which is commonly used in real-world fraud detection systems.

---

## Dataset
**Source:** Cheque Detection Dataset (Kaggle)

- Contains scanned bank cheque images
- Originally designed for object detection tasks
- Includes `.jpg` images and corresponding `.txt` annotation files

### Data Handling
- Only image files (`.jpg`, `.png`) are used
- Annotation files are ignored
- Original cheque images are treated as **REAL**
- Synthetic transformations are applied to generate **FAKE** samples

---

## Synthetic Forgery Strategy
To simulate real-world cheque fraud, synthetic fake samples are generated using image-level tampering such as:

- Localized blackouts (simulating overwritten fields)
- Gaussian blur (re-scan artifacts)
- Noise injection
- Contrast and color distortions

This allows the model to learn **tampering patterns** rather than memorizing document templates.

---

## Model Architecture
- Backbone: **ResNet-18 (ImageNet pretrained)**
- Framework: **PyTorch**
- Task: **Binary classification (REAL vs FAKE)**
- Input size: `224 × 224 RGB`

The final fully connected layer is replaced to support binary classification.

---

## Training Details
- Loss Function: Cross-Entropy Loss
- Optimizer: AdamW
- Batch Size: 16
- Epochs: 5
- Device: GPU (if available)

Training shows a **stable and monotonic loss decrease**, indicating effective learning without overfitting.

---

## Inference
The trained model supports inference on:
- Any cheque image from the dataset
- New cheque images added to the Kaggle input directory

The output includes:
- Predicted label: `REAL` or `FAKE`
- Confidence score
- Visualization of the input image

---

## Results
- Training loss decreased steadily across epochs
- Model successfully distinguishes original cheques from synthetically tampered ones
- Demonstrates strong qualitative separation between REAL and FAKE samples

⚠️ Note:  
This model detects **visual tampering patterns** and should not be interpreted as a bank-certified fraud system.

---

## Key Learnings
- Synthetic data generation is critical for fraud detection problems
- Visual tampering patterns are learnable using CNNs
- Proper dataset inspection and preprocessing are essential for real-world datasets

---

## Future Work
- Add validation split and quantitative metrics (precision, recall, ROC-AUC)
- Improve forgery realism using region-aware tampering (amount, signature, payee fields)
- Integrate signature-level verification using BCSD dataset
- Add Grad-CAM for explainable fraud detection
- Deploy using Streamlit or FastAPI

---

## Tech Stack
- Python
- PyTorch
- Torchvision
- OpenCV
- Matplotlib
- Kaggle GPU Environment

---

## Author
Built as an applied deep learning project focused on **financial document fraud detection** using PyTorch.
