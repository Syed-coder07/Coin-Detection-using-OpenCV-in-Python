## Coin-Detection-using-OpenCV-in-Python

## Aim:

To develop an AI-based image processing system that can automatically detect and count coins in an image using Python and OpenCV, while visualizing all the intermediate processing steps such as grayscale conversion, blurring, edge detection, and contour detection

## OBJECTIVE:

* To apply fundamental computer vision techniques to identify circular objects (coins).
* To understand the use of image preprocessing and feature extraction using OpenCV.
* To display all intermediate outputs to explain how detection is achieved.
* To count and label the number of coins accurately.

## ALGORITHM:

* Start
* Input the image (coins image file).
* Convert the image to grayscale to simplify analysis.
* Apply Gaussian Blur to reduce image noise and smooth edges.
* Apply Canny Edge Detection to find edges of coins.
* Find Contours in the edge-detected image.
* Filter Contours based on area (to remove small noise).
* Draw circles around detected coins and assign serial numbers.
* Count the total number of coins detected.

## Program:

```
import cv2
import numpy as np
import matplotlib.pyplot as plt
import os
image_path = "coin.jpg" 
image = cv2.imread(r"C:\Users\syedf\OneDrive\Documents\DIPT\Coin.png")
if image is None:
    raise FileNotFoundError(f"Image not found at {image_path}")
gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
blurred = cv2.GaussianBlur(gray, (11, 11), 0)
edges = cv2.Canny(blurred, 30, 150)
contours, _ = cv2.findContours(edges.copy(), cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)
output = image.copy()

coin_count = 0
for contour in contours:
    area = cv2.contourArea(contour)
    if area < 300:
        continue

    # Draw contour
    ((x, y), radius) = cv2.minEnclosingCircle(contour)
    if radius > 15:
        coin_count += 1
        cv2.circle(output, (int(x), int(y)), int(radius), (0, 255, 0), 2)
        cv2.putText(output, f"{coin_count}", (int(x - 10), int(y + 10)),
                    cv2.FONT_HERSHEY_SIMPLEX, 0.6, (0, 0, 255), 2)

print("Total coins detected:", count)
print("Total coins detected:", count)

fig, axs = plt.subplots(1, 5, figsize=(20, 6))

axs[0].imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))
axs[0].set_title("Original Image")
axs[0].axis("off")

axs[1].imshow(gray, cmap='gray')
axs[1].set_title("Grayscale Image")
axs[1].axis("off")

axs[2].imshow(blurred, cmap='gray')
axs[2].set_title("Blurred Image")
axs[2].axis("off")

axs[3].imshow(edges, cmap='gray')
axs[3].set_title("Edge Detection (Canny)")
axs[3].axis("off")

axs[4].imshow(cv2.cvtColor(output, cv2.COLOR_BGR2RGB))
axs[4].set_title(f"Detected Coins: {coin_count}")
axs[4].axis("off")

plt.tight_layout()
plt.show()
```

## Output:

## Original Image:

<img width="456" height="522" alt="image" src="https://github.com/user-attachments/assets/ff10031a-ef41-4b3d-969f-6110bd0e6043" />

## Grayscale Image:

<img width="457" height="518" alt="image" src="https://github.com/user-attachments/assets/356190cc-f4e4-40b3-abe6-26783d365769" />

## Blurred Image:

<img width="458" height="517" alt="image" src="https://github.com/user-attachments/assets/aab9b0eb-9274-4d55-8d17-4a2ba136737d" />

## Cany Edge Detection Image:

<img width="455" height="520" alt="image" src="https://github.com/user-attachments/assets/80a634a5-c3cd-41bf-8822-6b7e23027f6c" />

## Detected Coins:

<img width="450" height="528" alt="image" src="https://github.com/user-attachments/assets/dda6c6b7-ce6a-4572-954c-e600e2461d9f" />

## Result:

The system successfully detected and counted all coins in the given image.
