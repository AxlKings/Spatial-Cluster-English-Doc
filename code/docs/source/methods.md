Methods
========

DMoN
------------

Deep Modular Neural network (DMoN) is a graph-based neural network (GNN) used in this case for unsupervised clustering. It focuses on optimizing modularity, which is a measure used to determine the quality of clustering.

### Parameters


- **features_X**: *(Pandas DataFrame)* Contains the attributes of the data (excluding longitude and latitude). *DMoN* **does not** work with strings, and it's recommended that the data be of float type.
- **features_position**: *(Pandas DataFrame)* Contains the longitude and latitude of the data.
- **A**: *(Numpy matrix)* Adjacency matrix used. If not provided, the adjacencyMatrix method from SpatialCluster will be used to create one. Default: None
- **criteria**: *(string)* Criterion used to create the adjacency matrix (*k*, *r*, *rk*). Default: "k"
- **r_max**: *(float)* Maximum radius in meters used for adjacency matrix creation if needed. Default: 300.0
- **n_clusters**: *(int)* Number of clusters considered by the method for grouping the data. Default: 4
- **reg**: *(float)* Non-negative parameter within the range [0,1] that weights the regularization of the loss function to avoid trivial solutions like clustering all the data in the same cluster. Default: 1.0
- **dropout**: *(float)* Parameter within the range [0,1] to prevent overfitting to the data. Higher values help prevent overfitting but can affect training, requiring more data or epochs. Default: 0.0
- **num_epochs**: *(int)* Number of training epochs. Very high values might lead to overfitting. Default: 500
- **learning_rate**: *(float)* Parameter within the range [0,1] indicating the rate of adjustments the network will make in each epoch. Very high values can lead to aggressive changes, potentially preventing it from finding the optimal solution. Low values mean slower learning, requiring more epochs and data for training.

### Return

- **DMoN_areas_to_points**: *(dict)* For each cluster, it stores the points belonging to that cluster.
- **DMoN_clusters**: *(Numpy Array)* Contains points labeled according to the cluster they were assigned to.

``` 
   from SpatialCluster.methods.DMoN import DMoN_Clustering
   DMoN_areas_to_points, DMoN_clusters = DMoN_Clustering(features_X, features_position, A = None, criteria = "k", r_max = 300.0, n_clusters = 4, reg = 1.0, dropout = 0.0, num_epochs = 500, learning_rate = 0.001)
```

GMM
------------

This method allows you to use a Gaussian Mixture Model (GMM) probability distribution for clustering.

### Parameters

- **features_X**: *(Pandas DataFrame)* Contains the attributes of the data (excluding longitude and latitude). *GMM* **does not** work with strings, and it's recommended that the data be of float type.
- **features_position**: *(Pandas DataFrame)* Contains the longitude and latitude of the data.
- **n_clusters**: *(int)* Number of clusters considered by the method for grouping the data. Default: 4
- **covariance_type**: *(string)* Describes the type of covariance parameters. It must be one of the following:

   - "full": Each component has its own general covariance matrix.

   - "tied": All components share the same general covariance matrix.

   - "diag": Each component has its own diagonal covariance matrix.

   - "spherical": Each component has its own individual variance.

Default: "full"

- **tol**: *(float)* Tolerance threshold. Expectation-Maximization (EM) iterations will stop when the average gain of the lower bound is below this threshold. Default: 1e-3
- **reg_covar**: *(float)* Non-negative parameter for regularization added to the diagonal of the covariance matrix. Ensures positive definite covariance matrices. Default: 1e-6

### Return

- **GMM_areas_to_points**: *(dict)* For each cluster, it stores the points belonging to that cluster.
- **GMM_clusters**: *(Numpy Array)* Contains points labeled according to the cluster they were assigned to.

```
   from SpatialCluster.methods.GMM import GMM_Clustering
   GMM_areas_to_points, GMM_clusters = GMM_Clustering(features_X, features_position, n_clusters = 4, covariance_type = "full", tol=1e-3, reg_covar=1e-6)
```

KNN
------------

K-Nearest Neighbors (KNN) is an approach that avoids the Modifiable Areal Unit Problem (MAUP). This method is based on multiscale aggregation of the *k* nearest neighbors of a location, comparing it statistically with a larger reference area where  *K* nearest neighbors are used (siendo *K > k*). This method distinguishes between two types of clusters: *hot spots* and *cold spots*.

### Parameters

- **features_X**: *(Pandas DataFrame)* Contains the attributes of the data (excluding longitude and latitude).
- **features_position**: *(Pandas DataFrame)* Contains the longitude and latitude of the data.
- **attribute**: *(string)* Indicates which column of features_X will be used to characterize the data.
- **threshold**: *(float/int/bool)* Threshold determining if a data point meets the criterion based on its *attribute* column.
- **location**: *(string)* Name of the column in *features_X* used to determine the location to which the data belongs (e.g., "comuna").
- **condition**: *(string)* Operator used (">", "<", ">=", "<=", "==") to check if the data meets the condition or not. Default: "<"
- **k**: *(int)* Minimum number of nearest neighbors used for the smaller area unit. Default: 1500
- **K**: *(int)* Minimum number of nearest neighbors used for the larger area unit. Default: 5000
- **alfa**: *(float)* Threshold to evaluate whether the data corresponds to a *cold spot* or *hot spot* with statistical significance. Default: 0.01
- **leafsize**: *(int)* Number of points at which the KDTree algorithm switches to brute force. For more information, refer to the [Documentación de KDTree](https://docs.scipy.org/doc/scipy/reference/generated/scipy.spatial.KDTree.html). Default: 10

### Return

- **KNN_areas_to_points**: *(dict)* For each cluster, it stores the points belonging to that cluster.
- **KNN_clusters**: *(Numpy Array)* Contains points labeled according to the cluster they were assigned to.

```
   from SpatialCluster.methods.KNN import KNN_Clustering
   KNN_areas_to_points, KNN_clusters = KNN_Clustering(features_X, features_position, attribute, threshold, location, condition="<", k=1500, K=5000, alfa = 0.01, leafsize=10)
```

SOM
------------

Self Organizing Map (SOM) is a type of artificial neural network capable of transforming complex and nonlinear statistical relationships between high-dimensional data elements into simple geometric relationships of low dimension. This method leverages this SOM property to perform clustering.

### Parameters

- **features_X**: *(Pandas DataFrame)* Contains the attributes of the data (excluding longitude and latitude). *SOM* does not work with strings, and it's recommended that the data be of float type.
- **features_position**: *(Pandas DataFrame)* Contains the longitude and latitude of the data.
- **n_clusters**: *(int)* Indica la cantidad de clusters que considerará el método para agrupar los datos. Por defecto: 4
- **som_shape**: *(tuple of ints)* Determines the topology of the neural network that *SOM* will use in the form (number_of_rows, number_of_columns). Default: (3,3)
- **sigma**: *(float)* Dispersion of the neighborhood function, should be appropriate for the *SOM* dimension used. Default: 0.5
- **learning_rate**: *(float)* Parameter within the range [0,1] that corresponds to the amount of initial information shared between neurons in each iteration of the network's training process. Default: 0.5
- **num_iterations**: *(int)* Number of iterations that will be performed in the training process. Default: 100

### Return

- **SOM_areas_to_points**: *(dict)* For each cluster, it stores the points belonging to that cluster.
- **SOM_clusters**: *(Numpy Array)* Contains points labeled according to the cluster they were assigned to.

```
   from SpatialCluster.methods.SOM import SOM_Clustering
   SOM_areas_to_points, SOM_clusters = SOM_Clustering(features_X, features_position, som_shape = (2,2), sigma=0.5, learning_rate=0.5, num_iterations = 100)
```

TDI
------------

TDI stands for a method based on Information Theory. It uses a weight matrix with Shannon divergence as the distance between points. Then, Spectral Clustering is applied to this matrix. This method allows profile curves with non-constant spatial scales and decomposition analysis with non-arbitrary area units.

### Parameters

- **features_X**: *(Pandas DataFrame)* Contains the attributes of the data (excluding longitude and latitude). *TDI* does not work with strings, and it's recommended that the data be of float type.
- **features_position**: *(Pandas DataFrame)* Contains the longitude and latitude of the data.
- **n_clusters**: *(int)* Indicates the number of clusters that the method will consider for grouping the data. Default: 4
- **A**: *(Numpy matrix)* Adjacency matrix representing the topology of the graph used for *Spectral clustering*. This matrix should represent a connected and symmetric graph to ensure consistent results. If no matrix is provided, the *adjacencyMatrix* will be used to create one. Default: None
- **k**: *(int)* Maximum number of nearest neighbors that the neighborhood will have for each point. Default: 20
- **leafsize**: Corresponds to the number of points at which the KDTree algorithm switches to brute force. For more information, refer to the [Documentación de KDTree](https://docs.scipy.org/doc/scipy/reference/generated/scipy.spatial.KDTree.html). Default: 10

### Return

- **TDI_areas_to_points**: *(dict)* For each cluster, it stores the points belonging to that cluster.
- **TDI_clusters**: *(Numpy Array)* Contains points labeled according to the cluster they were assigned to.

```
   from SpatialCluster.methods.TDI import TDI_Clustering
   TDI_areas_to_points, TDI_clusters = TDI_Clustering(features_X, features_position, n_clusters=4, A=A, k=20, leafsize=10)
```