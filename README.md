# Image-Handling-and-Pixel-Transformations-Using-OpenCV 

## AIM:
Write a Python program using OpenCV that performs the following tasks:

1) Read and Display an Image.  
2) Adjust the brightness of an image.  
3) Modify the image contrast.  
4) Generate a third image using bitwise operations.

## Software Required:a
- Anaconda - Python 3.7
- Jupyter Notebook (for interactive development and execution)

## Algorithm:
### Step 1:
Load an image from your local directory and display it.

### Step 2:
Create a matrix of ones (with data type float64) to adjust brightness.

### Step 3:
Create brighter and darker images by adding and subtracting the matrix from the original image.  
Display the original, brighter, and darker images.

### Step 4:
Modify the image contrast by creating two higher contrast images using scaling factors of 1.1 and 1.2 (without overflow fix).  
Display the original, lower contrast, and higher contrast images.

### Step 5:
Split the image (boy.jpg) into B, G, R components and display the channels

## Program Developed By:
- **Name:** Dhanussh Elango
- **Register Number:** 212224040069

  ### Ex. No. 01

#### 1. Read the image ('Eagle_in_Flight.jpg') using OpenCV imread() as a grayscale image.
```python
# Import libraries
import cv2
import numpy as np
import matplotlib.pyplot as plt
img = cv2.imread('Eagle_in_Flight.jpg', cv2.IMREAD_GRAYSCALE)

```

#### 2. Print the image width, height & Channel.
```python
img.shape
```

#### 3. Display the image using matplotlib imshow().
```python
plt.imshow(img, cmap='gray')
plt.title("Grayscale Eagle")
plt.axis("off")
plt.show()
```

#### 4. Save the image as a PNG file using OpenCV imwrite().
```python
cv2.imwrite("Eagle_in_Flight_gray.png", img)
```

#### 5. Read the saved image above as a color image using cv2.cvtColor().
```python
gray_img=cv2.imread('Eagle_in_Flight.jpg')
color_img = cv2.cvtColor(gray_img, cv2.COLOR_BGR2RGB)
```

#### 6. Display the Colour image using matplotlib imshow() & Print the image width, height & channel.
```python
plt.imshow(color_img)
plt.show()
img.shape
```

#### 7. Crop the image to extract any specific (Eagle alone) object from the image.
```python
crop = color_img[20:430,200:550] 
plt.imshow(crop)
plt.title("Cropped Region")
plt.axis("off")
plt.show()
crop.shape
```

#### 8. Resize the image up by a factor of 2x.
```python
res= cv2.resize(crop,(200*2, 200*2))

```

#### 9. Flip the cropped/resized image horizontally.
```python
flip= cv2.flip(res,1)
plt.imshow(flip)
plt.title("Flipped Horizontally")
plt.axis("off")
plt.show()
```

#### 10. Read in the image ('Apollo-11-launch.jpg').
```python
img2=cv2.imread("Apollo-11-launch.jpg")

```

#### 11. Add the following text to the dark area at the bottom of the image (centered on the image):
```python
text = 'Apollo 11 Saturn V Launch, July 16, 1969'
font_face = cv2.FONT_HERSHEY_PLAIN
text = 'Apollo 11 Saturn V Launch, July 16, 1969'
font_face = cv2.FONT_HERSHEY_PLAIN
text = cv2.putText(img2, "Apollo 11 Saturn V Launch, July 16, 1969", (300, 700),cv2.FONT_HERSHEY_SIMPLEX, 1, (255, 255, 255), 2)  
plt.imshow(text, cmap='gray')  
plt.title("New image")
plt.show()  
```

#### 12. Draw a magenta rectangle that encompasses the launch tower and the rocket.
```python
rect_color = "magenta"
# rect_color = magenta
annoted_img = cv2.rectangle(img2, (400, 50), (800, 650), (255,0,255), 3)  
```

#### 13. Display the final annotated image.
```python
plt.imshow(annoted_img)
```

#### 14. Read the image ('Boy.jpg').
```python
img3 = cv2.imread("boy.jpg",1)
img3_rgb = cv2.cvtColor(img3,cv2.COLOR_BGR2RGB)

```

#### 15. Adjust the brightness of the image.
```python
# Create a matrix of ones (with data type float64)
# matrix_ones = 
m = np.ones(img3_rgb.shape, dtype="uint8") * 50
```

#### 16. Create brighter and darker images.
```python

img3_brighter = cv2.add(img3_rgb, m)
img3_darker = cv2.subtract(img3_rgb, m)

```

#### 17. Display the images (Original Image, Darker Image, Brighter Image).
```python
plt.figure(figsize=(10,5))
plt.subplot(1,3,1), plt.imshow(img3_rgb), plt.title("Original Image"), plt.axis("off")
plt.subplot(1,3,2), plt.imshow(img3_brighter), plt.title("Brighter Image"), plt.axis("off")
plt.subplot(1,3,3), plt.imshow(img3_darker), plt.title("Darker Image"), plt.axis("off")
plt.show()
```

#### 18. Modify the image contrast.
```python
# Create two higher contrast images using the 'scale' option with factors of 1.1 and 1.2 (without overflow fix)
# matrix1 = 
# matrix2 = 
# img_higher1 = 
# img_higher2 = 
matrix1 = np.ones(img3_rgb.shape, dtype="float32") * 1.1
matrix2 = np.ones(img3_rgb.shape, dtype="float32") * 1.2
img_higher1 = cv2.multiply(img3_rgb.astype("float32"), matrix1).clip(0,255).astype("uint8")
img_higher2 = cv2.multiply(img3_rgb.astype("float32"), matrix2).clip(0,255).astype("uint8")
```

#### 19. Display the images (Original, Lower Contrast, Higher Contrast).
```python
plt.figure(figsize=(10,5))
plt.subplot(1,3,1), plt.imshow(img3_rgb), plt.title("Original Image"), plt.axis("off")
plt.subplot(1,3,2), plt.imshow(img_higher1), plt.title("Higher Contrast (1.1x)"), plt.axis("off")
plt.subplot(1,3,3), plt.imshow(img_higher2), plt.title("Higher Contrast (1.2x)"), plt.axis("off")
plt.show()
```

#### 20. Split the image (boy.jpg) into the B,G,R components & Display the channels.
```python
b, g, r = cv2.split(img3)
plt.figure(figsize=(10,5))
plt.subplot(1,3,1), plt.imshow(b, cmap='gray'), plt.title("Blue Channel"), plt.axis("off")
plt.subplot(1,3,2), plt.imshow(g, cmap='gray'), plt.title("Green Channel"), plt.axis("off")
plt.subplot(1,3,3), plt.imshow(r, cmap='gray'), plt.title("Red Channel"), plt.axis("off")
plt.show()
```

#### 21. Merged the R, G, B , displays along with the original image
```python
merged_rgb = cv2.merge([r, g, b])
plt.figure(figsize=(5,5))
plt.imshow(merged_rgb)
plt.title("Merged RGB Image")
plt.axis("off")
plt.show()
```

#### 22. Split the image into the H, S, V components & Display the channels.
```python
hsv_img = cv2.cvtColor(img3_rgb, cv2.COLOR_RGB2HSV)
h, s, v = cv2.split(hsv_img)
plt.figure(figsize=(10,5))
plt.subplot(1,3,1), plt.imshow(h, cmap='gray'), plt.title("Hue Channel"), plt.axis("off")
plt.subplot(1,3,2), plt.imshow(s, cmap='gray'), plt.title("Saturation Channel"), plt.axis("off")
plt.subplot(1,3,3), plt.imshow(v, cmap='gray'), plt.title("Value Channel"), plt.axis("off")
plt.show()
```
#### 23. Merged the H, S, V, displays along with original image.
```python
merged_hsv = cv2.cvtColor(cv2.merge([h, s, v]), cv2.COLOR_HSV2RGB)
combined = np.concatenate((img3_rgb, merged_hsv), axis=1)
plt.figure(figsize=(10, 5))
plt.imshow(combined)
plt.title("Original Image  &  Merged HSV Image")
plt.axis("off")
plt.show()
```

## Output:
- **i)** Read and Display an Image.
- <img width="704" height="537" alt="image" src="https://github.com/user-attachments/assets/749cb13d-8e64-401a-8bfc-d914b1130ddc" />
- <img width="780" height="555" alt="image" src="https://github.com/user-attachments/assets/89191ab3-64df-46ed-a082-328eeff815da" />
<img width="552" height="535" alt="image" src="https://github.com/user-attachments/assets/b4e2063a-1e82-4522-8920-f9fa565af807" />
<img width="538" height="538" alt="image" src="https://github.com/user-attachments/assets/8da364cb-4f20-4765-87aa-05d57f07702c" />
<img width="765" height="465" alt="image" src="https://github.com/user-attachments/assets/210fff0e-7ea8-46f3-88aa-65eb04fa1eb8" />
<img width="779" height="442" alt="image" src="https://github.com/user-attachments/assets/17b43eeb-7168-4bc6-97a6-849147f63598" />


- **ii)** Adjust Image Brightness.

- <img width="1096" height="309" alt="image" src="https://github.com/user-attachments/assets/221f2924-d152-446c-a282-7b376daa2663" />

- **iii)** Modify Image Contrast.
- <img width="1062" height="312" alt="image" src="https://github.com/user-attachments/assets/37fb9ef1-42a4-497b-83cc-0d6f9371b4d0" />

- **iv)** Generate Third Image Using Bitwise Operations.

- <img width="1035" height="283" alt="image" src="https://github.com/user-attachments/assets/646a32dd-121d-4b37-8356-331cea5c405c" />
<img width="604" height="443" alt="image" src="https://github.com/user-attachments/assets/9c279aa9-1336-4e26-8137-1ca6e51f4cfa" />
<img width="1085" height="302" alt="image" src="https://github.com/user-attachments/assets/de336a77-0609-420b-a781-8effa3bdcdab" />
<img width="1099" height="447" alt="image" src="https://github.com/user-attachments/assets/71751dc1-b30c-4e91-a6f2-f2cf7365358f" />


## Result:
Thus, the images were read, displayed, brightness and contrast adjustments were made, and bitwise operations were performed successfully using the Python program.

