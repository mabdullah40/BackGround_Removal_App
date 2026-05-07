# 🖼️ Flask Background Removal App

A simple yet powerful Flask web application that automatically removes the background from images using deep learning.

![Python](https://img.shields.io/badge/python-3.9-blue.svg)
![PyTorch](https://img.shields.io/badge/PyTorch-1.10.2-ee4c2c.svg)
![Flask](https://img.shields.io/badge/Flask-2.0.3-lightgrey.svg)

---

## 🌟 Overview

This application provides a web interface where users can upload an image, and it returns the image with the background completely removed. It leverages the **U<sup>2</sup>-Net (U-Square-Net)** deep learning architecture via **PyTorch** to generate highly accurate salient object masks.

## ✨ Key Features

- **Web Interface:** Easy-to-use Flask UI for uploading and viewing images.
- **Deep Learning Powered:** Uses the pre-trained `U2NET` model for state-of-the-art salient object detection.
- **Automatic Masking:** Generates an alpha matte (mask) and automatically applies it to extract the foreground.
- **CPU/GPU Support:** Automatically detects and uses CUDA if available, falling back to CPU otherwise.

## 🏗️ Architecture

- **Backend:** Flask (`app.py`) handles routing, file uploads, and model inference.
- **Model Architecture:** U<sup>2</sup>-Net implemented in PyTorch (`model/`).
- **Data Preprocessing:** Images are resized to `320x320`, normalized, and passed as tensors to the network.
- **Output:** The predicted mask is combined with the original image as an RGBA PNG, saving the final output in the `static/results/` directory.

## 🚀 Getting Started

Follow these instructions to get the application running on your local machine.

### Prerequisites

You need `python 3.9` installed. It is highly recommended to use a virtual environment like Conda or venv.

### Installation Steps

1. **Clone the repository:**
   ```bash
   git clone https://github.com/iabahmad/background_removal_app.git
   cd background_removal_app
   ```

2. **Create a virtual environment (Optional but recommended):**
   ```bash
   conda create -p ./venv python==3.9
   conda activate ./venv/
   ```

3. **Install the required dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

   *Note: This will install PyTorch, OpenCV, Flask, scikit-image, and other necessary libraries.*

4. **Model Weights:**
   Ensure that the pre-trained U2NET model file (`u2net.pth`) is placed inside the `saved_models/u2net/` directory.

### Running the App

Start the Flask development server:

```bash
flask run
```
*Alternatively, you can run:*
```bash
python app.py
```

The application will start on `http://127.0.0.1:5000/`.

## 📁 Directory Structure

```text
background_removal_app/
│
├── app.py                 # Main Flask application and inference pipeline
├── model/                 # Contains the U2NET model architecture classes
├── data_loader.py         # Helper functions for data loading (if used)
├── saved_models/          # Directory containing the pre-trained weights
│   └── u2net/
│       └── u2net.pth      # Model weights file
├── static/                # Static assets
│   ├── inputs/            # Temporarily saves user uploaded images
│   ├── masks/             # Saves the generated black/white masks
│   └── results/           # Saves the final background-removed images
├── templates/             # HTML templates (index.html)
└── uploads/               # Directory for raw incoming uploads
```

## 🧠 How it Works

1. The user uploads an image via the web interface (`/`).
2. The image is saved locally and loaded via OpenCV.
3. It is resized and normalized into a PyTorch FloatTensor.
4. The tensor is passed through the `U2NET` network.
5. The network outputs a mask predicting the salient object.
6. A post-processing script overlays the mask onto the original image, converting the background to transparent (RGBA).
7. The result is returned to the frontend.

## 📝 License

This project is open-source. Please refer to the repository owner for specific licensing details.
