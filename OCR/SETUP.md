# Environment Setup for OCR and OpenCV Labs

This guide explains how to install the required software and Python libraries for the Computer Vision labs.

## Software Requirements

| Software | Recommended Version |
|----------|---------------------|
| Python | 3.10.x |
| OpenCV | 4.10.0.84 |
| Tesseract OCR | 5.x |
| pytesseract | Latest |
| Visual Studio Code | Latest |

---

# 1. Install Python 3.10

## Download Python

Download Python 3.10 from the official website:

https://www.python.org/downloads/

During installation:

✅ Select:

```
Add Python.exe to PATH
```

Then click:

```
Install Now
```

---

## Verify Python Installation

Open Command Prompt:

```bash
python --version
```

Expected output:

```
Python 3.10.x
```

Check pip:

```bash
pip --version
```

Expected output:

```
pip 23.x.x
```

---

# 2. Create Project Folder

Create a folder for the project.

Example:

```
D:\Projects\OCR_with_OpenCV_Tesseract
```

Move into the folder:

```bash
cd D:\Projects\OCR_with_OpenCV_Tesseract
```

---

# 3. Create Python Virtual Environment

Creating a virtual environment keeps project libraries separate.

Run:

```bash
python -m venv venv
```

A new folder will be created:

```
OCR_with_OpenCV_Tesseract
│
├── venv
│
└── project files
```

---

# 4. Activate Virtual Environment

## Windows

Run:

```bash
venv\Scripts\activate
```

After activation:

```
(venv) D:\Projects\OCR_with_OpenCV_Tesseract>
```

The `(venv)` indicates that the virtual environment is active.

---

# 5. Upgrade pip

Before installing libraries, upgrade pip:

```bash
python -m pip install --upgrade pip
```

---

# 6. Install OpenCV

Install the recommended OpenCV version:

```bash
pip install opencv-python==4.10.0.84
```

---

## Verify OpenCV Installation

Run:

```bash
python -c "import cv2; print(cv2.__version__)"
```

Expected output:

```
4.10.0
```

Check Haar Cascade support:

```bash
python -c "import cv2; print(cv2.CascadeClassifier)"
```

Expected output:

```
<class 'cv2.CascadeClassifier'>
```

---

# 7. Install Tesseract OCR

Tesseract is the OCR engine that converts images into text.

Download Tesseract OCR:

https://github.com/UB-Mannheim/tesseract/wiki


Install using the default settings.

Example installation location:

```
C:\Program Files\Tesseract-OCR\
```

The main executable:

```
C:\Program Files\Tesseract-OCR\tesseract.exe
```

---

# Verify Tesseract Installation

Open Command Prompt:

```bash
tesseract --version
```

Expected output:

```
tesseract 5.x.x
```

Example:

```
tesseract 5.3.4
```

---

# 8. Install pytesseract

`pytesseract` is a Python wrapper that connects Python with Tesseract OCR.

Install:

```bash
pip install pytesseract
```

---

# Verify pytesseract Installation

Run:

```bash
python -c "import pytesseract; print(pytesseract.get_tesseract_version())"
```

Expected output:

```
5.x.x
```

---

# 9. Install Additional Libraries

Install NumPy:

```bash
pip install numpy
```

Install Pillow:

```bash
pip install pillow
```

---

# 10. Verify Complete Environment

Create a file:

```
test_environment.py
```

Add the following code:

```python
import cv2
import pytesseract
import numpy

print("OpenCV Version:", cv2.__version__)

print("Tesseract Version:",
      pytesseract.get_tesseract_version())

print("Environment Setup Successful")
```

---

Run:

```bash
python test_environment.py
```

Expected Output:

```
OpenCV Version: 4.10.0

Tesseract Version: 5.x.x

Environment Setup Successful
```

---

# 11. Required Packages Summary

Your final environment should contain:

```
Python             3.10.x
OpenCV             4.10.0.84
Tesseract OCR      5.x
pytesseract        Latest
NumPy              Latest
Pillow             Latest
```

---

# 12. requirements.txt

To save the installed packages:

```bash
pip freeze > requirements.txt
```

Generated file:

```
requirements.txt
```

Example:

```
opencv-python==4.10.0.84
pytesseract==0.x.x
numpy==x.x.x
Pillow==x.x.x
```

---

# Troubleshooting

## Problem 1: cv2 has no CascadeClassifier

Error:

```
AttributeError:
module 'cv2' has no attribute 'CascadeClassifier'
```

Solution:

Remove OpenCV:

```bash
pip uninstall opencv-python
```

Install stable version:

```bash
pip install opencv-python==4.10.0.84
```

---

## Problem 2: Tesseract Not Found

Error:

```
TesseractNotFoundError
```

Solution:

Specify the Tesseract path:

```python
import pytesseract

pytesseract.pytesseract.tesseract_cmd = (
"C:\\Program Files\\Tesseract-OCR\\tesseract.exe"
)
```

---

## Problem 3: Check Installed Packages

Run:

```bash
pip list
```

Verify:

```
opencv-python
pytesseract
numpy
Pillow
```

---

# Final Project Environment

```
OCR_with_OpenCV_Tesseract
│
├── venv/
│
├── test_environment.py
│
├── face_detection.py
│
├── ocr.py
│
├── sample.png
│
└── requirements.txt
```

---

# Conclusion

After completing this setup, your system is ready for:

- OCR using Tesseract
- Image Processing using OpenCV
- Haar Cascade Face Detection
- Computer Vision AI Labs
