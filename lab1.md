# CNN Lab 1: Understanding Image Filters (Feature Extraction)

## Objective

Learn how CNNs extract features from images using filters (kernels).

In this lab, students will:

- Upload an image
- Apply an edge detection filter
- Observe how image features are extracted
- Understand the basic concept behind Convolutional Neural Networks (CNNs)

---

## Step 1: Open Google Colab

Open Google Colab:

https://colab.research.google.com

Create a **New Notebook**.

---

## Step 2: Upload an Image

Run the following code:

```python
from google.colab import files

uploaded = files.upload()
```

A file browser will appear.

Upload an image such as:

```text
cat.jpg
```

After uploading, you should see something similar to:

```text
Saving cat.jpg to cat.jpg
```

---

## Step 3: Apply Edge Detection Filter

Run the following code:

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt

# Read image in grayscale
img = cv2.imread('cat.jpg', 0)

# Edge Detection Kernel
kernel = np.array([
    [-1, -1, -1],
    [-1,  8, -1],
    [-1, -1, -1]
])

# Apply convolution
filtered = cv2.filter2D(img, -1, kernel)

# Display images
plt.figure(figsize=(10, 5))

plt.subplot(1, 2, 1)
plt.imshow(img, cmap='gray')
plt.title("Original Image")
plt.axis("off")

plt.subplot(1, 2, 2)
plt.imshow(filtered, cmap='gray')
plt.title("Edge Detection")
plt.axis("off")

plt.show()
```

---

## Step 4: Understanding the Output

### Original Image

The original image contains all details, colors, textures, and objects.

### Edge Detection Output

The edge detection filter highlights boundaries and removes less important information.

### How CNN Uses Filters

CNN processes images using filters (kernels) to extract important features.

```text
Input Image
      ↓
Filter / Kernel
      ↓
Feature Map
      ↓
Edges
Shapes
Textures
Patterns
```

### Observation

Compare the original image and the filtered image:

- Which areas became brighter?
- Which details disappeared?
- Can you identify the object using only its edges?

### Learning Outcome

After completing this lab, students will understand:

- What a filter (kernel) is
- How convolution works
- How edge detection is performed
- How CNN extracts features from images
- Why feature extraction is important before classification
