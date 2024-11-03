---
title: Mathmatics in GIS
feed: show
date: 03-11-2024
---
## Distance Calculation

### 1. Euclidean Distance

- **Formula**:
  $$
  d = \sqrt{(x_2 - x_1)^2 + (y_2 - y_1)^2}
  $$

- **Description**: The Euclidean distance calculates the straight-line distance between two points \((x_1, y_1)\) and \((x_2, y_2)\) in a two-dimensional plane, based on the Pythagorean theorem. It determines the length of the hypotenuse of the right triangle formed by the two points.

- **Example**: To calculate the Euclidean distance between Seoul (Latitude 37.5665° N, Longitude 126.978° E) and Busan (Latitude 35.1796° N, Longitude 129.0756° E), we need to project the two points onto a flat coordinate system. For simplicity, we can use the following coordinates:
  - Seoul: \((0, 0)\)
  - Busan: \((2, 2)\) (simple hypothetical coordinates)
  $$
  d = \sqrt{(2 - 0)^2 + (2 - 0)^2} = \sqrt{2^2 + 2^2} = \sqrt{4 + 4} = \sqrt{8} \approx 2.83.
  $$

### 2. Manhattan Distance

- **Formula**:
  $$
  d = |x_2 - x_1| + |y_2 - y_1|
  $$

- **Description**: The Manhattan distance is suitable for calculating distances in a city grid layout, where movement can only occur in horizontal and vertical directions. This distance can be equal to or greater than the actual distance.

- **Example**: To calculate the Manhattan distance between Seoul and Busan using the same hypothetical coordinates:
  $$
  d = |2 - 0| + |2 - 0| = 2 + 2 = 4.
  $$

### 3. Haversine Distance

- **Formula**:
  $$
  d = 2r \cdot \arcsin\left(\sqrt{\sin^2\left(\frac{\Delta \phi}{2}\right) + \cos(\phi_1) \cos(\phi_2) \sin^2\left(\frac{\Delta \lambda}{2}\right)}\right)
  $$

- **Description**: The Haversine distance calculates the distance between two points on the surface of a sphere, such as the Earth. This formula is based on the differences in latitude \(\Delta \phi\) and longitude \(\Delta \lambda\), where \(r\) represents the radius of the Earth.

- **Example**: To calculate the Haversine distance between Seoul and Busan, we use their latitude and longitude. The latitude of Seoul is $$\phi_1 = 37.5665° N$$ and the longitude is $$\lambda_1 = 126.978° E$$, while Busan's latitude is $$\phi_2 = 35.1796° N$$ and longitude is $$\lambda_2 = 129.0756° E$$. We can define the differences in latitude and longitude as follows:
  - Latitude difference:
  $$
  \Delta \phi = \phi_2 - \phi_1 = 35.1796 - 37.5665 = -2.3869 \text{°}
  $$
  - Longitude difference:
  $$
  \Delta \lambda = \lambda_2 - \lambda_1 = 129.0756 - 126.978 = 2.0976 \text{°}
  $$
  Assuming the Earth's radius \(r\) is approximately 6371 km, we can convert the latitude and longitude to radians and apply the Haversine formula to calculate the distance.

### 4. Great-circle Distance

- **Formula**:
  $$
  d = r \cdot \Delta \sigma
  $$

- **Description**: The great-circle distance is defined as the shortest distance between two points on a sphere. Here, $$\Delta \sigma$$ represents the central angle between the two points, typically measured in radians. This method is useful for long-distance travel, such as flight paths.

- **Example**: To calculate the great-circle distance between Seoul and Busan, we need to know the central angle $$\Delta \sigma$$ between the two points. In this case, we can assume that \(\Delta \sigma\) is approximately 0.58 radians. Assuming the Earth's radius \(r\) is 6371 km,
  $$
  d = 6371 \cdot 0.58 \approx 3692.18 \text{ km}.
  $$

These distance calculation methods are utilized in various fields, and understanding the characteristics of each method allows for the selection of the appropriate distance calculation method for specific situations.

## 2. Area Calculation

### 2.1 Polygon Area
- **Formula**:
  $$
  A = \frac{1}{2} \left| \sum_{i=1}^{n} (x_i y_{i+1} - x_{i+1} y_i) \right|
  $$
  
- **Description**: To calculate the area of a polygon, the coordinates of each vertex \((x_i, y_i)\) are used. This formula connects the given vertices in order and sums the areas of the triangles formed to find the total area. Here, \((x_{n+1}, y_{n+1})\) returns to \((x_1, y_1)\).

- **Example**: 
  - Vertex coordinates: \(A(1, 1), B(4, 1), C(4, 3), D(1, 3)\)
  
  Calculation:
  $$
  A = \frac{1}{2} \left| (1 \cdot 1 + 4 \cdot 3 + 4 \cdot 3 + 1 \cdot 1) - (1 \cdot 4 + 1 \cdot 4 + 3 \cdot 1 + 3 \cdot 1) \right|
  $$
  $$
  = \frac{1}{2} \left| (1 + 12 + 12 + 1) - (4 + 4 + 3 + 3) \right|
  $$
  $$
  = \frac{1}{2} \left| 26 - 14 \right| = \frac{1}{2} \cdot 12 = 6
  $$
  Thus, the area \(A = 6\).

### 2.2 Circle Area
- **Formula**:
  $$
  A = \pi r^2
  $$
  
- **Description**: This formula calculates the area of a circle by multiplying the square of the radius \(r\) by the constant \(\pi\).

- **Example**: 
  - Area calculation for a circle with radius \(r = 3\):
  
  $$
  A = \pi (3)^2 = 9\pi \approx 28.27
  $$
  Thus, the area of the circle is approximately \(28.27\).

### 2.3 Ellipse Area
- **Formula**:
  $$
  A = \pi a b
  $$
  
- **Description**: The area of an ellipse is calculated by multiplying the lengths of the major axis \(a\) and the minor axis \(b\) and then multiplying by \(\pi\).

- **Example**: 
  - Area of an ellipse with major axis \(a = 5\) and minor axis \(b = 3\):
  
  $$
  A = \pi (5)(3) = 15\pi \approx 47.12
  $$
  Thus, the area of the ellipse is approximately \(47.12\).

### 2.4 Triangle Area
- **Formula**:
  $$
  A = \frac{1}{2} b h
  $$
  
- **Description**: The area of a triangle is calculated by multiplying the base \(b\) by the height \(h\) and then dividing by 2.

- **Example**: 
  - Area of a triangle with base \(b = 6\) and height \(h = 4\):
  
  $$
  A = \frac{1}{2} (6)(4) = 12
  $$
  Thus, the area of the triangle is \(12\).

### 2.5 Perimeter Length
- **Formula**:
  $$
  L = \sum_{i=1}^{n} d_{i,i+1}
  $$
  
- **Description**: The perimeter length of a polygon is defined as the sum of the distances \(d_{i,i+1}\) between each vertex. This distance can be calculated using the Euclidean distance between two points.

- **Example**: 
  - Vertex coordinates: \(A(1, 1), B(4, 1), C(4, 3), D(1, 3)\)
  
  Distance calculations:
  $$
  d_{AB} = \sqrt{(4 - 1)^2 + (1 - 1)^2} = \sqrt{3^2} = 3
  $$
  $$
  d_{BC} = \sqrt{(4 - 4)^2 + (3 - 1)^2} = \sqrt{2^2} = 2
  $$
  $$
  d_{CD} = \sqrt{(1 - 4)^2 + (3 - 3)^2} = \sqrt{3^2} = 3
  $$
  $$
  d_{DA} = \sqrt{(1 - 1)^2 + (1 - 3)^2} = \sqrt{2^2} = 2
  $$
  Therefore, the perimeter length \(L\) is:
  $$
  L = d_{AB} + d_{BC} + d_{CD} + d_{DA} = 3 + 2 + 3 + 2 = 10
  $$

Through these various area calculation methods and examples, the formulas can be better understood.


## 3. Boundary and Adjacency Analysis

### 3.1 Buffering
- **Formula**: The process of creating a new area within a specified distance around a certain point.

- **Description**: Buffering is a method that generates a circular or rectangular area around a specific point, defined by a certain radius. This area is useful for analyzing the adjacency of other objects within a specified distance. For instance, it is used to establish safety zones around roads or protected environmental areas.

- **Example**: 
  - When creating a circular buffer with a radius \(r = 2\) at point \(A(3, 4)\), the boundary of the buffer is defined as:
  
  $$
  (x - 3)^2 + (y - 4)^2 \leq 2^2
  $$
  
  This buffer generates a circle of radius \(2\) centered at point \(A\), which can be used to find other points contained within it.

### 3.2 Adjacency Analysis
- **Description**: Adjacency analysis is a method of filtering data based on distance to evaluate the proximity to specific objects. This process identifies objects that are adjacent to one another based on distance or connectivity, helping to understand the relationships within the data.

- **Example**: 
  - For example, if there are several stores, one can filter nearby stores based on distance. Assuming the coordinates of stores \(S_1\) and \(S_2\) are \((1, 2)\) and \((3, 4)\), respectively, the Euclidean distance between the two points is:
  
  $$
  d(S_1, S_2) = \sqrt{(3 - 1)^2 + (4 - 2)^2} = \sqrt{4 + 4} = \sqrt{8} \approx 2.83
  $$
  
  If this distance is less than \(3\), it can be concluded that the two stores are adjacent.

### 3.3 Point Set Distance-Based Analysis
- **Formula**:
  $$
  D = \min_{p \in P} d(p, x)
  $$

- **Description**: This method calculates the shortest distance between point \(x\) and points in the set \(P\). The formula computes the distance between point \(x\) and all points \(p\) in the set \(P\), then selects the minimum distance.

- **Example**: 
  - Given point \(x(2, 3)\) and the point set \(P = \{(1, 1), (4, 5), (3, 2)\}\), the distances to each point are calculated as follows:
  
  $$
  d((2, 3), (1, 1)) = \sqrt{(1 - 2)^2 + (1 - 3)^2} = \sqrt{1 + 4} = \sqrt{5} \approx 2.24
  $$
  
  $$
  d((2, 3), (4, 5)) = \sqrt{(4 - 2)^2 + (5 - 3)^2} = \sqrt{4 + 4} = \sqrt{8} \approx 2.83
  $$
  
  $$
  d((2, 3), (3, 2)) = \sqrt{(3 - 2)^2 + (2 - 3)^2} = \sqrt{1 + 1} = \sqrt{2} \approx 1.41
  $$

  In this case, the shortest distance is $$D = \min(\sqrt{5}, \sqrt{8}, \sqrt{2}) \approx 1.41$$, which represents the minimum distance between point \(x\) and the points in set \(P\).


## 4. Spatial Statistics

### 4.1 Kriging
- **Formula**:
  $$
  Z^*(x_0) = \sum_{i=1}^{n} \lambda_i Z(x_i)
  $$
  
- **Description**: Kriging is a method that utilizes the spatial correlation of geographical data to predict the value at a specific point. Here, \(Z(x_i)\) represents the observed values, while \(\lambda_i\) are the weights assigned to each observation. These weights are determined based on spatial distance or correlation.

- **Example**: 
  - Suppose we want to predict air pollution levels in a specific city. Let’s say the observed pollution levels at several monitoring stations in Seoul are \(Z(x_1) = 40\), \(Z(x_2) = 50\), and \(Z(x_3) = 30\). If the weights for these points are \(\lambda_1 = 0.3\), \(\lambda_2 = 0.5\), and \(\lambda_3 = 0.2\), then:
  
  $$
  Z^*(x_0) = 0.3 \cdot 40 + 0.5 \cdot 50 + 0.2 \cdot 30 = 12 + 25 + 6 = 43
  $$
  
  Therefore, the predicted air pollution level at the specific area \(x_0\) is \(43\).

### 4.2 Kernel Density Estimation
- **Formula**:
  $$
  K(x) = \frac{1}{n h^2} \sum_{i=1}^{n} K\left(\frac{x - x_i}{h}\right)
  $$
  
- **Description**: Kernel density estimation is a method for estimating the density of given data points to visualize the distribution of a specific area. \(K\) is the kernel function, and \(h\) represents the bandwidth, which affects the smoothness of the density estimation.

- **Example**: 
  - Assume we are analyzing population flow data in Seoul. The data points represent the number of people in a specific area, for example, near Gangnam Station, with values \(x_1 = 1000\), \(x_2 = 1500\), and \(x_3 = 800\). Setting the bandwidth \(h = 200\) and using a Gaussian kernel, we can calculate:
  
  $$
  K(1200) = \frac{1}{3 \cdot 200^2} \left( K\left(\frac{1200 - 1000}{200}\right) + K\left(\frac{1200 - 1500}{200}\right) + K\left(\frac{1200 - 800}{200}\right) \right)
  $$
  
  We calculate the kernel function values to estimate the density and visualize the population density near Gangnam Station.

### 4.3 Mean Center
- **Formula**:
  $$
  C_x = \frac{1}{n} \sum_{i=1}^{n} x_i, \quad C_y = \frac{1}{n} \sum_{i=1}^{n} y_i
  $$
  
- **Description**: This formula calculates the average position of data points to find the center point. \(C_x\) is the average of the \(x\) coordinates, and \(C_y\) is the average of the \(y\) coordinates.

- **Example**: 
  - Suppose the coordinates of cafes and restaurants located in Songdo, Incheon, are as follows: 
    - Cafe A: \((1, 3)\)
    - Cafe B: \((2, 5)\)
    - Restaurant C: \((4, 1)\)
  
  Calculating the mean center gives:
  
  $$
  C_x = \frac{1 + 2 + 4}{3} = \frac{7}{3} \approx 2.33, \quad C_y = \frac{3 + 5 + 1}{3} = \frac{9}{3} = 3
  $$
  
  Thus, the mean center is approximately \((2.33, 3)\), located near the center of Songdo.

### 4.4 Standard Deviation
- **Formula**:
  $$
  \sigma = \sqrt{\frac{1}{N} \sum_{i=1}^{N} (x_i - \bar{x})^2}
  $$
  
- **Description**: Standard deviation is a measure of the dispersion of data, indicating how much the data spreads from the mean. Here, \(\bar{x}\) is the mean of the data.

- **Example**: 
  - Let’s examine temperature data in Seoul. If the data points are \(20^\circ\), \(22^\circ\), \(24^\circ\), and \(26^\circ\), then the average \(\bar{x}\) is:
  
  $$
  \bar{x} = \frac{20 + 22 + 24 + 26}{4} = 23
  $$
  
  The standard deviation is calculated as follows:
  
  $$
  \sigma = \sqrt{\frac{1}{4} \left((20 - 23)^2 + (22 - 23)^2 + (24 - 23)^2 + (26 - 23)^2\right)}
  $$
  $$
  = \sqrt{\frac{1}{4} (9 + 1 + 1 + 9)} = \sqrt{\frac{20}{4}} = \sqrt{5} \approx 2.24
  $$
  
  Therefore, the standard deviation of Seoul's temperature data is approximately \(2.24^\circ\).

### 4.5 Variance
- **Formula**:
  $$
  D = \frac{1}{N-1} \sum_{i=1}^{N} (x_i - \bar{x})^2
  $$
  
- **Description**: Variance is a formula used to measure the variability of data, calculated as the average squared distance from the mean.

- **Example**: 
  - Suppose the sea surface temperature data in Busan is \(18^\circ\), \(19^\circ\), \(20^\circ\), and \(22^\circ\). The average \(\bar{x}\) is:
  
  $$
  \bar{x} = \frac{18 + 19 + 20 + 22}{4} = 19.75
  $$
  Then the variance is calculated as:
  $$
  D = \frac{1}{4 - 1} \left((18 - 19.75)^2 + (19 - 19.75)^2 + (20 - 19.75)^2 + (22 - 19.75)^2\right)
  $$
  $$
  = \frac{1}{3} \left(3.0625 + 0.5625 + 0.0625 + 5.0625\right) = \frac{8.75}{3} \approx 2.92
  $$
  
  Therefore, the variance of the sea surface temperature in Busan is approximately \(2.92\).


# 5. Geographic Data Modeling

## 5.1 Coordinate Transformation
- **Formula**:
  $$ 
  \begin{bmatrix}
  x' \\
  y'
  \end{bmatrix} =
  \begin{bmatrix}
  a & b \\
  c & d
  \end{bmatrix}
  \begin{bmatrix}
  x \\
  y
  \end{bmatrix} + 
  \begin{bmatrix}
  e \\
  f
  \end{bmatrix}
  $$
  
- **Description**: This represents the process of transforming a given coordinate \((x, y)\) into a new coordinate system. The transformation matrix \(\begin{bmatrix} a & b \\ c & d \end{bmatrix}\) includes rotation, scaling, etc., and \(\begin{bmatrix} e \\ f \end{bmatrix}\) represents translation.

- **Example**: 
  - For instance, let's transform a specific point in Seoul \((x, y) = (2, 3)\). If the transformation matrix is 
  $$
  \begin{bmatrix}
  1 & 0 \\
  0 & 1
  \end{bmatrix}
  $$ 
  (meaning no transformation) and the translation vector is 
  $$
  \begin{bmatrix}
  5 \\
  -2
  \end{bmatrix}
  $$, then,
  
  $$
  \begin{bmatrix}
  x' \\
  y'
  \end{bmatrix} =
  \begin{bmatrix}
  1 & 0 \\
  0 & 1
  \end{bmatrix}
  \begin{bmatrix}
  2 \\
  3
  \end{bmatrix} + 
  \begin{bmatrix}
  5 \\
  -2
  \end{bmatrix}
  =
  \begin{bmatrix}
  7 \\
  1
  \end{bmatrix}
  $$
  
  Therefore, the transformed coordinates are \((7, 1)\).

## 5.2 Transformation Matrix
- **Formula**:
  $$ 
  T = 
  \begin{bmatrix}
  s_x & 0 & t_x \\
  0 & s_y & t_y \\
  0 & 0 & 1
  \end{bmatrix}
  $$
  
- **Description**: This matrix represents transformations in 2D space, where \(s_x\) and \(s_y\) are the scaling factors for the \(x\) and \(y\) axes, and \(t_x\) and \(t_y\) represent the position after transformation.

- **Example**: 
  - If we want to scale an object on a city map by a factor of 2 and move it by \((3, 4)\), the scaling factors would be \(s_x = 2\) and \(s_y = 2\), and the translation values would be \(t_x = 3\) and \(t_y = 4\). The transformation matrix would be:
  
  $$
  T = 
  \begin{bmatrix}
  2 & 0 & 3 \\
  0 & 2 & 4 \\
  0 & 0 & 1
  \end{bmatrix}
  $$
  
  Using this matrix to transform the point \((1, 1)\) yields:
  
  $$
  \begin{bmatrix}
  x' \\
  y' \\
  1
  \end{bmatrix} =
  \begin{bmatrix}
  2 & 0 & 3 \\
  0 & 2 & 4 \\
  0 & 0 & 1
  \end{bmatrix}
  \begin{bmatrix}
  1 \\
  1 \\
  1
  \end{bmatrix} =
  \begin{bmatrix}
  5 \\
  6 \\
  1
  \end{bmatrix}
  $$
  
  Thus, the transformed point is \((5, 6)\).

## 5.3 Ratio Transformation
- **Formula**:
  $$ 
  \text{scaled value} = \frac{\text{original value}}{\text{scale factor}} 
  $$
  
- **Description**: This describes the process of adjusting the ratio of a given value to transform it into a new value. The scale factor determines the ratio of the transformation.

- **Example**: 
  - For instance, to convert a temperature of \(30^\circ C\) measured in a specific area of Seoul to Fahrenheit, we can use the conversion formula:
  
  $$ 
  F = C \times 1.8 + 32
  $$
  
  Thus, converting \(30^\circ C\) gives:
  
  $$
  F = 30 \times 1.8 + 32 = 86^\circ F
  $$ 

  Therefore, \(30^\circ C\) converts to \(86^\circ F\).


# 6. Land Use Change Detection

## 6.1 NDVI (Normalized Difference Vegetation Index)
- **Formula**:
  $$ NDVI = \frac{NIR - RED}{NIR + RED} $$

- **Description**: NDVI is an indicator used to assess the health of vegetation, based on the reflectance of the red (RED) and near-infrared (NIR) wavelengths. The values range from -1 to 1, where values above 0.2 indicate the presence of vegetation.

- **Example**:
  - In a park in Seoul, if the red reflectance is \(RED = 0.2\) and the near-infrared reflectance is \(NIR = 0.5\), then
  
  $$
  NDVI = \frac{0.5 - 0.2}{0.5 + 0.2} = \frac{0.3}{0.7} \approx 0.43
  $$
  
  This value indicates that healthy vegetation exists in that area.

## 6.2 Change Detection
- **Formula**:
  $$ \Delta = V_{t2} - V_{t1} $$

- **Description**: This method calculates the change amount by comparing the values at two time points \(t_1\) and \(t_2\). Generally, values obtained from satellite images or specific indices are used.

- **Example**:
  - If the vegetation index for a specific area changes from \(V_{t1} = 0.6\) (2020) to \(V_{t2} = 0.4\) (2021), then
  
  $$
  \Delta = 0.4 - 0.6 = -0.2
  $$
  
  This indicates that the health of the vegetation in that area has declined.

## 6.3 Land Cover Change Detection
- **Formula**:
  $$ \text{Change} = \frac{(L_{t2} - L_{t1})}{L_{t1}} \times 100\% $$

- **Description**: This process calculates the change rate by comparing land cover at two time points. It is useful for analyzing urban development, agricultural expansion, and deforestation.

- **Example**:
  - If the land cover of a specific area changes from \(L_{t1} = 150\) hectares in 2020 to \(L_{t2} = 120\) hectares in 2021, then
  
  $$
  \text{Change} = \frac{(120 - 150)}{150} \times 100\% = \frac{-30}{150} \times 100\% = -20\%
  $$
  
  This indicates a 20% decrease in land cover in that area.

## 6.4 Patch Variability Index
- **Formula**:
  $$ PVI = \frac{\text{Patch Area}}{\text{Total Area}} $$

- **Description**: This index represents the area of a specific patch as a proportion of the total area, assessing the significance of that patch. A high PVI value indicates that the specific patch occupies a large proportion of the overall area.

- **Example**:
  - In a city, if a specific park has a patch area of \(Patch Area = 20\) hectares and the total area is \(Total Area = 200\) hectares, then
  
  $$
  PVI = \frac{20}{200} = 0.1
  $$
  
  This indicates that the park occupies 10% of the total area. Such ratios help evaluate the importance of green spaces in the city.


# 7. Clustering

## 7.1 K-Means Clustering
- **Formula**:
  $$ J = \sum_{j=1}^{K} \sum_{x_i \in C_j} \| x_i - \mu_j \|^2 $$

- **Description**: K-means clustering is an algorithm that divides data points into K clusters, minimizing the sum of the squared distances between the data points and the cluster centers (means) within each cluster. The center of each cluster is updated to the average of the points belonging to that cluster.

- **Example**:
  - For instance, let’s assume \(K = 3\) and the data points are as follows:
    
    \{(1, 2), (1, 4), (1, 0), (10, 2), (10, 4), (10, 0)\}
    
  - Suppose the initial cluster centers are \((1, 2)\), \((10, 2)\), and \((5, 5)\). The algorithm calculates the distance from each point to the corresponding cluster centers, assigns each point to the nearest cluster, and then iteratively updates the centers to find the optimal clustering.

## 7.2 DBSCAN (Density-Based Spatial Clustering of Applications with Noise)
- **Formula**: Clusters are defined as areas of high density, where points within an epsilon distance are connected to form a cluster.

- **Description**: DBSCAN is a density-based clustering algorithm that groups points with sufficient density within a specific radius (epsilon). Noise points are not included in clusters. The two main parameters are \(\epsilon\) (radius) and \(minPts\) (minimum number of points required to form a cluster).

- **Example**:
  - For example, with \( \epsilon = 0.5\) and \(minPts = 3\), if the specific data points are \((2, 3)\), \((2, 2)\), and \((3, 2)\), they are closely located and form a cluster. However, points like \((10, 10)\) are considered noise if they are not sufficiently close to any other cluster.

## 7.3 Silhouette Score
- **Formula**:
  $$ S = \frac{b - a}{\max(a, b)} $$

- **Description**: The silhouette score measures the cohesion and separation of clusters. Here, \(a\) is the average distance between a point and other points in the same cluster (intra-cluster distance), and \(b\) is the average distance between the point and the points in the nearest different cluster (inter-cluster distance). The silhouette score can range from -1 to 1, with values closer to 1 indicating better clustering.

- **Example**:
  - For instance, if a specific point has \(a = 1.0\) (average distance within the same cluster) and \(b = 2.0\) (average distance to the nearest cluster), then
  
  $$
  S = \frac{2.0 - 1.0}{\max(1.0, 2.0)} = \frac{1.0}{2.0} = 0.5
  $$
  
  This indicates that the point is well-clustered but is also close to another cluster.


# 8. Regression Analysis

## 8.1 Linear Regression
- **Formula**:
  $$ Y = a + bX + \epsilon $$

- **Description**: Linear regression is a model that analyzes the effect of an independent variable \(X\) on a dependent variable \(Y\). Here, \(a\) represents the y-intercept (the point where the regression line intersects the y-axis), \(b\) is the slope (the change in \(Y\) for each unit change in \(X\)), and \(\epsilon\) is the error term (the difference between actual data and predicted values).

- **Example**:
  - Suppose we analyze the relationship between population density \(Y\) and traffic volume \(X\) using GIS data. The data is as follows:
    - Traffic volume (number of vehicles): \([200, 400, 600, 800]\)
    - Population density: \([1500, 2000, 2500, 3000]\)

  - By estimating the slope and intercept using a linear regression model, we can derive the following regression equation:
  
  $$
  Y = 1000 + 2.5X
  $$

  - This indicates that for each additional vehicle, the population density increases by 2.5 people.

## 8.2 Polynomial Regression
- **Formula**:
  $$ Y = a + b_1X + b_2X^2 + ... + b_nX^n + \epsilon $$

- **Description**: Polynomial regression is a technique that models non-linear relationships by including multiple degrees of the independent variable. While linear regression assumes a linear relationship, polynomial regression allows for a curved relationship.

- **Example**:
  - Assume we analyze the relationship between altitude \(X\) and vegetation index \(Y\) in GIS. The data is as follows:
    - Altitude (m): \([100, 200, 300, 400, 500]\)
    - Vegetation index: \([0.5, 0.7, 0.9, 0.6, 0.3]\)

  - Through polynomial regression analysis, we can obtain the following regression equation:
  
  $$
  Y = 0.8 - 0.002X^2
  $$

  - This model indicates that the vegetation index increases with altitude until a certain point, after which it decreases.

## 8.3 Logistic Regression
- **Formula**:
  $$ P(Y=1|X) = \frac{1}{1 + e^{-(a + bX)}} $$

- **Description**: Logistic regression is used to predict a binary dependent variable and models the log odds ratio. \(P(Y=1|X)\) represents the probability that the dependent variable \(Y\) equals 1 given the independent variable \(X\).

- **Example**:
  - Assume we analyze the relationship between land use change \(Y\) and nearby development density \(X\) using GIS data. Here, \(Y\) is 1 if a change occurs and 0 if not. The data is as follows:
    - Development density (number of buildings per unit area): \([1, 2, 3, 4, 5]\)
    - Land use change status: \([0, 0, 1, 1, 1]\)

  - The logistic regression model yields the following regression equation:
  
  $$
  P(Y=1|X) = \frac{1}{1 + e^{-(-2 + 0.8X)}}
  $$

  - This model indicates that as development density increases, the probability of land use change also increases.

# 9. GIS Data Transformation

## 9.1 Raster to Vector Conversion
- **Formula**: The process of generating vector polygons for each raster pixel.

- **Description**: This method converts raster data into vector format, forming areas based on the values of each pixel. The conversion process typically involves the following two steps:
  1. Group pixels with the same value in the raster image to define boundaries.
  2. Convert each group into polygons.

- **Example**:
  - For instance, suppose each pixel in a raster image represents a specific land use type. If a pixel value of 1 indicates forest and 2 indicates agricultural land, we can generate vectors through the following process:
  
  $$ 
  \text{Polygon}_{\text{forest}} = \bigcup_{(i,j) \in R} \{(i,j) | \text{Pixel}_{i,j} = 1\} 
  $$

  Here, \(R\) is the set of all pixel indices in the raster image. This process creates a polygon that defines the boundaries of the forest.

## 9.2 Vector to Raster Conversion
- **Formula**: The process of assigning attribute values of vector objects to raster pixels.

- **Description**: This method converts vector data into raster format for pixel-based representation. The conversion process involves:
  1. Defining the bounding box of each vector object and mapping it to the raster grid.
  2. Assigning the attribute values of vector objects to overlapping raster pixels.

- **Example**:
  - For example, assume we have vector data for rivers in a specific area. Let the width of the river be \(W\). The conversion to raster can be performed as follows:
  
  $$
  \text{Raster}_{(x,y)} = 
  \begin{cases}
  W & \text{if } (x,y) \text{ is within the boundary of the vector object} \\
  0 & \text{otherwise}
  \end{cases}
  $$

  This process is useful for representing the area of the river in raster data.

## 9.3 Reprojection
- **Formula**: The process of converting coordinates from one coordinate system to a new one.

- **Description**: The process of converting between different geographic coordinate systems typically involves:
  1. Transforming coordinates \((x, y)\) in the original coordinate system to coordinates \((x', y')\) in the new coordinate system.
  
  $$ 
  \begin{bmatrix}
  x' \\
  y'
  \end{bmatrix} =
  \begin{bmatrix}
  a & b \\
  c & d
  \end{bmatrix}
  \begin{bmatrix}
  x \\
  y
  \end{bmatrix} + 
  \begin{bmatrix}
  e \\
  f
  \end{bmatrix}
  $$

  Here, $$\begin{bmatrix} a & b \\ c & d \end{bmatrix}$$ is the transformation matrix and $$\begin{bmatrix} e \\ f \end{bmatrix}$$ is the translation vector.

- **Example**:
  - When converting from the WGS 84 coordinate system to the UTM coordinate system, we can use the transformation formula above to reproject the coordinates of each point.

## 9.4 Geographic Data Indexing
- **Formula**: 
  $$ I = \{(x, y) | \text{condition}\} $$

- **Description**: This method indexes geographic data points that satisfy specific conditions for fast access. Indexing is typically implemented using structures like R-Trees or Quad-Trees.

- **Example**:
  - For example, suppose we have data for all parks in a city. To index park data with an area of 1000㎡ or more, we can set the following condition:
  
  $$
  I = \{(x, y) | \text{Area} \geq 1000 \, \text{m}^2\}
  $$

  This indexes the set of park locations \((x,y)\) that meet this condition, allowing for efficient access during search or analysis processes.
