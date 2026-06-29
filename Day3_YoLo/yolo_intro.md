# Introduction to YOLO (You Only Look Once)

## Objective

After completing this lesson, students will be able to:

- Understand what Object Detection is.
- Differentiate Image Classification and Object Detection.
- Explain why YOLO is widely used.
- Install and run YOLO for the first time.
- Detect objects in images using a pre-trained YOLO model.

---

# What is Computer Vision?

Computer Vision is a field of Artificial Intelligence (AI) that enables computers to understand and interpret images and videos similarly to humans.

Examples include:

- Face Recognition
- Vehicle Detection
- Medical Image Analysis
- Traffic Monitoring
- Security Surveillance
- Self-driving Cars

---

# What is Image Classification?

Image Classification predicts **what object is present** in an image.

### Example

Input Image

```
+-----------------------+
|                       |
|        🐱             |
|                       |
+-----------------------+
```

Output

```
Cat
```

The model identifies the object but **does not know where it is located**.

---

# Limitation of Image Classification

Consider the following image:

```
+--------------------------------------+
|   🚗      🚌        🚶       🚲        |
+--------------------------------------+
```

Image Classification may only predict:

```
Vehicles
```

It cannot answer:

- Where is the car?
- Where is the person?
- How many objects are present?

---

# What is Object Detection?

Object Detection identifies:

- What the object is
- Where it is located
- How confident the model is

Example

```
Car      98%
Bus      96%
Person   94%

+--------------------------------------+
| [Car]     [Bus]      [Person]        |
+--------------------------------------+
```

This is called **Object Detection**.

---

# What is YOLO?

YOLO stands for

> **You Only Look Once**

It is one of the fastest and most popular real-time Object Detection algorithms.

Instead of scanning an image multiple times, YOLO processes the image **only once**.

This makes it extremely fast.

---

# Traditional Object Detection

Older algorithms examine different parts of the image repeatedly.

```
Image

↓

Scan

↓

Scan Again

↓

Scan Again

↓

Detect Objects
```

This approach is slower.

---

# YOLO Approach

YOLO processes the image in a single pass.

```
Image

↓

YOLO

↓

Detect All Objects
```

Advantages

- Faster
- Real-time
- Higher efficiency
- Suitable for live video

---

# Applications of YOLO

YOLO is widely used in:

- Smart Traffic Systems
- Self-driving Cars
- CCTV Surveillance
- Face Detection
- Industrial Automation
- Agriculture
- Medical Imaging
- Robotics
- Retail Analytics

---

# How YOLO Works

YOLO divides an image into multiple grid cells.

Example

```
+-----+-----+-----+
|     |Car  |     |
+-----+-----+-----+
|Dog  |     |Bus  |
+-----+-----+-----+
|     |Man  |     |
+-----+-----+-----+
```

Each grid predicts:

- Object present?
- Object class
- Bounding Box
- Confidence Score

---

# Bounding Box

A Bounding Box is a rectangle drawn around an object.

Example

```
+-------------------------+
|                         |
|     +-----------+       |
|     |   Car     |       |
|     +-----------+       |
|                         |
+-------------------------+
```

Each bounding box contains:

- x-coordinate
- y-coordinate
- Width
- Height

---

# Confidence Score

Confidence Score indicates how certain the model is about its prediction.

Example

| Object | Confidence |
|----------|------------|
| Car | 99% |
| Person | 96% |
| Bicycle | 91% |

Higher confidence means higher certainty.

---

# YOLO Workflow

```
Image

↓

Resize

↓

CNN Backbone

↓

Feature Extraction

↓

YOLO Detection Head

↓

Bounding Boxes

↓

Confidence Score

↓

Object Class

↓

Final Detection
```

---

# CNN vs YOLO

| CNN | YOLO |
|------|------|
| Image Classification | Object Detection |
| One object | Multiple objects |
| No location | Gives object location |
| Class prediction | Class + Bounding Box |
| Mainly for classification | Real-time detection |

---

# Installing YOLO

Install Ultralytics

```bash
pip install ultralytics
```

---

# Verify Installation

```python
from ultralytics import YOLO

print("YOLO Installed Successfully")
```

---

# Download a Pre-trained Model

```python
from ultralytics import YOLO

model = YOLO("yolov8n.pt")
```

The first execution automatically downloads the model.

---

# Detect Objects in an Image

```python
from ultralytics import YOLO

model = YOLO("yolov8n.pt")

results = model("bus.jpg", show=True)
```

---

# Understanding the Code

```python
model = YOLO("yolov8n.pt")
```

Loads the pre-trained YOLO model.

---

```python
results = model("cat.jpg")
```

Runs object detection.

---

```python
show=True
```

Displays the output image.

---

# Print Detection Results

```python
for result in results:
    print(result.boxes)
```

Example Output

```
Person
Bus
Car
Traffic Light
```

---

# Live Webcam Detection

```python
from ultralytics import YOLO

model = YOLO("yolov8n.pt")

model.predict(source=0, show=True)
```

This opens the webcam and performs real-time object detection.

---

# Summary

In this lesson, we learned:

- Computer Vision
- Image Classification
- Object Detection
- YOLO
- Bounding Boxes
- Confidence Score
- Installing YOLO
- Running the first object detection program

---

# Lab Exercise

## Exercise 1

Install Ultralytics.

---

## Exercise 2

Load the YOLOv8 Nano model.

---

## Exercise 3

Run object detection on an image.

---

## Exercise 4

Run live webcam object detection.

---

# Assignment

1. Detect objects from five different images.
2. Record the detected object names.
3. Compare the confidence scores.
4. Explain why confidence scores differ between images.

---

