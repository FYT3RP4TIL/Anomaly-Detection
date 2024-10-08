# Anomaly-Detection 
![](https://github.com/user-attachments/assets/c4e54da3-c232-492a-b9d3-f019703ee6df)

# Isolation Forest (Decision Trees) Anomaly Detection

![](https://github.com/user-attachments/assets/b3e0a873-b7f6-459f-bc17-7fe454792233)

## How It Works

Isolation Forest is an unsupervised learning algorithm used for anomaly detection. The key idea behind the algorithm is to isolate anomalies rather than profiling normal data points. The underlying principle is that anomalies are few and different from the majority of the data, making them easier to isolate.

### Key Concepts

1. **Isolation by Random Partitioning**: 
   - Isolation Forest works by creating a series of random partitions of the data. Each partitioning step involves selecting a random feature and then selecting a random split value between the minimum and maximum values of that feature.
   - Anomalies, which are distinct and few in number, require fewer partitions to be isolated because they are different from the rest of the data. That means they are found quickly. 

2. **Tree Structure**:
   - The algorithm builds a collection of isolation trees (iTrees). Each iTree is a binary tree that recursively divides the data points. The depth of the tree required to isolate a point is the number of partitions needed to isolate the point.
   - Points that are isolated quickly (with fewer splits) are likely to be anomalies, while normal points require more splits.

3. **Anomaly Score**:
   - The anomaly score for each point is based on the depth of the tree where the point was isolated. The score is normalized such that the lower the score, the more anomalous the point is considered.
   - The anomaly score is calculated for each data point across all trees, and the average score is used to determine if a point is an anomaly.

     ![](https://github.com/user-attachments/assets/73fdd90e-9ca4-4246-b148-8bb8b8dcba18)

5. **Threshold**:
   - By setting a threshold on the anomaly score, data points can be classified as normal or anomalous. Points with scores above the threshold are labeled as anomalies.

     ![Screenshot 2024-08-28 152501](https://github.com/user-attachments/assets/c7b2a548-29bc-4bf8-9005-86b146d549ed)

### Advantages

- **Efficiency**: Isolation Forest is highly efficient and scales well with large datasets since it works by isolating points rather than modeling the distribution of data.
- **No Assumptions**: Unlike many other anomaly detection methods, Isolation Forest does not make any assumptions about the distribution of data, making it versatile for different types of datasets.
- **Works Well with High Dimensional Data**: The random partitioning process does not suffer from the curse of dimensionality, making Isolation Forest effective even in high-dimensional spaces.

# DBSCAN Anomaly Detection

<div align="center">
    <img src="https://github.com/user-attachments/assets/92024f19-42ae-4c4b-8af3-bb0a7e68092a" alt="Centered Image">
</div

## How It Works

DBSCAN (Density-Based Spatial Clustering of Applications with Noise) is an unsupervised learning algorithm primarily used for clustering, but it also excels at detecting anomalies. The key idea behind DBSCAN is to group together points that are closely packed (dense regions) and mark points that lie alone in low-density regions as anomalies.

### Key Concepts

![](https://github.com/user-attachments/assets/a9043861-fbc1-4c70-bf08-a8b8b8faae7c)

1. **Core Points, Border Points, and Noise**:
   - **Core Points**: Points that have at least a minimum number of neighboring points (MinPts) within a given radius (ε). These points form the dense regions of the data.
   - **Border Points**: Points that have fewer than MinPts within ε but are still within the neighborhood of a core point. They belong to the edge of a cluster.
   - **Noise**: Points that are neither core points nor border points and are considered outliers or anomalies. These points do not belong to any cluster.

     <p align="left">
    <img src="https://github.com/user-attachments/assets/1f39f50e-8eb3-4074-a523-041293099deb" alt="Image 1" width="550">
    <br>
    <img src="https://github.com/user-attachments/assets/60884540-cba8-4275-a918-b002a3025f77" alt="Image 2" width="550">
    <br>
    <img src="https://github.com/user-attachments/assets/0300982e-f448-48e2-b383-ecd27d0ddb26" alt="Image 3" width="550">
   </p>

2. **Density-Based Clustering**:
   - DBSCAN starts with an arbitrary point and retrieves its ε-neighborhood. If this neighborhood contains at least MinPts, the process continues by expanding the cluster. Otherwise, the point is labeled as noise (an anomaly). However, if this point later falls within the ε-neighborhood of a core point, it may be reassigned to a cluster.
   - The algorithm iteratively clusters points, with points that do not belong to any cluster remaining labeled as anomalies.

3. **Anomaly Detection**:
   - Anomalies are identified as the points that are labeled as noise by DBSCAN. These are points that do not have enough neighbors within the specified ε distance to be included in any cluster.

4. **Parameters**:
   - **ε (Epsilon)**: The maximum distance between two points for one to be considered as in the neighborhood of the other.
   - **MinPts**: The minimum number of points required to form a dense region (cluster).

<p align="center">
    <img src="https://github.com/user-attachments/assets/ffb68d91-4942-411e-a268-2cef7dae6c30" alt="Image 1" height="250">
    <img src="https://github.com/user-attachments/assets/9f02a377-cea9-4293-9bd7-c5629c6aa766" alt="Image 2" height="250">
</p>

# Local Outlier Factor (LOF) Anomaly Detection

![](https://github.com/user-attachments/assets/f425ef6b-13ff-43dd-9a3c-026a20e420e9)

## How It Works

Local Outlier Factor (LOF) is an unsupervised learning algorithm used for anomaly detection. The key idea behind LOF is to measure the local density deviation of a given data point with respect to its neighbors. The algorithm identifies points that have a significantly lower density than their neighbors as anomalies. Works on KNN.

### Key Concepts

1. **Local Density**:
   - The local density of a point is estimated by calculating the distance between the point and its nearest neighbors.
   - A point's local density is considered low if the average distance to its neighbors is high, indicating that the point is an outlier compared to its surrounding points.

2. **Reachability Distance**:
   - The reachability distance is defined for a point `A` with respect to another point `B` as the maximum of the distance between `A` and `B`, and the minimum distance required to reach `B` from any of its nearest neighbors.
   - This distance helps in comparing the density of different points by ensuring that outliers do not overly influence the distance calculations.

3. **Local Reachability Density (LRD)**:
   - The LRD of a point is the inverse of the average reachability distance from its neighbors.
   - Points in dense clusters will have a high LRD, while outliers will have a low LRD.

4. **LOF Score**:
   - The LOF score is calculated by comparing the LRD of a point to the LRDs of its neighbors. 
   - A point with a high LOF score (greater than 1) is considered an anomaly because its density is significantly lower than that of its neighbors.
   - The LOF score is used to rank the data points according to their degree of outlierness.

## Applications - Anomoly Detection

- Fraud detection in financial transactions
- Intrusion detection in cybersecurity
- Fault detection in manufacturing systems
- Health monitoring systems

By leveraging these algorithms, it is possible to efficiently and accurately identify anomalies in various datasets, making it a valuable tool for detecting unusual patterns that could indicate problems or unusual behavior.
