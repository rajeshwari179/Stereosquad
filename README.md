# Video

We curated our own dataset for our project, focusing on the Coda building. To maintain clarity and sharpness across the frames of the video, we used a gimbal during recording. This ensured minimal blurring and stable footage throughout, enhancing the quality of the video dataset. For accurate camera calibration, we used various checkerboard patterns. These patterns serve as a calibration tool due to their well-defined geometry and known dimensions. The known properties of the checkerboard patterns provide a ground truth reference, helping in the precise estimation of camera parameters. To diversify our calibration dataset and avoid symmetrical patterns that could potentially skew the calibration results, we designed custom 3x3 grids.

## FAST SIFT (implemented)

### Feature Mapping

We worked on KD-tree algorithm for feature mapping. KD-trees are designed for efficient nearest neighbor searches. KD-trees are efficient in handling high-dimensional data, making them suitable for feature mapping where the dimensionality of the data is a concern.

- **Feature mapping across different frames of the video**

### Fundamental Matrix

Using the matched key points, compute the Fundamental Matrix (F) that encapsulates the epipolar geometry between the two images. Use RANSAC algorithm to obtain the fundamental matrix. The computed Fundamental Matrix should satisfy the epipolar constraint for all matched points.

- The epipolar constraint states that a point `(x, y)` in the first image and its corresponding point `(x', y')` in the second image, along with the Fundamental Matrix F, should satisfy the equation: `x'TFx = 0`

### From Epipolar Lines to 3D Coordinates

After obtaining the epipolar lines from the Fundamental Matrix, the next step is to triangulate the corresponding 3D coordinates of the matched keypoints. This is done by finding the intersection point of the epipolar lines from the two images.

### Compute 3D Coordinates

For a matched pair of keypoints `(point1, point2)`, the 3D coordinates `(X, Y, Z)` can be computed using triangulation. This involves finding the intersection point of the epipolar lines corresponding to `point1` and `point2`.

### Compute Angle in Real Coordinate Axes

Once you have the 3D coordinates `(X, Y, Z)` of a point captured by different shots in a video, its angle with respect to the real coordinate axes (X-axis, Y-axis, Z-axis) can be computed.

### Goldberg Polygon Binning

To categorize the points based on their angles, you can use the Goldberg Polygon technique. This method divides the 3D space around the point into a set of polygons or bins based on the angles. Each bin represents a range of angles, and the points falling within that range are assigned to that bin.

### Store RGB Value in Bins

For each bin created by the Goldberg Polygon, store the RGB (Red, Green, Blue) color value of the point captured from different shots in the video. This creates a color histogram or color map for each angle range, capturing the color variations of the point from different viewpoints.

### Use Color Data for Stereo Images

By storing the RGB values in different angle bins using the Goldberg Polygon, you have a comprehensive color dataset for the point from various perspectives. This color information can be utilized to generate stereo images or 3D reconstructions, providing a rich and detailed visualization of the scene or object.
