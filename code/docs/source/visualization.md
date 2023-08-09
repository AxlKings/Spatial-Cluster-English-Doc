Visualization
===============

Plot Complete Map
-----------------------

The following method generates a map with all the points, colored according to the assigned cluster.

### Parameters

- **gdf**: *(GeoPandas DataFrame)* Contains the clusters to which each point belongs and the geometry to locate them geographically on the map. If the "geometry" column does not exist, the method will generate it from the "lon" and "lat" columns.
- **markersize**: *(int)* Size of the points on the map. Default: 30
- **figsize**: *(Tuple of ints)* Size of the figure that will contain the map. Default: (12,8)
- **path**: *(string)* Indicates the path and name to be used for saving the file (e.g., "/maps/map.png"). Default: None

### Return

- Does not return anything, it plots the generated map.

```
   from SpatialCluster.visualization.plotters import plot_map
   plot_map(gdf, markersize=30, figsize=(12,8), path=None)
```

Plot Random Sampling
----------------------------

The following method generates an interactive map with a random sampling of the points, colored according to the assigned cluster.

### Parameters

- **areas_to_points**: *(dict)* A dictionary that stores the points belonging to each cluster.
- **min_supp**: *(int)* Minimum number of points a cluster must have to appear.
- **max_samples_per_clusters**: *(int)* Maximum number of points to be shown for each cluster.
- **location**: *(Tuple of ints)* Longitude and latitude of the map's center position. Default: (-33.45, -70.65)
- **radius**: *(int)* Size of the circle representing each point. Default: 10
- **path**: *(string)* Indicates the path and name to be used for saving the file (e.g., "/maps/map.html"). Default: None

### Return

- **hmap**: *(Folium Map)* Generated interactive map.

```
   from SpatialCluster.visualization.plotters import plot_map_sample
   hmap = plot_map_sample(areas_to_points, min_supp=min_supp, max_samples_per_clusters=max_samples_per_clusters, location=location, radius=radius, path=None)
```
