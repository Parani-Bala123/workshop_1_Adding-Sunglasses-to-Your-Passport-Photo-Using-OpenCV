# Workshop_1: Adding Sunglasses to a Passport Photo Using OpenCV

### Name: Parani Bala M
### Reg.no: 212224230192

## Aim
To develop a Python program using OpenCV to add sunglasses to a passport-size photograph using image processing and masking techniques.

## Objectives
- To understand image processing using OpenCV.
- To load and display images using Python.
- To resize sunglasses according to face dimensions.
- To separate colour and alpha channels from a PNG image.
- To apply image masking and arithmetic operations.
- To overlay sunglasses onto the eye region of a face image.

## Algorithm
1. Import the required libraries: OpenCV, NumPy and Matplotlib.
2. Load the face image and sunglasses PNG image.
3. Resize the sunglasses image to fit the eye region.
4. Separate the colour channels and alpha channel.
5. Create a copy of the original face image.
6. Specify the position of the sunglasses.
7. Extract the eye region from the face image.
8. Create a mask using the alpha channel.
9. Apply masking using `cv2.multiply()`.
10. Combine the masked eye region and sunglasses using `cv2.add()`.
11. Display the final augmented image.

## Program

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt

# Load face image
faceImage = cv2.imread('My_Image.png')
plt.imshow(faceImage[:,:,::-1])
plt.title("Face")

# Load sunglasses image
glassPNG = cv2.imread('sunglass.png', -1)
plt.imshow(glassPNG[:,:,::-1])
plt.title("Sunglasses")

# Resize sunglasses
glassPNG = cv2.resize(glassPNG, (190, 50))

# Separate colour and alpha channels
glassBGR = glassPNG[:,:,0:3]
glassMask1 = glassPNG[:,:,3]

# Create a copy of face image
faceWithGlasses = faceImage.copy()

# Set sunglasses position
x, y = 165, 145
h, w = glassBGR.shape[:2]

# Overlay sunglasses
faceWithGlasses[y:y+h, x:x+w] = glassBGR

# Create 3-channel mask
glassMask = cv2.merge(
    (glassMask1, glassMask1, glassMask1)
)

# Normalize mask
glassMask = np.uint8(glassMask/255)

# Extract eye region
eyeROI = faceImage[135:185, 110:300]

# Apply masking
maskedEye = cv2.multiply(eyeROI, (1-glassMask))
maskedGlass = cv2.multiply(glassBGR, glassMask)

# Combine images
eyeRoiFinal = cv2.add(maskedEye, maskedGlass)

# Display final result
plt.figure(figsize=[15,15])
plt.imshow(eyeRoiFinal[:,:,::-1])
plt.title("Final Augmented Image")
plt.axis('off')
plt.show()
```

### Output:
<img width="1382" height="573" alt="image" src="https://github.com/user-attachments/assets/6709fb00-f340-4043-b9dd-6501b504ef5c" />
<img width="1370" height="376" alt="image" src="https://github.com/user-attachments/assets/df494ddc-02cb-4616-aa99-0f2390db50ce" />
<img width="1372" height="227" alt="image" src="https://github.com/user-attachments/assets/3966a5f5-ecdf-4205-837a-c5a124735ac7" />
<img width="1371" height="478" alt="image" src="https://github.com/user-attachments/assets/68438e1c-1b53-4942-96be-ae035208005d" />
<img width="1381" height="205" alt="image" src="https://github.com/user-attachments/assets/b6e5ff88-4165-4d11-ad16-cd41c78fa759" />
<img width="1386" height="507" alt="image" src="https://github.com/user-attachments/assets/8239cc0b-1ce4-48fa-b3e4-5524aed0098e" />


## Result
Thus, the Python program was successfully executed using OpenCV to add sunglasses to a passport-size photograph using image resizing, alpha channel extraction, masking and arithmetic operations.
