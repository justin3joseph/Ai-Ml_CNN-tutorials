# Lab 09 – Optical Character Recognition (OCR) using OpenCV and Tesseract

## Aim

To extract text from an image using OpenCV and Tesseract OCR.

---

# Prerequisites

Before starting this lab, ensure you have:

- Python 3.10 or later
- Visual Studio Code
- OpenCV
- pytesseract
- Tesseract OCR installed

---

# Software Requirements

| Software | Version |
|----------|----------|
| Python | 3.10+ |
| OpenCV | Latest |
| pytesseract | Latest |
| Tesseract OCR | Latest |
| VS Code | Latest |

---

# Install Required Libraries

Open the terminal and execute the following commands.

```bash
pip install opencv-python
pip install pytesseract
```

---

# Install Tesseract OCR

### Windows

Download and install

https://github.com/UB-Mannheim/tesseract/wiki

After installation, remember the installation path.

Example

```text
C:\Program Files\Tesseract-OCR\tesseract.exe
```

---

# Project Structure

```
OCR-Lab/
│
├── sample.png
├── ocr.py
└── output.txt
```

---

# Sample Image

Create an image named **sample.png**

Example

```
-------------------------
Name : Justin Joseph
Course : AI & ML
Roll No : 105
-------------------------
```

Save it inside the project folder.

---

# Complete Python Program

```python
import cv2
import pytesseract

# Path to Tesseract executable (Windows only)
pytesseract.pytesseract.tesseract_cmd = r"C:\Program Files\Tesseract-OCR\tesseract.exe"

# Read the image
image = cv2.imread("sample.png")

# Convert image into grayscale
gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

# Apply binary thresholding
threshold = cv2.threshold(
    gray,
    150,
    255,
    cv2.THRESH_BINARY
)[1]

# Extract text
text = pytesseract.image_to_string(threshold)

# Display extracted text
print("Extracted Text")
print("----------------")
print(text)

# Save extracted text into a file
with open("output.txt", "w") as file:
    file.write(text)

print("\nText saved successfully.")

# Display image
cv2.imshow("Input Image", image)

cv2.waitKey(0)
cv2.destroyAllWindows()
```

---

# Program Output

```
Extracted Text
----------------

Name : Justin Joseph
Course : AI & ML
Roll No : 105

Text saved successfully.
```

---

# Code Explanation

## Line 1

```python
import cv2
```

Imports the **OpenCV** library.

OpenCV is used for

- Reading images
- Processing images
- Displaying images

---

## Line 2

```python
import pytesseract
```

Imports the Python wrapper for Tesseract OCR.

This library communicates with the Tesseract OCR engine.

---

## Line 5

```python
pytesseract.pytesseract.tesseract_cmd = r"C:\Program Files\Tesseract-OCR\tesseract.exe"
```

This tells Python where Tesseract OCR is installed.

### Why?

`pytesseract` is only a Python interface. The actual OCR engine is the **Tesseract executable** installed on your system. This line points Python to that executable.

> **Linux/macOS:** If Tesseract is installed through the package manager and available in your system's PATH, you usually **do not need this line**.

---

## Line 8

```python
image = cv2.imread("sample.png")
```

Reads the image from disk.

The image is stored inside the variable called **image**.

---

## What does `imread()` mean?

**im** → Image

**read** → Read

So,

```
cv2.imread()
```

means

> Read an image from storage.

---

## Line 11

```python
gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
```

Converts the color image into grayscale.

OCR performs better on grayscale images because it removes unnecessary color information.

Example

```
Color Image

↓

Gray Image
```

---

## What is BGR?

OpenCV stores images in

```
Blue
Green
Red
```

instead of

```
Red
Green
Blue
```

Therefore,

```
COLOR_BGR2GRAY
```

means

```
Convert

Blue Green Red

↓

Gray
```

---

## Line 14

```python
threshold = cv2.threshold(
    gray,
    150,
    255,
    cv2.THRESH_BINARY
)[1]
```

This converts the grayscale image into a binary (black and white) image.

### Parameters

```
gray
```

Input image.

```
150
```

Threshold value.

Any pixel below 150 becomes black.

```
255
```

Maximum value (white).

```
cv2.THRESH_BINARY
```

Binary thresholding mode.

The `[1]` at the end selects the thresholded image from the function's return values.

---

## Why Thresholding?

Without thresholding

```
Gray Gray Gray
Gray Gray Gray
```

After thresholding

```
Black White Black
White White Black
```

Characters become clearer.

OCR becomes more accurate.

---

## Line 22

```python
text = pytesseract.image_to_string(threshold)
```

This is the most important line.

It sends the processed image to Tesseract.

Tesseract recognizes every character.

Returns

```
Editable Text
```

---

## Line 25

```python
print("Extracted Text")
```

Displays the heading.

---

## Line 26

```python
print("----------------")
```

Prints a separator line.

---

## Line 27

```python
print(text)
```

Prints the extracted text on the console.

---

## Line 30

```python
with open("output.txt", "w") as file:
```

Creates a text file.

```
output.txt
```

The `"w"` mode means **write mode**.

If the file already exists, its contents are overwritten.

---

## Line 31

```python
file.write(text)
```

Writes the extracted text into the file.

Example

```
output.txt

Name : Justin Joseph
Course : AI & ML
Roll No : 105
```

---

## Line 33

```python
print("\nText saved successfully.")
```

Displays a success message.

---

## Line 36

```python
cv2.imshow("Input Image", image)
```

Displays the original image in a new window.

---

## Line 38

```python
cv2.waitKey(0)
```

Waits indefinitely until a key is pressed.

Without this line, the image window closes immediately.

---

## Line 39

```python
cv2.destroyAllWindows()
```

Closes all OpenCV windows and releases associated resources.

---

# Complete Workflow

```
Image

      │

      ▼

Read Image using OpenCV

      │

      ▼

Convert to Grayscale

      │

      ▼

Apply Threshold

      │

      ▼

Tesseract OCR

      │

      ▼

Extract Text

      │

      ▼

Display Output

      │

      ▼

Save into Text File
```

---

# Expected Output

Console

```
Extracted Text

Name : Justin Joseph
Course : AI & ML
Roll No : 105
```

Generated File

```
output.txt
```

containing the extracted text.

---

# Exercises

### Exercise 1

Create an image containing your name and extract the text.

---

### Exercise 2

Extract text from a newspaper image.

---

### Exercise 3

Extract text from a college ID card.

---

### Exercise 4

Try OCR on a handwritten note and compare the results with printed text.

---

# Viva Questions

1. What is OCR?
2. What is Tesseract?
3. Why do we convert an image to grayscale?
4. What is thresholding?
5. What does `cv2.imread()` do?
6. What is the purpose of `image_to_string()`?
7. Why is preprocessing important before OCR?
8. What is the purpose of `cv2.waitKey(0)`?
9. What file format is generated in this lab?
10. Name three real-world applications of OCR.

---

# Conclusion

In this lab, you learned how to use **OpenCV** to preprocess an image and **Tesseract OCR** to extract editable text. You also learned why grayscale conversion and thresholding improve OCR accuracy. This forms the foundation for more advanced applications such as invoice processing, document digitization, automatic form reading, and number plate recognition.
