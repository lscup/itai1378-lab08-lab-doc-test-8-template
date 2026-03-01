---

## 1. Overview

# Lab 8: Interactive Image Processing Application

Welcome to the Interactive Image Processing Lab. In this lab, you will build an interactive image processing application using OpenCV, Matplotlib, and ipywidgets. You will implement various functionalities such as image browsing, grayscale conversion, brightness adjustment, resizing, rotation, and histogram plotting.

### Objectives

- Build an interactive image processing application.
- Implement image browsing and display.
- Apply image transformations like grayscale conversion, brightness adjustment, resizing, and rotation.
- Visualize image histograms.

### Prerequisites

- Basic understanding of Python programming.
- Familiarity with Jupyter Notebooks.
- Introduction to image processing concepts.

---

## 2. Algorithm/Concept Background

Image processing involves performing operations on images to enhance, transform, or extract information. This lab will cover basic image transformations and display techniques.

Example of grayscale conversion:

```python
import cv2
import numpy as np

# Original RGB image
original_rgb = np.array([[[255, 0, 0], [0, 255, 0]], [[0, 0, 255], [255, 255, 0]]], dtype=np.uint8)

# Convert to grayscale
gray = cv2.cvtColor(original_rgb, cv2.COLOR_RGB2GRAY)

print(gray)
```

| Property | Description |
|----------|-------------|
| Grayscale Conversion | Converts color images to shades of gray |
| Brightness Adjustment | Modifies the intensity of pixels |
| Resizing | Changes the dimensions of the image |
| Rotation | Rotates the image by specified angles |

---

## 3. Your Coding Environment

### Workspace Layout

| Area | What It Does |
|------|--------------|
| Code Editor (left) | Edit your files using the tabbed editor |
| Terminal (right) | See output when you click the **Run** button |
| AI Tutor (chat panel) | Ask your AI Tutor for help — it knows this lab and can guide you step by step |

### Workflow

1. Edit your code in the editor tabs
2. Click **Run** to execute and see output in the terminal
3. When ready, click **Commit** to save your work to GitHub and trigger the autograder
4. A ✅ (green check) or ❌ (red X) will appear showing whether tests passed

Tip: Commit early and often to track your progress!

---

## 4. Project Structure

```plaintext
notebook.ipynb   # YOUR WORK
```

---

## 5. Step-by-Step Implementation

This is the MOST IMPORTANT section — be extremely detailed and spoon-fed.

### Step 1: Import Libraries

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt
from ipywidgets import widgets
from IPython.display import display
import os
```

Explanation: Import all necessary libraries for image processing, plotting, and creating interactive widgets.

### Step 2: Initialize Global Variables

```python
original_bgr, original_rgb, processed_rgb = None, None, None
```

Explanation: Initialize global variables to store image data. These will be used by various functions.

### Step 3: Create Output Areas

```python
msg_out = widgets.Output()
img_out = widgets.Output()
hist_out = widgets.Output()
```

Explanation: Create output areas for displaying messages, images, and histograms.

### Step 4: Define Helper Functions

#### Show Images

```python
def show_images(original_rgb, processed_rgb):
    with img_out:
        img_out.clear_output()
        fig, ax = plt.subplots(1, 2, figsize=(10, 5))
        ax[0].imshow(original_rgb)
        ax[0].set_title('Original Image')
        ax[0].axis('off')
        ax[1].imshow(processed_rgb)
        ax[1].set_title('Processed Image')
        ax[1].axis('off')
        plt.show()
```

Explanation: This function displays the original and processed images side by side.

#### Show Histogram

```python
def show_histogram(processed_rgb):
    with hist_out:
        hist_out.clear_output()
        gray = cv2.cvtColor(processed_rgb, cv2.COLOR_RGB2GRAY)
        plt.figure(figsize=(5, 3))
        plt.hist(gray.ravel(), 256, [0, 256])
        plt.title('Histogram')
        plt.show()
```

Explanation: This function plots the histogram of the processed image.

### Step 5: Create UI Controls

```python
browse_btn = widgets.Button(description='Browse Image')
grayscale_btn = widgets.Button(description='Convert to Grayscale')
brightness_slider = widgets.IntSlider(description='Brightness', min=-100, max=100)
resize_dropdown = widgets.Dropdown(description='Resize', options=[1.0, 0.75, 0.5])
rotate_dropdown = widgets.Dropdown(description='Rotation', options=[0, 90, 180, 270])
histogram_btn = widgets.Button(description='Plot Histogram')
save_btn = widgets.Button(description='Save Image')
```

Explanation: Define UI controls for different functionalities.

### Step 6: Implement Callback Functions

Create functions to handle each UI control's action. Ensure all actions update `processed_rgb` and call `show_images`.

#### Browse Image

```python
def on_browse_image(change):
    from google.colab import files
    uploaded = files.upload()
    for fn in uploaded.keys():
        global original_bgr, original_rgb, processed_rgb
        original_bgr = cv2.imdecode(np.frombuffer(uploaded[fn], np.uint8), cv2.IMREAD_COLOR)
        if original_bgr is not None:
            original_rgb = cv2.cvtColor(original_bgr, cv2.COLOR_BGR2RGB)
            processed_rgb = original_rgb.copy()
            show_images(original_rgb, processed_rgb)
            with msg_out:
                msg_out.clear_output()
                print(f'Loaded {fn}')
```

Explanation: Allows users to upload an image and display it.

### Step 7: Connect Callbacks

```python
browse_btn.on_click(on_browse_image)
grayscale_btn.on_click(on_convert_to_grayscale)
brightness_slider.observe(on_brightness_change, names='value')
resize_dropdown.observe(on_resize, names='value')
rotate_dropdown.observe(on_rotate, names='value')
histogram_btn.on_click(on_plot_histogram)
save_btn.on_click(on_save_image)
```

Explanation: Connect each UI control to its respective callback function.

### Step 8: Create Layout

```python
controls = widgets.VBox([browse_btn, grayscale_btn, brightness_slider, resize_dropdown, rotate_dropdown, histogram_btn, save_btn])
outputs = widgets.VBox([img_out, hist_out])
layout = widgets.HBox([controls, outputs])

display(layout)
msg_out.append_stdout('Please click Browse Image to start.\n')
```

Explanation: Arrange the UI controls and output areas in the display.

### Complete Solution

```python
# All code combined; ensure your implementation matches this.
```

---

## 6. Testing Your Code

### Run Your Code

Click **Run** to execute and check the output.

### Submit for Grading

Click **Commit**, enter a message, and look for ✅ or ❌.

Expected output:

```
Loaded [filename]
Brightness adjusted
Image resized
```

---

## 7. Autograding

| Test | Points | What It Checks |
|------|--------|----------------|
| Syntax Check | 20 | Notebook runs without syntax errors |
| Browse Image Test | 20 | Image loading functionality |
| Grayscale Conversion | 20 | Grayscale conversion works |
| Brightness Adjustment | 20 | Brightness slider affects image |
| Resize Image | 20 | Image resizing functionality |

Total Points: 100

---

## 8. Lab Report

Click the README.md tab and fill in your lab report.

```markdown
# Lab Report

## Student Information
- Name: 
- Date: 

## Key Concepts
- Image Processing

## Tracing/Analysis
- Describe the flow of image data through various transformations.

## Complexity Analysis
| Operation | Complexity |
|-----------|------------|
| Grayscale Conversion | O(N) |
| Brightness Adjustment | O(N) |
| Resizing | O(N * M) |

## Reflection Questions
1. What challenges did you face during image processing?
2. How does brightness adjustment work in terms of pixel manipulation?
3. Explain the importance of histograms in image processing.
```

---

## 9. Submission Checklist

- [ ] All functions implemented
- [ ] Click Run — output matches expected
- [ ] Click Commit — autograder shows green check
- [ ] Lab report completed in README.md
- [ ] Final commit with completed lab report

---

