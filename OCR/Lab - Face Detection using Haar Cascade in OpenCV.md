# Lab 10 – Face Detection using Haar Cascade in OpenCV

## Aim

To detect human faces in an image using the Haar Cascade Classifier and OpenCV.

---

# Learning Objectives

After completing this lab, you will be able to:

- Install OpenCV.
- Load an image using OpenCV.
- Convert an image to grayscale.
- Load a Haar Cascade XML classifier.
- Detect faces in an image.
- Draw bounding boxes around detected faces.
- Display the output image.

---

# Prerequisites

Before starting this lab, ensure that you have:

- Python 3.10 or above
- Visual Studio Code
- OpenCV installed
- Sample image containing one or more faces

---

# Software Requirements

| Software | Version |
|----------|----------|
| Python | 3.10+ |
| OpenCV | Latest |
| VS Code | Latest |

---

# Install OpenCV

Open the terminal and execute:

```bash
pip install opencv-python
```

Verify the installation:

```bash
python -c "import cv2; print(cv2.__version__)"
```

---

# Project Structure

```
HaarCascadeLab/
│
├── face_detection.py
├── person.jpg
└── output.jpg
```

---

# Sample Image

Place an image named **person.jpg** inside the project folder.

Example:

```
person.jpg

One or more people looking towards the camera.
```

---

# Complete Python Program

```python
import cv2

# Load the Haar Cascade classifier
face_cascade = cv2.CascadeClassifier(
    cv2.data.haarcascades +
    "haarcascade_frontalface_default.xml"
)

# Read the input image
image = cv2.imread("person.jpg")

# Convert image to grayscale
gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

# Detect faces
faces = face_cascade.detectMultiScale(
    gray,
    scaleFactor=1.1,
    minNeighbors=5,
    minSize=(30, 30)
)

# Draw rectangles around detected faces
for (x, y, w, h) in faces:
    cv2.rectangle(
        image,
        (x, y),
        (x + w, y + h),
        (0, 255, 0),
        2
    )

# Display number of detected faces
print("Number of faces detected:", len(faces))

# Save the output image
cv2.imwrite("output.jpg", image)

# Display image
cv2.imshow("Face Detection", image)

cv2.waitKey(0)
cv2.destroyAllWindows()
```

---

# Expected Output

Console

```
Number of faces detected: 2
```

Image Output

```
+----------------------------+
|                            |
|  ┌──────────┐              |
|  │   Face   │              |
|  └──────────┘              |
|                            |
|             ┌──────────┐   |
|             │   Face   │   |
|             └──────────┘   |
|                            |
+----------------------------+
```

Green rectangles will appear around every detected face.

---

# Code Explanation

## Line 1

```python
import cv2
```

Imports the OpenCV library.

OpenCV provides functions for image processing and object detection.

---

## Loading the Haar Cascade

```python
face_cascade = cv2.CascadeClassifier(
    cv2.data.haarcascades +
    "haarcascade_frontalface_default.xml"
)
```

This loads the pre-trained Haar Cascade classifier.

OpenCV already includes many trained XML files.

The file

```
haarcascade_frontalface_default.xml
```

is trained to detect frontal human faces.

---

## What is an XML File?

The XML file contains thousands of learned Haar features.

It acts as the trained model used for detecting faces.

You do **not** need to train it yourself.

---

## Reading the Image

```python
image = cv2.imread("person.jpg")
```

Reads the image from disk.

The image is stored in the variable **image**.

---

## Converting to Grayscale

```python
gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
```

Converts the color image into grayscale.

Haar Cascade only requires brightness information.

Working with grayscale images:

- Reduces memory usage
- Increases processing speed
- Improves detection efficiency

---

## Detecting Faces

```python
faces = face_cascade.detectMultiScale(
    gray,
    scaleFactor=1.1,
    minNeighbors=5,
    minSize=(30,30)
)
```

This is the main function of the program.

It searches the image for faces.

The function returns the coordinates of every detected face.

Each detected face is represented as:

```
(x, y, width, height)
```

Example

```
(120, 60, 150, 150)
```

---

# Understanding detectMultiScale()

## Parameter 1

```python
gray
```

The grayscale image in which faces will be detected.

---

## Parameter 2

```python
scaleFactor = 1.1
```

Faces may appear at different sizes.

The image is repeatedly scaled down by 10% each time.

Smaller values improve accuracy but increase processing time.

Typical values:

```
1.05

1.10

1.20
```

---

## Parameter 3

```python
minNeighbors = 5
```

Determines how many nearby detections are required before accepting a face.

Higher values:

- Fewer false detections
- More reliable results

Lower values:

- Detects more faces
- May produce false positives

---

## Parameter 4

```python
minSize = (30,30)
```

Minimum size of a detected face.

Very small regions are ignored.

---

# Drawing Rectangles

```python
for (x, y, w, h) in faces:
```

Loops through every detected face.

Example

```
Face 1

x = 120

y = 90

w = 140

h = 140
```

---

## Drawing the Bounding Box

```python
cv2.rectangle(
    image,
    (x,y),
    (x+w,y+h),
    (0,255,0),
    2
)
```

Draws a rectangle around the detected face.

Parameters:

```
image
```

Image to draw on.

```
(x,y)
```

Top-left corner.

```
(x+w,y+h)
```

Bottom-right corner.

```
(0,255,0)
```

Green color in BGR format.

```
2
```

Rectangle thickness in pixels.

---

# Counting Faces

```python
print(len(faces))
```

Displays the number of detected faces.

Example

```
2
```

means two faces were found.

---

# Saving the Output

```python
cv2.imwrite("output.jpg", image)
```

Saves the processed image.

The output file contains the detected faces with rectangles.

---

# Displaying the Image

```python
cv2.imshow("Face Detection", image)
```

Opens a window displaying the result.

---

# Waiting for a Key

```python
cv2.waitKey(0)
```

Waits indefinitely until the user presses a key.

---

# Closing the Window

```python
cv2.destroyAllWindows()
```

Closes all OpenCV windows and releases resources.

---

# Program Workflow

```
Start
   │
   ▼
Read Image
   │
   ▼
Convert to Grayscale
   │
   ▼
Load Haar Cascade XML
   │
   ▼
Detect Faces
   │
   ▼
Draw Rectangles
   │
   ▼
Count Faces
   │
   ▼
Save Output Image
   │
   ▼
Display Result
   │
   ▼
End
```

---

# Exercises

## Exercise 1

Detect faces in your own photograph.

---

## Exercise 2

Test the program using a group photo.

Count how many faces are detected.

---

## Exercise 3

Change

```python
minNeighbors=5
```

to

```python
minNeighbors=3
```

Observe the difference.

---

## Exercise 4

Change

```python
scaleFactor
```

to

```
1.05

1.20
```

Compare the detection speed and accuracy.

---

## Challenge

Modify the program to display:

```
Face 1

Face 2

Face 3
```

above each detected face using:

```python
cv2.putText()
```

---

# Viva Questions

1. What is Haar Cascade?
2. Why is grayscale conversion necessary?
3. What is the purpose of `detectMultiScale()`?
4. What does `scaleFactor` control?
5. Why is `minNeighbors` important?
6. What does the XML file contain?
7. What is the purpose of `cv2.rectangle()`?
8. Why do we use `cv2.waitKey(0)`?
9. How does Haar Cascade differ from YOLO?
10. Mention three applications of Haar Cascade.

---

# Conclusion

In this lab, you learned how to use **OpenCV** and the **Haar Cascade Classifier** to detect human faces in an image. You explored how a pre-trained XML classifier works, converted images to grayscale for efficient processing, detected multiple faces, drew bounding boxes, counted the number of detected faces, and saved the final output. This lab provides a strong foundation for more advanced face recognition and object detection techniques such as **LBPH Face Recognition**, **DNN-based Face Detection**, and **YOLO Object Detection**.
