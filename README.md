# DocDetector

## Script Functions

### `preProcessing(img)`

This function takes an image as input and returns the preprocessed image. The image is first converted to grayscale, then Gaussian blur is applied, followed by edge detection using the Canny algorithm. Next, morphological operations such as dilation and erosion are performed to remove noise and fill gaps in the edges. Finally, the resulting binary image is returned.

### `getContours(img)`

This function takes an image as input and returns the largest contour found in the image that is a square object. The function first finds all contours in the binary image using `cv2.findContours()`. If the area of the contour is greater than 5000 pixels, it calculates the perimeter using `cv2.arcLength()`. It then approximates the contour to a polygon using the `cv2.approxPolyDP()` function. If the area of the contour is the largest found so far and the polygon has four sides, it is considered the largest square contour found, and its coordinates are returned.

### `reorder(points)`

This function takes an array of four points as input and rearranges them in a specific order. The four points are reshaped into a 4x2 matrix, and the sum and difference of the x and y coordinates of the points are calculated. The point with the smallest sum is assigned to the top-left corner, while the point with the largest sum is assigned to the bottom-right corner. The point with the smallest difference is assigned to the top-right corner, while the point with the largest difference is assigned to the bottom-left corner. The reordered points are returned.

### `getWarp(img, points)`

This function takes an image and the coordinates of the square object as input and returns the warped image. The coordinates of the square object are first rearranged using the `reorder()` function. The function then calculates the perspective transformation matrix using `cv2.getPerspectiveTransform()` and applies the transformation to the image using `cv2.warpPerspective()`. The resulting warped image is cropped to remove the margins and resized to the dimensions of the input image. The cropped and resized image is returned.

### `stackImages(scale, imgList)`

This function takes a scale factor and a list of images as input and returns a vertically stacked image of the input images. The function first checks if the input images are in a nested list format and resizes each image to the same dimensions if necessary. It then horizontally stacks the images in each row and vertically stacks the rows to create a single image.
