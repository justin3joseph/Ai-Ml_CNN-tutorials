# OpenCV Basics

## Objective

In this lab, you will learn how to:

- Install OpenCV
- Read and display images
- Access and modify pixels
- Work with image properties
- Process images
- Capture video from files and webcams
- Draw shapes and text
- Perform basic image processing operations

---

# What is OpenCV?

**OpenCV (Open Source Computer Vision Library)** is an open-source library used for **Computer Vision**, **Image Processing**, and **Machine Learning** applications.

It provides optimized functions for reading, processing, analyzing, and displaying images and videos in real time.

### Features

- Image Processing
- Video Processing
- Face Detection
- Object Detection
- OCR
- Gesture Recognition
- Camera Calibration
- Machine Learning
- Image Segmentation

---

# Why Learn OpenCV?

OpenCV is widely used in:

- Self-driving Cars
- CCTV Surveillance
- Robotics
- Medical Imaging
- AI Applications
- Augmented Reality
- Industrial Automation
- Object Detection using YOLO

---

# Installing OpenCV

Install OpenCV using pip.

```bash
pip install opencv-python
```

Install additional OpenCV modules.

```bash
pip install opencv-contrib-python
```

Verify installation.

```python
import cv2

print(cv2.__version__)
```

Example Output

```
4.12.0
```

---

# Reading an Image

```python
import cv2

img = cv2.imread("cat.jpg")

cv2.imshow("Image", img)

cv2.waitKey(0)

cv2.destroyAllWindows()
```

## Explanation

| Function | Description |
|----------|-------------|
| `cv2.imread()` | Reads an image from disk |
| `cv2.imshow()` | Displays the image |
| `cv2.waitKey()` | Waits for a keyboard key |
| `cv2.destroyAllWindows()` | Closes all OpenCV windows |

---

# Understanding Images

An image is simply a matrix of pixels.

Example:

```
255 120 90
100 180 60
40  70 200
```

For a color image, each pixel contains three values.

```
[B, G, R]
```

Example:

```
[255,0,0] → Blue
[0,255,0] → Green
[0,0,255] → Red
```

> **Note**
>
> OpenCV stores images in **BGR** format instead of RGB.

---

# Image Properties

## Shape

```python
print(img.shape)
```

Example Output

```
(720, 1280, 3)
```

Meaning:

- Height = 720
- Width = 1280
- Channels = 3

---

## Size

```python
print(img.size)
```

Formula

```
Height × Width × Channels
```

---

## Data Type

```python
print(img.dtype)
```

Example

```
uint8
```

Pixel values range from **0–255**.

---

# Accessing Pixels

```python
pixel = img[100,200]

print(pixel)
```

Example Output

```
[120 65 230]
```

Meaning

```
Blue  = 120
Green = 65
Red   = 230
```

---

# Access Individual Channels

```python
blue = img[100,200,0]
green = img[100,200,1]
red = img[100,200,2]

print(blue, green, red)
```

---

# Changing Pixel Values

```python
img[100,200] = [0,0,255]
```

This changes the pixel to **Red**.

---

# Saving an Image

```python
cv2.imwrite("new_image.jpg", img)
```

---

# Display Multiple Images

```python
import cv2

img1 = cv2.imread("cat.jpg")
img2 = cv2.imread("dog.jpg")

cv2.imshow("Cat", img1)
cv2.imshow("Dog", img2)

cv2.waitKey(0)

cv2.destroyAllWindows()
```

---

# Reading a Video

```python
import cv2

cap = cv2.VideoCapture("video.mp4")

while True:

    ret, frame = cap.read()

    if not ret:
        break

    cv2.imshow("Video", frame)

    if cv2.waitKey(25) & 0xFF == ord('q'):
        break

cap.release()

cv2.destroyAllWindows()
```

---

# Webcam Capture

```python
import cv2

cap = cv2.VideoCapture(0)

while True:

    ret, frame = cap.read()

    if not ret:
        break

    cv2.imshow("Webcam", frame)

    if cv2.waitKey(1) & 0xFF == ord('q'):
        break

cap.release()

cv2.destroyAllWindows()
```

---

# Color Space Conversion

## Convert to Grayscale

```python
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
```

## Convert to RGB

```python
rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
```

## Convert to HSV

```python
hsv = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)
```

---

# Resize an Image

```python
resized = cv2.resize(img, (640,480))
```

---

# Crop an Image

```python
crop = img[100:400,200:500]
```

Syntax

```
img[startY:endY, startX:endX]
```

---

# Drawing Shapes

## Draw Line

```python
cv2.line(img, (50,50), (300,50), (0,255,0), 3)
```

---

## Draw Rectangle

```python
cv2.rectangle(img, (100,100), (300,250), (255,0,0), 2)
```

---

## Draw Circle

```python
cv2.circle(img, (250,250), 80, (0,0,255), 3)
```

---

## Filled Circle

```python
cv2.circle(img, (250,250), 80, (0,255,0), -1)
```

---

# Add Text

```python
cv2.putText(
    img,
    "OpenCV",
    (50,50),
    cv2.FONT_HERSHEY_SIMPLEX,
    1,
    (255,0,0),
    2
)
```

---

# Split Color Channels

```python
b, g, r = cv2.split(img)
```

Merge Again

```python
merged = cv2.merge((b,g,r))
```

---

# Flip an Image

```python
flip = cv2.flip(img, 1)
```

| Value | Operation |
|-------|-----------|
| 0 | Vertical Flip |
| 1 | Horizontal Flip |
| -1 | Both |

---

# Rotate an Image

```python
rotated = cv2.rotate(img, cv2.ROTATE_90_CLOCKWISE)
```

---

# Gaussian Blur

```python
blur = cv2.GaussianBlur(img, (5,5), 0)
```

---

# Edge Detection

```python
edges = cv2.Canny(img, 100, 200)
```

---

# Binary Threshold

```python
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

_, thresh = cv2.threshold(
    gray,
    127,
    255,
    cv2.THRESH_BINARY
)
```

---

# Image Processing Workflow

```text
Image
   │
   ▼
Read Image
   │
   ▼
Resize
   │
   ▼
Convert Color
   │
   ▼
Noise Removal
   │
   ▼
Edge Detection
   │
   ▼
Feature Extraction
   │
   ▼
Object Detection
   │
   ▼
Display Result
```

---

# OpenCV + YOLO Workflow

```text
Camera/Image
      │
      ▼
OpenCV Reads Image
      │
      ▼
Preprocessing
      │
      ▼
YOLO Model
      │
      ▼
Object Detection
      │
      ▼
Bounding Boxes
      │
      ▼
Display Result
```

---

# Mini Project

Detect edges in an image.

```python
import cv2

img = cv2.imread("road.jpg")

gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

edges = cv2.Canny(gray, 100, 200)

cv2.imshow("Original", img)
cv2.imshow("Edges", edges)

cv2.waitKey(0)

cv2.destroyAllWindows()
```

---

# Frequently Used OpenCV Functions

| Function | Purpose |
|----------|---------|
| `cv2.imread()` | Read an image |
| `cv2.imwrite()` | Save an image |
| `cv2.imshow()` | Display an image |
| `cv2.VideoCapture()` | Read webcam/video |
| `cv2.cvtColor()` | Convert color space |
| `cv2.resize()` | Resize image |
| `cv2.flip()` | Flip image |
| `cv2.rotate()` | Rotate image |
| `cv2.GaussianBlur()` | Blur image |
| `cv2.Canny()` | Edge detection |
| `cv2.threshold()` | Thresholding |
| `cv2.rectangle()` | Draw rectangle |
| `cv2.circle()` | Draw circle |
| `cv2.line()` | Draw line |
| `cv2.putText()` | Draw text |

---

# Lab Exercises

1. Read and display an image.
2. Print image properties.
3. Access a pixel value.
4. Modify a pixel.
5. Convert to grayscale.
6. Resize an image.
7. Crop an image.
8. Draw a rectangle and circle.
9. Add text to an image.
10. Apply Gaussian Blur.
11. Detect edges using Canny.
12. Capture webcam video.
13. Read and display a video file.

---

# Summary

After completing this lab, you should be able to:

- Install OpenCV
- Read and display images
- Work with pixels
- Understand image properties
- Resize and crop images
- Draw shapes and text
- Capture webcam and video
- Apply basic image processing techniques
- Prepare images for AI models such as YOLO

---

**Next Lab:** Image Transformations and Geometric Operations in OpenCV
