# Lab 09 – Optical Character Recognition (OCR)

## Aim

To understand the fundamentals of Optical Character Recognition (OCR), learn how OCR works, and extract text from images using Python and Tesseract OCR.

---

# Learning Objectives

After completing this lab, you will be able to:

- Understand what OCR is.
- Explain how OCR works.
- Identify the different stages of the OCR process.
- Understand the role of image preprocessing.
- Learn about Tesseract OCR.
- Understand real-world applications of OCR.
- Prepare images for better OCR accuracy.

---

# Introduction

Many documents today are available only as images or scanned copies. Since computers cannot directly understand the text inside an image, we need a technology that converts the text into editable digital text.

This technology is called **Optical Character Recognition (OCR).**

OCR is one of the most widely used applications of Artificial Intelligence and Computer Vision. It helps computers read printed or handwritten text from images, scanned documents, photographs, and video frames.

For example, when you scan a book page using your mobile phone and copy the text into Microsoft Word, OCR is performing the recognition in the background.

---

# What is OCR?

**Optical Character Recognition (OCR)** is a technology that detects and converts text from images into machine-readable text.

In simple words,

> OCR allows a computer to **read text from an image**.

Instead of storing only the picture of a document, OCR extracts the actual letters, numbers, and symbols.

---

## Example

### Input Image

```text
--------------------------
| Student Name : Justin  |
| Roll No      : 101     |
| Course       : AI & ML |
--------------------------
```

### OCR Output

```text
Student Name : Justin
Roll No      : 101
Course       : AI & ML
```

Now the extracted text can be:

- Edited
- Copied
- Searched
- Stored in a database
- Translated
- Processed by AI applications

---

# Why Do We Need OCR?

Imagine a company has **10,000 paper invoices**.

Without OCR:

- An employee must type every invoice manually.
- It takes many hours or even days.
- Human typing errors are common.

With OCR:

- Scan the invoices.
- OCR extracts the text automatically.
- The data is saved into a database.

This saves time, cost, and effort.

---

# Everyday Examples of OCR

You may already use OCR without realizing it.

Examples include:

- Google Lens
- Google Translate Camera
- Microsoft Office Lens
- Adobe Scan
- Mobile banking cheque scanning
- Passport scanning
- Aadhaar card scanning
- QR invoice processing

---

# History of OCR

The development of OCR has improved over many years.

| Year | Development |
|------|-------------|
| 1920s | Early character-reading machines |
| 1950s | OCR used for printed text |
| 1970s | Commercial OCR software introduced |
| 1990s | Better recognition algorithms |
| Today | AI and Deep Learning provide highly accurate OCR |

Modern OCR systems can recognize:

- Printed text
- Handwritten text
- Multiple languages
- Numbers
- Symbols

---

# How OCR Works

OCR performs several steps before producing editable text.

```text
Image
   │
   ▼
Image Preprocessing
   │
   ▼
Text Detection
   │
   ▼
Character Recognition
   │
   ▼
Post Processing
   │
   ▼
Editable Text
```

Each stage improves the accuracy of the final output.

---

# OCR Workflow Explained

## Step 1 – Image Acquisition

The first step is to obtain an image.

The image may come from:

- Camera
- Scanner
- Mobile phone
- CCTV
- Screenshot

Example:

```text
Photo of an Invoice
```

↓

OCR receives this image.

---

## Step 2 – Image Preprocessing

Real-world images are often noisy or blurred.

Before recognizing text, OCR improves the image quality.

Common preprocessing techniques include:

- Convert to Grayscale
- Remove Noise
- Increase Contrast
- Resize Image
- Thresholding
- Deskew Image

Better images produce better OCR results.

---

### Grayscale

The color image is converted into black and white shades.

```text
Color Image
      │
      ▼
Grayscale Image
```

This reduces unnecessary color information.

---

### Noise Removal

Images captured using mobile phones often contain small dots or unwanted pixels.

Noise removal helps OCR recognize characters more accurately.

---

### Thresholding

Thresholding converts the image into pure black and white.

Example

```text
Gray Image

████░░░░

↓

Binary Image

████____
```

This makes characters more visible.

---

# Step 3 – Text Detection

OCR first finds **where text exists** in the image.

For example,

```
--------------------------------
|      COMPANY LOGO            |
|                              |
| Invoice No : 1023            |
| Date : 12-01-2026            |
--------------------------------
```

OCR ignores the logo and detects only the text region.

---

# Step 4 – Character Recognition

Once the text area is detected,

OCR separates each letter.

Example

```
HELLO

↓

H
E
L
L
O
```

Each character is compared with learned patterns.

Modern OCR uses Artificial Intelligence to recognize characters with high accuracy.

---

# Step 5 – Post Processing

After recognizing all characters,

OCR corrects possible mistakes.

Example

Incorrect OCR:

```
Hell0
```

Corrected OCR:

```
Hello
```

Many OCR systems use dictionaries and language models to improve accuracy.

---

# OCR Pipeline

```text
                IMAGE
                  │
                  ▼
      Image Preprocessing
                  │
                  ▼
          Text Detection
                  │
                  ▼
      Character Segmentation
                  │
                  ▼
      Character Recognition
                  │
                  ▼
         Error Correction
                  │
                  ▼
          Editable Text
```

---

# What is Tesseract OCR?

**Tesseract** is one of the world's most popular open-source OCR engines.

It was originally developed by Hewlett-Packard (HP) and is now maintained by Google.

Python can easily use Tesseract through the **pytesseract** library.

Advantages include:

- Free
- Open source
- Supports more than 100 languages
- Fast
- Easy to integrate with OpenCV

---

# OCR and OpenCV

OpenCV is mainly used for image processing.

Tesseract is mainly used for text recognition.

Together they create a powerful OCR system.

```text
Image

   │

OpenCV
(Image Enhancement)

   │

Tesseract OCR

   │

Editable Text
```

---

# Applications of OCR

OCR is used in many industries.

## Education

- Digitizing books
- Reading answer sheets
- Converting notes into editable text

---

## Banking

- Cheque processing
- Account verification
- Invoice processing

---

## Healthcare

- Reading prescriptions
- Digitizing patient records
- Medical reports

---

## Government

- Passport verification
- Aadhaar processing
- Driving license scanning

---

## Business

- Invoice automation
- Receipt scanning
- Document management

---

## Transportation

- Number plate recognition
- Ticket scanning
- Boarding pass verification

---

# Advantages of OCR

- Saves time
- Reduces manual typing
- Improves productivity
- Easy document search
- Digital document storage
- High accuracy for printed text
- Supports automation

---

# Limitations of OCR

OCR is not perfect.

Some challenges include:

- Poor image quality
- Blurred photographs
- Different font styles
- Low lighting
- Handwritten text
- Rotated documents

Proper image preprocessing greatly improves OCR accuracy.

---

# Best Practices for Better OCR Accuracy

To obtain better OCR results:

- Use high-resolution images.
- Keep the document flat.
- Avoid shadows.
- Increase brightness if needed.
- Remove image noise.
- Convert to grayscale.
- Apply thresholding.
- Crop unnecessary regions.

---

# OCR vs Manual Typing

| OCR | Manual Typing |
|------|---------------|
| Fast | Slow |
| Automatic | Manual |
| Saves time | Time consuming |
| Suitable for thousands of documents | Suitable for small amounts of text |
| Can process scanned images | Requires a person |

---

# OCR vs Barcode vs QR Code

| OCR | Barcode | QR Code |
|------|----------|----------|
| Reads printed text | Reads product codes | Stores large amounts of information |
| Uses AI | Uses barcode scanner | Uses QR scanner |
| Can recognize letters and numbers | Numbers only | Text, links, contacts, and more |

---

# Summary

In this chapter, you learned:

- OCR stands for **Optical Character Recognition**.
- OCR converts text from images into editable text.
- OCR works through preprocessing, text detection, character recognition, and post-processing.
- OpenCV improves image quality before OCR.
- Tesseract is one of the most popular open-source OCR engines.
- OCR is widely used in banking, healthcare, education, government, and business.
- Better image quality leads to better OCR accuracy.

---

## Key Points to Remember

- OCR = Reading text from images.
- OpenCV = Image processing.
- Tesseract = Text recognition.
- Good preprocessing improves OCR results.
- OCR is a core technology in Artificial Intelligence and Computer Vision.
