Image Color Detection

A project that detects the dominant colors in an image using pixel-level analysis and K-Means clustering, with visualization of color palettes and distribution.

------------------------------------------------------


Libraries Used:

Image Processing

-   OpenCV
-   Pillow (PIL)

Numerical & Data Handling

-   NumPy
-   Pandas

Visualization

-   Matplotlib
-   Seaborn

------------------------------------------------------------------------

PROJECT OVERVIEW

This project identifies dominant colors in an image by: - Preprocessing the image
- Extracting pixel data
- Applying K-Means clustering
- Visualizing the detected colors

Useful For:

-   Color palette extraction
-   Automated design workflows
-   Simplified image color analysis
-   Creative theme generation
-   UI color suggestions

------------------------------------------------------------------------

PREPROCESSING

1. Image Uploading



```python
from google.colab import files
uploaded = files.upload()
```
```

2. Reading the Image

``` python
img = cv2.imread('image.jpg')
img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
```

3. Reshaping for Pixel Extraction

``` python
pixel_values = img_rgb.reshape((-1, 3))
pixel_values = np.float32(pixel_values)
```

4. Noise Removal 

Slight resizing or blurring may be applied if needed.

------------------------------------------------------------------------

COLOR CLUSTERING

K-Means Clustering

``` python
from sklearn.cluster import KMeans
k = 5
model = KMeans(n_clusters=k)
labels = model.fit_predict(pixel_values)
```

Extracting Dominant Colors

``` python
colors = model.cluster_centers_.astype(int)
```

Calculating Percentages

``` python
unique, counts = np.unique(labels, return_counts=True)
color_percentages = counts / sum(counts)
```

------------------------------------------------------------------------

RESULT VISUALIZATION

1. Displaying Original Image

``` python
plt.imshow(img_rgb)
plt.axis('off')
```
2. Color Bar Palette

``` python
plt.bar(range(k), color_percentages, color=np.array(colors)/255)
```

3. Pie Chart

``` python
plt.pie(color_percentages, labels=[f'Color {i+1}' for i in range(k)],
        colors=np.array(colors)/255)
```

------------------------------------------------------------------------

OUTPUT INCLUDES

-   Extracted dominant RGB colors
-   Percentage of each color
-   Color palette bar
-   Pie chart distribution
-   Display of processed image

Example (K = 5):

-   Color 1: RGB(122, 45, 33) --- 32%
-   Color 2: 25%
-   Color 3: 18%
-   Color 4: 15%
-   Color 5: 10%

------------------------------------------------------------------------

FUTURE IMPROVEMENTS

-   Add Hex code output
-   Dynamic K selection (Elbow Method)
-   Background color detection
-   GUI or Web-app interface
-   Video frame color extraction
-   Mobile camera live color detection


