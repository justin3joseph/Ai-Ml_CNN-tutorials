# CNN Lab 5: Handwritten Digit Recognition using MNIST

## Objective

Build a Convolutional Neural Network (CNN) that can recognize handwritten digits (0–9) using the MNIST dataset.

---

# What is MNIST?

MNIST is a dataset containing:

- 60,000 training images
- 10,000 testing images
- Handwritten digits from 0 to 9
- Image size: 28 × 28 pixels

Example:

```text
Digit 0
 ####
#    #
#    #
 ####

Digit 7
######
    #
   #
  #
 #
```

---

# CNN Workflow

```text
MNIST Images
      ↓
Convolution Layer
      ↓
Feature Extraction
      ↓
ReLU Activation
      ↓
Max Pooling
      ↓
Flatten
      ↓
Dense Layer
      ↓
Digit Prediction
```

---

# Complete Program

```python
from tensorflow.keras.datasets import mnist
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Conv2D, MaxPooling2D
from tensorflow.keras.layers import Flatten, Dense
import matplotlib.pyplot as plt

# Load MNIST dataset
(X_train, y_train), (X_test, y_test) = mnist.load_data()

# Normalize and reshape images
X_train = X_train.reshape(-1, 28, 28, 1) / 255.0
X_test = X_test.reshape(-1, 28, 28, 1) / 255.0

# Build CNN Model
model = Sequential([
    Conv2D(
        32,
        (3,3),
        activation='relu',
        input_shape=(28,28,1)
    ),

    MaxPooling2D((2,2)),

    Flatten(),

    Dense(
        128,
        activation='relu'
    ),

    Dense(
        10,
        activation='softmax'
    )
])

# Compile Model
model.compile(
    optimizer='adam',
    loss='sparse_categorical_crossentropy',
    metrics=['accuracy']
)

# Train Model
model.fit(
    X_train,
    y_train,
    epochs=5
)

# Evaluate Model
model.evaluate(
    X_test,
    y_test
)

# Display Sample Image
plt.imshow(
    X_test[0].reshape(28,28),
    cmap='gray'
)

plt.title("Test Image")
plt.axis("off")
plt.show()

# Predict Digit
prediction = model.predict(
    X_test[0].reshape(1,28,28,1)
)

print("Predicted Digit:", prediction.argmax())
print("Actual Digit:", y_test[0])
```

---

# Step-by-Step Explanation

## Step 1: Import Required Libraries

```python
from tensorflow.keras.datasets import mnist
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Conv2D, MaxPooling2D
from tensorflow.keras.layers import Flatten, Dense
import matplotlib.pyplot as plt
```

### Purpose

Import required modules.

| Module | Purpose |
|----------|----------|
| mnist | Load dataset |
| Sequential | Create CNN model |
| Conv2D | Convolution layer |
| MaxPooling2D | Pooling layer |
| Flatten | Convert matrix to vector |
| Dense | Neural network layer |
| matplotlib | Display images |

---

## Step 2: Load Dataset

```python
(X_train, y_train), (X_test, y_test) = mnist.load_data()
```

### Purpose

Load handwritten digit images.

### Output

```text
Training Images : 60000
Testing Images  : 10000
```

---

### Example

```text
X_train[0]
```

contains:

```text
Image of digit 5
```

and

```text
y_train[0]
```

contains:

```text
5
```

---

## Step 3: Reshape Images

```python
X_train = X_train.reshape(-1, 28, 28, 1)
X_test = X_test.reshape(-1, 28, 28, 1)
```

### Why?

Current shape:

```text
60000 × 28 × 28
```

CNN expects:

```text
60000 × 28 × 28 × 1
```

where:

```text
1 = Number of channels
```

---

### Channel Meaning

```text
Grayscale Image = 1 Channel

Color Image = 3 Channels
             (R,G,B)
```

---

## Step 4: Normalize Pixel Values

```python
/ 255.0
```

### Why?

Original pixels:

```text
0 → 255
```

Converted to:

```text
0.0 → 1.0
```

Example:

```text
255 → 1.0

128 → 0.50

0 → 0.0
```

This helps CNN train faster.

---

# Step 5: Build CNN

```python
model = Sequential([
```

Creates a layer-by-layer CNN.

---

## Convolution Layer

```python
Conv2D(
    32,
    (3,3),
    activation='relu',
    input_shape=(28,28,1)
)
```

### Meaning

```text
32 Filters

Filter Size = 3×3

Activation = ReLU
```

---

### Process

```text
Input Image
      ↓
Filter 1
      ↓
Feature Map 1

Filter 2
      ↓
Feature Map 2

...

Filter 32
      ↓
Feature Map 32
```

CNN learns these filters automatically.

---

## Max Pooling Layer

```python
MaxPooling2D((2,2))
```

### Purpose

Reduce image size.

Example:

```text
1 5
7 9
```

Output:

```text
9
```

---

### Benefit

```text
Less Memory

Less Computation

Keep Important Features
```

---

## Flatten Layer

```python
Flatten()
```

### Purpose

Convert matrix into a single vector.

Example:

Before:

```text
2 × 2 × 32
```

After:

```text
128 Numbers
```

---

## Dense Layer

```python
Dense(
    128,
    activation='relu'
)
```

### Purpose

Learn relationships between extracted features.

Think of this as the decision-making layer.

---

## Output Layer

```python
Dense(
    10,
    activation='softmax'
)
```

### Why 10?

Digits:

```text
0
1
2
3
4
5
6
7
8
9
```

Total:

```text
10 Classes
```

---

### Softmax Output

```text
Digit 0 : 0.01

Digit 1 : 0.02

Digit 2 : 0.05

Digit 7 : 0.95

Digit 8 : 0.01
```

Highest probability:

```text
Digit 7
```

---

# Step 6: Compile Model

```python
model.compile(
    optimizer='adam',
    loss='sparse_categorical_crossentropy',
    metrics=['accuracy']
)
```

### Optimizer

```python
adam
```

Updates weights automatically.

---

### Loss Function

```python
sparse_categorical_crossentropy
```

Measures prediction error.

---

### Accuracy

Shows how many predictions are correct.

Example:

```text
98%
```

---

# Step 7: Train Model

```python
model.fit(
    X_train,
    y_train,
    epochs=5
)
```

### Meaning

Train using:

```text
60000 Images
```

for:

```text
5 Complete Iterations
```

---

### Learning Process

```text
Image
  ↓
Prediction
  ↓
Compare With Label
  ↓
Calculate Error
  ↓
Adjust Weights
  ↓
Learn
```

Repeated thousands of times.

---

# Step 8: Evaluate Model

```python
model.evaluate(
    X_test,
    y_test
)
```

### Purpose

Test on unseen images.

Example Output:

```text
Accuracy = 98%
```

---

# Step 9: Display Test Image

```python
plt.imshow(
    X_test[0].reshape(28,28),
    cmap='gray'
)
```

Display first test image.

---

# Step 10: Predict Digit

```python
prediction = model.predict(
    X_test[0].reshape(1,28,28,1)
)
```

CNN analyzes image and generates probabilities.

Example:

```text
Digit 0 = 0.001

Digit 1 = 0.002

Digit 7 = 0.980

Digit 8 = 0.003
```

---

# Step 11: Find Highest Probability

```python
prediction.argmax()
```

Returns:

```text
7
```

because:

```text
0.980 is the highest probability.
```

---

# Step 12: Compare with Actual Answer

```python
print("Predicted Digit:", prediction.argmax())
print("Actual Digit:", y_test[0])
```

Example:

```text
Predicted Digit: 7
Actual Digit: 7
```

---

# Final CNN Architecture

```text
Input Image (28×28×1)
           ↓
Conv2D (32 Filters)
           ↓
ReLU
           ↓
Max Pooling
           ↓
Flatten
           ↓
Dense (128 Neurons)
           ↓
Dense (10 Neurons)
           ↓
Predicted Digit
```

# Learning Outcome

After completing this lab, students will understand:

- What CNN is
- How convolution extracts features
- Why ReLU is used
- How pooling reduces dimensions
- How flatten works
- How dense layers classify data
- How CNN predicts handwritten digits
- End-to-end image classification using deep learning
