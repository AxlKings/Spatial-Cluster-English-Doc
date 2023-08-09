Preprocessing
====================


Formatting Data Table
--------------------

To obtain data separated into variables with the format used by the library's methods, two different functions are provided.

The first one is *attributes_format*, which separates the data into position (longitude, latitude) and attributes.

### Parameters

- **df**: *(Pandas DataFrame)* Contains the data to be used.

### Return

- **features_position**: *(Pandas DataFrame)* Contains the longitude and latitude of the data.

- **features_X**: *(Pandas DataFrame)* Contains the attributes of the data (excluding longitude and latitude).


```
   from SpatialCluster.preprocess.data_format import attributes_format
   features_position, features_X = attributes_format(df)
```

The second one is *attributes_with_zone_format*, which separates the data into position (longitude, latitude) and attributes with an additional column indicating the zone to which each point belongs (in the example dataset, this corresponds to "comuna").

### Parameters

- **df**: *(Pandas DataFrame)* Contains the data to be used.

- **zona**: *(string)* Name of the column that contains the zone to which each point belongs.

### Return

- **features_position**: *(Pandas DataFrame)* Contains the longitude and latitude of the data.

- **features_X**: *(Pandas DataFrame)* Contains the attributes of the data, including the zone column (excluding longitude and latitude).

```
   from SpatialCluster.preprocess.data_format import attributes_with_zone_format
   features_position, features_X = attributes_with_zone_format(df, zona = "comuna")
```


Adjacency Matrix
---------------------

The *adjacencyMatrix* function creates an adjacency matrix in which each point is related to its nearest neighbors according to a specific criterion.

The following criteria can be used to define a neighborhood for creating the adjacency matrix:

By k nearest neighbors (criterion "*k*").

By neighbors within a radius r (criterion "*r*").

By neighbors within a radius r, with a minimum of k_min neighbors. If there are not enough points to meet this threshold, k nearest neighbors will be used (criterion "*rk*").

### Parameters

- **features_X**: *(Pandas DataFrame)* Contains the attributes of the data (excluding longitude and latitude).
- **r**: *(float)* Maximum distance in meters at which a point will be considered a neighbor (neighborhood radius for each point). Default: 300.0
- **k**: *(int)* Maximum number of neighbors in the neighborhood for each point. Default: 5
- **min_k**: *(int)* Minimum number of neighbors required for the neighborhood if using the "rk" criterion. Default: 2
- **criteria**: *(string)* Criterion used to determine neighborhoods (*k*, *r*, *rk*). Default: "k"
- **leafsize**: *(int)* Number of points at which the KDTree algorithm switches to brute force. For more information, refer to the [Documentación de KDTree](https://docs.scipy.org/doc/scipy/reference/generated/scipy.spatial.KDTree.html). Default: 10

### Return

- **A**: *(Numpy Matrix)* Adjacency matrix

```
   from SpatialCluster.preprocess.adjacency import adjacencyMatrix
   A = adjacencyMatrix(features_position, r = 300.0, k = 5, min_k = 2, criteria = "k", directed = True, leafsize = 10)
```


Rings
------------

The *rings* function uses the weighting of neighbors' data for each point, creating a new column with these weighted values. This process is repeated for each original column in the dataset, thus smoothing the difference in attributes between nearby points. For each original column, as many columns will be created as the number of parameters entered in *max_radios* or *max_neighbours*, considering the new corresponding neighborhood definition for each parameter.

For example: If *max_radios* corresponds to (300, 400, 500), for each column in *features_X*, a column will be created that uses neighborhoods of 300 meters, another column using neighborhoods of 400 meters, and finally another column using neighborhoods of 500 meters.

The following criteria can be used to define a neighborhood for creating the rings:

- By k nearest neighbors (criterion "*k*").

- By neighbors within a radius r (criterion "*r*").

- By neighbors within a radius r, with a minimum of k_min neighbors. If there are not enough points to meet this threshold, k nearest neighbors will be used (criterion "*rk*").

### Parameters

- **features_X**: *(Pandas DataFrame)* Contains the attributes of the data (excluding longitude and latitude).
- **features_position**: *(Pandas DataFrame)* Contains the longitude and latitude of the data.
- **criteria**: *(string)* Criterion used to determine neighborhoods (*k*, *r*, *rk*). Default: "k"
- **max_radios**: *(List of floats)* List of radii in meters used to define neighborhoods. Default: [200.0, 300.0, 400.0]
- **max_neighbours**: *(List of floats)* List of radii in meters used to define neighborhoods. Default: [200.0, 300.0, 400.0]
- **weight_mode**: *(string)* Criterion used for weighting ("*Simple*" or "*Distance Inverse*"). Default: "Simple"
- **keep_original_value**: *(bool)* Determines whether the original columns are kept or not. Default: True
- **smoothing**: *(float)* Parameter used to smooth distances when weighting data (useful when weighting with the inverse of distance, in case these are very close to 0). Default: 1e-08
- **normalize**: *(bool)* Determines whether distances are normalized, which prevents some data from being overrepresented when weighted by the inverse of distance. Default: True
- **leafsize**: *(int)* Number of points at which the KDTree algorithm switches to brute force. For more information, refer to the [Documentación de KDTree](https://docs.scipy.org/doc/scipy/reference/generated/scipy.spatial.KDTree.html).  Default: 10

### Return

- **features_rings**: *(Pandas DataFrame)* Contains the newly created columns.

```
   from SpatialCluster.preprocess.rings import rings
   features_rings = rings(features_X, features_position, criteria="k", max_radios=[200.0, 300.0, 400.0], max_neighbours=[200, 500, 1000], weight_mode="Simple", keep_original_value=True, smoothing=1e-08, normalize=True, leafsize=10)
```

