# Lab 01: Hand Signal Recognition using OpenCV and MediaPipe

## 🎯 Objective

In this lab, students will learn how to:

- Access a webcam using OpenCV
- Detect a hand using Google's MediaPipe
- Identify 21 hand landmarks
- Count the number of raised fingers
- Recognize simple hand gestures
- Display the detected gesture in real time

---

# Introduction

Hand Gesture Recognition is a Computer Vision technique that enables computers to understand human hand movements.

Instead of using a mouse or keyboard, users can control applications using their hands.

Some real-world applications include:

- ✋ Contactless Interfaces
- 🎮 Gesture Controlled Games
- 🖱️ Virtual Mouse
- 🎨 Air Drawing
- 🤖 Robot Control
- 📽️ Presentation Controller
- 🔊 Volume Control
- 🤟 Sign Language Recognition

---

# Software Requirements

- Python 3.10+
- OpenCV
- MediaPipe

---

# Install Required Libraries

```bash
pip install opencv-python
pip install mediapipe
```

or

```bash
pip install opencv-python mediapipe
```

---

# Project Structure

```
HandSignalRecognition/
│
├── detector.py
└── README.md
```

---

# Step 1 – Import Required Libraries

```python
import cv2
import mediapipe as mp
```

## Explanation

### OpenCV (`cv2`)

OpenCV is an open-source Computer Vision library.

It provides functions to

- Open webcam
- Read images
- Process video
- Draw text
- Draw shapes
- Display images

### MediaPipe (`mediapipe`)

MediaPipe is Google's AI framework.

It contains pretrained models for

- Hand Detection
- Face Detection
- Face Mesh
- Pose Detection
- Object Tracking

We will use the **Hand Detection Model**.

---

# Step 2 – Load the Hand Detection Model

```python
mp_hands = mp.solutions.hands
```

## Explanation

MediaPipe contains several AI solutions.

```
MediaPipe
│
├── Hands
├── Face Detection
├── Pose
├── Face Mesh
└── Selfie Segmentation
```

This line selects the **Hands** module.

---

# Step 3 – Create the Hand Detector

```python
hands = mp_hands.Hands(
    static_image_mode=False,
    max_num_hands=1,
    min_detection_confidence=0.7,
    min_tracking_confidence=0.7
)
```

## Explanation

### static_image_mode=False

Indicates that input comes from a live video.

MediaPipe detects the hand once and then tracks it efficiently.

If set to `True`, every frame is processed as an independent image, which is slower.

---

### max_num_hands=1

Detect only one hand.

Examples:

```
1 → One hand

2 → Two hands
```

---

### min_detection_confidence=0.7

Minimum confidence required before accepting a detected hand.

```
Detected Confidence = 95%

95 > 70

Hand Accepted
```

---

### min_tracking_confidence=0.7

After detection, MediaPipe tracks the hand.

If tracking confidence falls below 70%, MediaPipe performs hand detection again.

---

# Step 4 – Drawing Utility

```python
mp_draw = mp.solutions.drawing_utils
```

## Explanation

This utility automatically draws

- Hand landmarks
- Connection lines

Without it, we would have to manually draw every point.

---

# Step 5 – Open Webcam

```python
cap = cv2.VideoCapture(0)
```

## Explanation

Open webcam number 0.

```
0 → Laptop Camera

1 → USB Camera

2 → External Camera
```

---

# Step 6 – Fingertip Landmark IDs

```python
tip_ids = [4,8,12,16,20]
```

## Explanation

MediaPipe assigns an ID to every landmark.

```
Thumb Tip      → 4

Index Tip      → 8

Middle Tip     → 12

Ring Tip       → 16

Little Tip     → 20
```

These IDs help determine whether a finger is open or closed.

---

# Step 7 – Start Infinite Loop

```python
while True:
```

## Explanation

The webcam continuously captures images.

```
Frame 1

↓

Frame 2

↓

Frame 3

↓

Frame 4

↓

...
```

---

# Step 8 – Capture Webcam Frame

```python
success, frame = cap.read()
```

## Explanation

The webcam returns

```
success

True if image captured
```

and

```
frame

Captured image
```

---

# Step 9 – Flip the Image

```python
frame = cv2.flip(frame,1)
```

## Explanation

Without flipping

```
Raise Right Hand

↓

Appears Left
```

After flipping

```
Mirror View
```

This feels natural for users.

---

# Step 10 – Convert BGR to RGB

```python
rgb = cv2.cvtColor(frame, cv2.COLOR_BGR2RGB)
```

## Explanation

OpenCV stores images as

```
Blue

Green

Red
```

MediaPipe expects

```
Red

Green

Blue
```

Therefore, conversion is necessary.

---

# Step 11 – Detect Hands

```python
results = hands.process(rgb)
```

## Explanation

MediaPipe analyzes the RGB image.

Output includes

- Hand Detection
- Landmark Positions
- Left/Right Hand
- Confidence Scores

---

# Step 12 – Initialize Variables

```python
finger_count = 0
gesture = "No Hand"
```

## Explanation

Default values before processing each frame.

---

# Step 13 – Check if a Hand Exists

```python
if results.multi_hand_landmarks:
```

## Explanation

If a hand is detected,

MediaPipe returns all 21 landmarks.

Otherwise,

```
None
```

---

# Step 14 – Process Every Detected Hand

```python
for hand_landmarks in results.multi_hand_landmarks:
```

## Explanation

Even when detecting one hand,

MediaPipe returns a list.

If two hands are enabled,

both hands are processed one after another.

---

# Step 15 – Draw Landmarks

```python
mp_draw.draw_landmarks(
    frame,
    hand_landmarks,
    mp_hands.HAND_CONNECTIONS
)
```

## Explanation

Automatically draws

- 21 Landmark Points
- Connection Lines

Example

```
          8
         ●
        /
       ● 7
      /
     ● 6
    /
   ● 5

Thumb

4 ●
```

---

# Step 16 – Get Landmark Coordinates

```python
landmarks = hand_landmarks.landmark
```

Each landmark contains

```python
landmark.x
landmark.y
landmark.z
```

Example

```python
landmarks[8].x
```

returns the X coordinate of the Index Finger Tip.

---

# Step 17 – Finger Detection Logic

### Thumb

```python
if landmarks[tip_ids[0]].x < landmarks[tip_ids[0]-1].x:
    fingers.append(1)
else:
    fingers.append(0)
```

### Explanation

The thumb bends sideways.

Therefore,

X coordinate is compared.

---

### Remaining Fingers

```python
for tip in tip_ids[1:]:

    if landmarks[tip].y < landmarks[tip-2].y:
        fingers.append(1)
    else:
        fingers.append(0)
```

### Explanation

Each finger is compared with its lower joint.

Example

```
5

6

7

8 ← Finger Tip
```

If

```
Tip Y < Joint Y
```

Finger is OPEN.

Otherwise,

Finger is CLOSED.

Remember

Image coordinates start from the top.

```
Top

Y = 0

↓

↓

↓

Bottom

Large Y
```

Smaller Y means higher position.

---

# Step 18 – Count Raised Fingers

```python
finger_count = sum(fingers)
```

Example

```python
fingers = [1,1,0,1,0]
```

Output

```
3
```

---

# Step 19 – Gesture Recognition

```python
if finger_count == 0:
    gesture = "FIST"

elif finger_count == 1:
    gesture = "ONE"

elif finger_count == 2:
    gesture = "TWO"

elif finger_count == 3:
    gesture = "THREE"

elif finger_count == 4:
    gesture = "FOUR"

elif finger_count == 5:
    gesture = "PALM"
```

## Explanation

The number of raised fingers determines the displayed gesture.

---

# Step 20 – Display Gesture

```python
cv2.putText(
    frame,
    f'Gesture: {gesture}',
    (20,50),
    cv2.FONT_HERSHEY_SIMPLEX,
    1,
    (0,255,0),
    2
)
```

Displays the detected gesture on the webcam.

---

# Step 21 – Display Finger Count

```python
cv2.putText(
    frame,
    f'Fingers: {finger_count}',
    (20,90),
    cv2.FONT_HERSHEY_SIMPLEX,
    1,
    (255,0,0),
    2
)
```

Displays the number of raised fingers.

---

# Step 22 – Show Video

```python
cv2.imshow("Hand Signal Recognition", frame)
```

Displays the processed webcam feed.

---

# Step 23 – Exit Program

```python
if cv2.waitKey(1) & 0xFF == 27:
    break
```

ESC Key exits the program.

```
ASCII Code

ESC = 27
```

---

# Step 24 – Release Resources

```python
cap.release()
cv2.destroyAllWindows()
```

Closes the webcam and destroys all OpenCV windows.

---

# Complete Program

```python
import cv2
import mediapipe as mp

mp_hands = mp.solutions.hands

hands = mp_hands.Hands(
    static_image_mode=False,
    max_num_hands=1,
    min_detection_confidence=0.7,
    min_tracking_confidence=0.7
)

mp_draw = mp.solutions.drawing_utils

cap = cv2.VideoCapture(0)

tip_ids = [4,8,12,16,20]

while True:

    success, frame = cap.read()

    if not success:
        break

    frame = cv2.flip(frame,1)

    rgb = cv2.cvtColor(frame, cv2.COLOR_BGR2RGB)

    results = hands.process(rgb)

    finger_count = 0
    gesture = "No Hand"

    if results.multi_hand_landmarks:

        for hand_landmarks in results.multi_hand_landmarks:

            mp_draw.draw_landmarks(
                frame,
                hand_landmarks,
                mp_hands.HAND_CONNECTIONS
            )

            landmarks = hand_landmarks.landmark

            fingers = []

            if landmarks[tip_ids[0]].x < landmarks[tip_ids[0]-1].x:
                fingers.append(1)
            else:
                fingers.append(0)

            for tip in tip_ids[1:]:

                if landmarks[tip].y < landmarks[tip-2].y:
                    fingers.append(1)
                else:
                    fingers.append(0)

            finger_count = sum(fingers)

            if finger_count == 0:
                gesture = "FIST"

            elif finger_count == 1:
                gesture = "ONE"

            elif finger_count == 2:
                gesture = "TWO"

            elif finger_count == 3:
                gesture = "THREE"

            elif finger_count == 4:
                gesture = "FOUR"

            elif finger_count == 5:
                gesture = "PALM"

    cv2.putText(
        frame,
        f'Gesture: {gesture}',
        (20,50),
        cv2.FONT_HERSHEY_SIMPLEX,
        1,
        (0,255,0),
        2
    )

    cv2.putText(
        frame,
        f'Fingers: {finger_count}',
        (20,90),
        cv2.FONT_HERSHEY_SIMPLEX,
        1,
        (255,0,0),
        2
    )

    cv2.imshow("Hand Signal Recognition", frame)

    if cv2.waitKey(1) & 0xFF == 27:
        break

cap.release()
cv2.destroyAllWindows()
```

---

# Expected Output

```
Gesture : PALM

Fingers : 5
```

```
Gesture : FIST

Fingers : 0
```

```
Gesture : TWO

Fingers : 2
```

---

# Exercises

1. Detect both hands simultaneously.
2. Display Left Hand and Right Hand labels.
3. Recognize the 👍 Thumbs Up gesture.
4. Recognize the ✌ Victory gesture.
5. Change the text color based on the detected gesture.
6. Display FPS (Frames Per Second).
7. Save a screenshot when five fingers are detected.

---

# Viva Questions

1. What is OpenCV?
2. What is MediaPipe?
3. Why is RGB conversion required?
4. Why do we flip the webcam image?
5. What are hand landmarks?
6. How many landmarks does MediaPipe detect?
7. Why is the thumb detected using the X-axis?
8. Why are the other fingers detected using the Y-axis?
9. What is `cv2.putText()` used for?
10. Why is `cap.release()` important?

---

# Conclusion

In this lab, we successfully built a real-time hand gesture recognition system using OpenCV and MediaPipe. We learned how to capture video from a webcam, detect a hand, identify its 21 landmarks, count raised fingers, recognize basic gestures, and display the results in real time. This project provides a foundation for more advanced applications such as virtual mouse control, air drawing, sign language recognition, and gesture-controlled automation.
