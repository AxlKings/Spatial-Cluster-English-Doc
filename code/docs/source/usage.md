Introduction
=============


Spatial Cluster is an open-source library that aims to facilitate the generation of urban attribute maps that group data into different disjoint sets (clustering). The project consists of 5 main modules, which are as follows:

   -  **Preprocessing**: It offers various data preprocessing functions to make them usable by the methods included in the library.

   - **Methods**: Currently, it features 5 different methods that perform the clustering task.

   - **Visualization**: Currently, it provides two functions to generate corresponding maps using the results obtained after applying a clustering algorithm.

   - **Evaluation**: Currently, it includes two evaluation metrics for comparing pairs of maps (ARI and AMI).

   - **Dataset**: It offers a dataset collected from the Metropolitan Region of Chile, which meets the necessary requirements to utilize any method offered by the library.


Installation
------------

To use SpatialCluster, it must first be installed using pip:

```{eval-rst}
.. code-block:: console

   (.venv) $ pip install SpatialCluster
```

Next Steps
-----------------

To use the library, it is recommended to visit the [Methods](methods.md) and [Visualization](visualization.md) sections to see usage examples. It is also advisable to review the [Preprocessing](preprocess.md) section as it can be quite useful in obtaining good results.