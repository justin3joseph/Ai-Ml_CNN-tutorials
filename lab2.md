# CNN Lab 2: Manual Convolution Calculation

## Objective

Understand how convolution works by manually applying a kernel to an image matrix.

This lab helps students visualize how CNN filters generate feature maps.

---

## Theory

Convolution is the process of sliding a small matrix called a **kernel (filter)** over an image and performing element-wise multiplication followed by summation.

The resulting values form a new matrix called the **feature map**.

---

## Input Image Matrix

Consider the following 3 × 3 image:

```text
1 2 3
4 5 6
7 8 9
```

---

## Kernel (Filter)

Use the following 2 × 2 kernel:

```text
1 0
0 1
```

---

## Step 1: Position the Kernel

Place the kernel on the top-left corner of the image:

```text
Image Area:

1 2
4 5

Kernel:

1 0
0 1
```

---

## Step 2: Multiply Corresponding Elements

```text
(1 × 1) + (2 × 0) + (4 × 0) + (5 × 1)
```

---

## Step 3: Add the Results

```text
1 + 0 + 0 + 5 = 6
```

The first value of the feature map is:

```text
6
```

---

## Step 4: Slide the Kernel Right

```text
Image Area:

2 3
5 6

Kernel:

1 0
0 1
```

Calculation:

```text
(2 × 1) + (3 × 0) + (5 × 0) + (6 × 1)

= 2 + 0 + 0 + 6

= 8
```

---

## Step 5: Slide the Kernel Down

```text
Image Area:

4 5
7 8

Kernel:

1 0
0 1
```

Calculation:

```text
(4 × 1) + (5 × 0) + (7 × 0) + (8 × 1)

= 4 + 0 + 0 + 8

= 12
```

---

## Step 6: Final Position

```text
Image Area:

5 6
8 9

Kernel:

1 0
0 1
```

Calculation:

```text
(5 × 1) + (6 × 0) + (8 × 0) + (9 × 1)

= 5 + 0 + 0 + 9

= 14
```

---

## Final Feature Map

```text
6   8
12 14
```

---

## Visualization

```text
Input Image
┌─────────┐
│1 2 3    │
│4 5 6    │
│7 8 9    │
└─────────┘

      ↓ Convolution

Feature Map
┌───────┐
│6   8  │
│12 14  │
└───────┘
```

---

## Student Activity

Calculate the feature map manually using the following image:

```text
2 4 6
1 3 5
7 8 9
```

Use the same kernel:

```text
1 0
0 1
```

---

## Learning Outcome

After completing this lab, students will understand:

- What convolution means
- How a kernel slides over an image
- How element-wise multiplication works
- How feature maps are generated
- The foundation of CNN feature extraction
