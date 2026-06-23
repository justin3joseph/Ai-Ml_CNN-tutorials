# Bonus Lab: Experimenting with Different CNN Filters

## Objective

Explore how different filters (kernels) affect an image and understand how CNNs use filters to extract various features.

---

## Instructions

Use the same code from **Lab 1** and replace only the `kernel` variable with the kernels given below.

Observe the output image and compare the results.

---

# 1. Vertical Edge Detection Filter

## Kernel

```python
kernel = np.array([
    [-1, 0, 1],
    [-1, 0, 1],
    [-1, 0, 1]
])
```

## Purpose

Detects vertical edges in an image.

### Example

```text
Original Image

|   |
|   |
|   |

After Filtering

Vertical boundaries become brighter.
```

## Observation Questions

- Which vertical objects become more visible?
- Are horizontal edges highlighted?

---

# 2. Horizontal Edge Detection Filter

## Kernel

```python
kernel = np.array([
    [-1, -1, -1],
    [ 0,  0,  0],
    [ 1,  1,  1]
])
```

## Purpose

Detects horizontal edges in an image.

### Example

```text
Original Image

-----------
-----------
-----------

After Filtering

Horizontal boundaries become brighter.
```

## Observation Questions

- Which horizontal structures become clearer?
- Are vertical edges highlighted?

---

# 3. Blur Filter

## Kernel

```python
kernel = np.ones((3,3)) / 9
```

## Purpose

Smooths the image and reduces noise.

### Example

```text
Before

Sharp details visible

After

Details become smoother
```

## Observation Questions

- Does the image appear softer?
- What happens to fine details?
- Are edges still sharp?

---

# 4. Sharpen Filter

## Kernel

```python
kernel = np.array([
    [ 0, -1,  0],
    [-1,  5, -1],
    [ 0, -1,  0]
])
```

## Purpose

Enhances edges and image details.

### Example

```text
Before

Normal Image

After

Edges become more prominent
```

## Observation Questions

- Which details become clearer?
- Does the image look more focused?
- Are edges easier to identify?

---

# Comparison Activity

Apply all four filters to the same image and record your observations.

| Filter | Purpose | Result |
|----------|----------|----------|
| Vertical Edge | Detect vertical boundaries | |
| Horizontal Edge | Detect horizontal boundaries | |
| Blur | Reduce noise and smooth image | |
| Sharpen | Enhance details and edges | |

---

# Discussion

### Why does CNN use multiple filters?

A single filter can only detect one type of feature.

For example:

```text
Filter 1 → Vertical Edges

Filter 2 → Horizontal Edges

Filter 3 → Corners

Filter 4 → Textures

Filter 5 → Shapes
```

CNN combines the outputs from many filters to understand the image.

---

# CNN Feature Extraction Pipeline

```text
Input Image
      ↓
Multiple Filters
      ↓
Feature Maps
      ↓
Edges
Corners
Textures
Shapes
Patterns
      ↓
Object Recognition
```

---

# Learning Outcome

After completing this bonus lab, students will understand:

- Different filters extract different features
- CNN uses multiple filters simultaneously
- Filters help identify edges, textures, and patterns
- Feature extraction is the first step in image recognition
- Multiple feature maps are combined to identify objects
