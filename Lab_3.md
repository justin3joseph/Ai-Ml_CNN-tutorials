# CNN Lab 3: Understanding ReLU Activation Function

## Objective

Learn how the ReLU (Rectified Linear Unit) activation function works and why it is used in CNNs.

---

## Theory

After convolution, the feature map may contain positive and negative values.

Example:

```text
-4   2
-1   8
```

Negative values often represent less useful information.

CNNs use the ReLU activation function to remove negative values.

---

## ReLU Formula

```text
ReLU(x) = max(0, x)
```

This means:

```text
If x > 0  → Keep the value

If x < 0  → Replace with 0
```

---

## Input Feature Map

```text
-4   2
-1   8
```

---

## Step 1: Apply ReLU

For each value:

```text
ReLU(-4) = 0

ReLU(2) = 2

ReLU(-1) = 0

ReLU(8) = 8
```

---

## Output After ReLU

```text
0   2
0   8
```

---

## Python Implementation

```python
import numpy as np

feature_map = np.array([
    [-4, 2],
    [-1, 8]
])

relu_output = np.maximum(0, feature_map)

print("Original Feature Map:")
print(feature_map)

print("\nAfter ReLU:")
print(relu_output)
```

---

## Expected Output

```text
Original Feature Map:

[[-4  2]
 [-1  8]]

After ReLU:

[[0 2]
 [0 8]]
```

---

## Visualization

```text
Feature Map

-4   2
-1   8

      ↓ ReLU

0    2
0    8
```

---

## Why CNN Uses ReLU

### 1. Removes Negative Values

```text
Negative values become zero.
```

---

### 2. Introduces Non-Linearity

Without ReLU:

```text
CNN behaves like a simple mathematical equation.
```

With ReLU:

```text
CNN can learn complex patterns and objects.
```

---

### 3. Faster Training

ReLU is computationally simple:

```text
max(0, x)
```

This helps CNN train efficiently.

---

## Student Activity

Apply ReLU manually to:

```text
-5   3   1
 2  -7   4
-2   6   8
```

Write the resulting matrix.

---

## Challenge Activity

Using Python, apply ReLU to:

```python
feature_map = np.array([
    [-5, 3, 1],
    [2, -7, 4],
    [-2, 6, 8]
])
```

Display both input and output matrices.

---

## Learning Outcome

After completing this lab, students will understand:

- What an activation function is
- Why ReLU is used in CNNs
- How negative values are removed
- How non-linearity helps neural networks learn
- The role of ReLU in deep learning models
