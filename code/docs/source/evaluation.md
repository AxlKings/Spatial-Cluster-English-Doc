Evaluation
===========

Below are two measurements for comparing clusterings. Both are commonly used together since their purpose is the same, but they have different theoretical bases. The value is 0 when the compared partitions are random and independent, and it is 1 when they are identical.

ARI
------------

To compare two attribute map clusterings, you can use the ARI (Adjusted Rand Index) function, which returns a real number between 0 and 1 indicating the degree of similarity between the two solutions.

### Parámetros

- **clustering_1**: *(Numpy Array)* Contains the clusters to which each point belongs for clustering 1.
- **clustering_2**: *(Numpy Array)* Contains the clusters to which each point belongs for clustering 2.

### Return

- **ARI**: *(float)* ARI score.

```
   from SpatialCluster.metrics.ARI import ARI
   ari = ARI(clustering_1, clustering_2)
```

If you want to compare more than one pair of maps at once, you can generate a matrix that shows the ARI relationship for each pair of clusterings.

### Parameters

- **clusterings**: *(Pandas DataFrame)* Contains the clusters to which each point belongs for the different clusterings to be compared.
- **plot**: *(bool)* Indicates whether to display the matrix graphically.

### Return

- **ARI_matr**: *(Pandas DataFrame)* Contains the ARI score for each pair of clusterings.

```
   from SpatialCluster.metrics.ARI import ARI_matrix
   ari_matr = ARI_matrix(clusterings, plot=True)
```


AMI
------------

To compare two attribute map clusterings, you can use the AMI (Adjusted Mutual Information) function, which returns a real number between 0 and 1 indicating the degree of similarity between the two solutions.

### Parameters

- **clustering_1**: *(Numpy Array)* Contains the clusters to which each point belongs for clustering 1.
- **clustering_2**: *(Numpy Array)* Contains the clusters to which each point belongs for clustering 2.

### Return

- **AMI**: *(float)* AMI score.

```
   from SpatialCluster.metrics.AMI import AMI
   ami = AMI(clusters_map1, clusters_map2)
```

If you want to compare more than one pair of maps at once, you can generate a matrix that shows the AMI relationship for each pair of clusterings.

### Parameters

- **clusterings**: *(Pandas DataFrame)* Contains the clusters to which each point belongs for the different clusterings to be compared.
- **plot**: *(bool)* Indicates whether to display the matrix graphically.

### Return

- **AMI_matr**: *(Pandas DataFrame)* Contains the AMI score for each pair of clusterings.

```
   from SpatialCluster.metrics.AMI import AMI_matrix
   ami_matr = AMI_matrix(clusterings, plot=True)
```