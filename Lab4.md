# CNN Lab 4: Understanding Max Pooling

## Objective

Learn how Max Pooling reduces the size of a feature map while preserving the most important information.

---

## Theory

After convolution and ReLU, CNNs often apply a process called **Pooling**.

Pooling helps to:

- Reduce image dimensions
- Reduce computation
- Reduce memory usage
- Preserve important features
- Prevent overfitting

The most common pooling method is **Max Pooling**.

---

## What is Max Pooling?

Max Pooling selects the **largest value** from a small region of the feature map.

For example, in a 2 × 2 region:

```text
1 5
7 9
```

The maximum value is:

```text
9
```

Therefore, the output becomes:

```text
9
```

---

## Input Feature Map

Consider the following 4 × 4 feature map:

```text
1 5 3 2
7 9 4 1
2 8 6 3
1 2 5 4
```

---

## Step 1: Apply a 2 × 2 Pooling Window

Divide the feature map into 2 × 2 regions.

### Region 1

```text
1 5
7 9
```

Maximum value:

```text
9
```

---

### Region 2

```text
3 2
4 1
```

Maximum value:

```text
4
```

---

### Region 3

```text
2 8
1 2
```

Maximum value:

```text
8
```

---

### Region 4

```text
6 3
5 4
```

Maximum value:

```text
6
```

---

## Step 2: Construct the Output Feature Map

Collect all maximum values:

```text
9 4
8 6
```

---

## Final Output

```text
Input Feature Map

1 5 3 2
7 9 4 1
2 8 6 3
1 2 5 4

        ↓ Max Pooling (2 × 2)

9 4
8 6
```

---

## Visualization

```text
Input Size

4 × 4

        ↓ Max Pooling

Output Size

2 × 2
```

Pooling reduces the dimensions while keeping the strongest features.

---

## Python Implementation

```python
import tensorflow as tf
import numpy as np

feature_map = np.array([
    [
        [[1], [5], [3], [2]],
        [[7], [9], [4], [1]],
        [[2], [8], [6], [3]],
        [[1], [2], [5], [4]]
    ]
])

pool = tf.keras.layers.MaxPooling2D(pool_size=(2,2))

output = pool(feature_map)

print(output.numpy())
```

---

## Expected Output

```text
[[[[9]
   [4]]

  [[8]
   [6]]]]
```

---

## Why CNN Uses Pooling

### 1. Reduces Computation

Smaller feature maps require fewer calculations.

---

### 2. Preserves Important Features

The strongest features are retained.

Example:

```text
1 5
7 9

→ Keep only 9
```

---

### 3. Reduces Memory Usage

Smaller feature maps require less storage.

---

### 4. Helps Prevent Overfitting

The model learns general patterns instead of memorizing every pixel.

---

## Student Activity

Perform Max Pooling manually on the following feature map:

```text
4 8 2 1
6 7 3 5
9 1 4 2
3 8 6 7
```

Use:

```text
Pool Size = 2 × 2
Stride = 2
```

Calculate the output feature map.

---

## Challenge Activity

Modify the Python code and test the following feature map:

```python
feature_map = np.array([
    [
        [[4], [8], [2], [1]],
        [[6], [7], [3], [5]],
        [[9], [1], [4], [2]],
        [[3], [8], [6], [7]]
    ]
])
```

Observe the pooled output.

---

## Learning Outcome

After completing this lab, students will understand:

- What Max Pooling is
- How pooling reduces feature map dimensions
- How important features are preserved
- Why CNNs use pooling layers
- The role of pooling in image classification
