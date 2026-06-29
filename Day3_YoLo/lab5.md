# YOLO Object Detection using Google Colab

## 🎯 Lab Objectives

By the end of this lab, students will be able to:

- Install the Ultralytics YOLO library
- Load a pre-trained YOLO model
- Upload an image in Google Colab
- Detect objects in the image
- Understand the detection results
- Display the detected image
- Identify detected objects and confidence scores

---

# What is YOLO?

YOLO (**You Only Look Once**) is a real-time object detection algorithm.

Unlike a traditional CNN that only predicts **what object is present**, YOLO predicts:

- What object is present
- Where the object is located
- Confidence score
- Multiple objects simultaneously

---

# Step 1: Install YOLO

Run the following command to install the Ultralytics library.

```python
!pip install ultralytics
```

### Expected Output

```
Successfully installed ultralytics
```

> **Note:** Installation may take a few minutes the first time.

---

# Step 2: Import Required Libraries

```python
from ultralytics import YOLO
import matplotlib.pyplot as plt
from PIL import Image
```

### Explanation

- `YOLO` → Loads the YOLO model.
- `matplotlib` → Displays images.
- `PIL` → Opens image files.

---

# Step 3: Load the Pre-trained YOLO Model

```python
model = YOLO("yolov8n.pt")
```

### What happens?

The first time this code runs:

- Downloads the YOLOv8 Nano model
- Saves it locally
- Loads it into memory

### Why YOLOv8 Nano?

- Small model
- Fast inference
- Beginner-friendly
- Works well on Google Colab

---

# Step 4: Upload an Image

Run the following cell.

```python
from google.colab import files

uploaded = files.upload()
```

A file selection window will appear.

Upload an image such as:

- street.jpg
- traffic.jpg
- classroom.jpg
- bus.jpg

---

# Step 5: Get the Uploaded File Name

```python
image_path = list(uploaded.keys())[0]

print("Uploaded Image:", image_path)
```

### Example Output

```
Uploaded Image: street.jpg
```

---

# Step 6: Display the Uploaded Image

```python
image = Image.open(image_path)

plt.figure(figsize=(8,6))
plt.imshow(image)
plt.axis("off")
plt.show()
```

### Activity

Before running YOLO, answer the following:

1. How many people do you see?
2. How many cars?
3. How many bicycles?
4. How many buses?

Write your answers in your notebook.

---

# Step 7: Perform Object Detection

```python
results = model.predict(
    source=image_path,
    save=True,
    conf=0.5
)
```

### Explanation of Parameters

| Parameter | Description |
|-----------|-------------|
| `source` | Input image |
| `save=True` | Saves the detected image |
| `conf=0.5` | Minimum confidence score (50%) |

---

# Step 8: Display the Detection Result

```python
import glob

result_path = glob.glob("runs/detect/predict/*.jpg")[0]

result_image = Image.open(result_path)

plt.figure(figsize=(10,8))
plt.imshow(result_image)
plt.axis("off")
plt.show()
```

### Observation

Notice that YOLO draws:

- Bounding Boxes
- Object Labels
- Confidence Scores

---

# Step 9: Print Detected Objects

```python
for result in results:
    for box in result.boxes:
        class_id = int(box.cls)
        print(model.names[class_id])
```

### Example Output

```
person
person
car
car
bus
traffic light
bicycle
```

---

# Step 10: Print Confidence Scores

```python
for result in results:
    for box in result.boxes:
        class_id = int(box.cls)
        confidence = float(box.conf)

        print(model.names[class_id], confidence)
```

### Example Output

```
person 0.99
person 0.98
car 0.97
bus 0.95
traffic light 0.92
```

### What does Confidence Score mean?

A confidence score indicates how certain the model is about its prediction.

Example:

| Confidence | Meaning |
|------------|---------|
| 0.99 | Very confident |
| 0.90 | High confidence |
| 0.70 | Moderate confidence |
| 0.50 | Minimum accepted confidence |

---

# Step 11: Print Bounding Box Coordinates

```python
for result in results:
    for box in result.boxes:
        print(box.xyxy)
```

### Example Output

```
tensor([[120.4, 85.6, 320.8, 420.5]])
```

The four values represent:

```
(x1, y1) ------
|              |
|   Object     |
|              |
------ (x2, y2)
```

| Value | Description |
|--------|-------------|
| x1 | Left coordinate |
| y1 | Top coordinate |
| x2 | Right coordinate |
| y2 | Bottom coordinate |

---

# Step 12: Count the Detected Objects

```python
object_count = {}

for result in results:
    for box in result.boxes:
        class_name = model.names[int(box.cls)]
        object_count[class_name] = object_count.get(class_name, 0) + 1

print(object_count)
```

### Example Output

```python
{
    'person': 4,
    'car': 6,
    'bus': 1,
    'traffic light': 2
}
```

---

# Student Exercise 1

Upload another image.

Examples:

- Parking lot
- Classroom
- Shopping mall
- Airport
- Railway station

Answer the following:

1. How many people were detected?
2. How many cars?
3. How many buses?
4. Which object has the highest confidence score?
5. Which object has the lowest confidence score?

---

# Student Exercise 2

Run YOLO on **three different images**.

Complete the following table.

| Image | Persons | Cars | Buses | Bicycles | Confidence Range |
|--------|---------|------|--------|-----------|------------------|
| Image 1 | | | | | |
| Image 2 | | | | | |
| Image 3 | | | | | |

---

# Student Exercise 3

Compare your manual count with YOLO.

| Object | Manual Count | YOLO Count |
|---------|--------------|------------|
| Person | | |
| Car | | |
| Bus | | |
| Bicycle | | |

### Discussion

- Did YOLO miss any objects?
- Did YOLO detect any unexpected objects?
- Why do you think this happened?

---

# Challenge Exercise

Take a photo of your classroom or workplace and upload it.

Use YOLO to detect:

- 👨 People
- 💺 Chairs
- 💻 Laptops
- 🎒 Backpacks
- 🪑 Benches
- 🖥️ Monitors

Create a summary table.

| Object | Count |
|---------|-------|
| Person | |
| Chair | |
| Laptop | |
| Backpack | |
| Monitor | |

---

# Lab Summary

In this lab, you learned how to:

- Install Ultralytics YOLO
- Load a pre-trained YOLO model
- Upload images in Google Colab
- Detect multiple objects
- Display detection results
- Print object names
- Print confidence scores
- Print bounding box coordinates
- Count detected objects

---

# Next Lab

**Lab 06: Real-Time Video Object Detection using YOLO**

```python
results = model.predict(
    source="Video1.mp4",
    imgsz=320,
    conf=0.5,
    save=True
)
```

Display the output video

```python
from IPython.display import Video

Video("output.mp4", embed=True)
```
