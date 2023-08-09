Dataset
=======

Origin
--------------

The dataset originally consists of administrative unit data from the census of Santiago, Chile, and other sources at the block level. These data contain various attributes that were grouped into three categories: Visual, Social, and Land Use.


Visual Attributes
-------------------------

These attributes were obtained from photographs of the corresponding physical locations, which were processed by a neural network. The following six visual characteristics were considered:

    - beautiful: (float) Indicates the perceived level of beauty in the image location.
    - boring: (float) Indicates how monotonous the image location appears.
    - depressing: (float) Indicates how sad the image location is perceived.
    - lively: (float) Indicates how lively or exciting the image location appears.
    - safe: (float) Indicates how safe the image location appears.
    - wealth: (float) Indicates how luxurious the image location appears.

Principal Components Analysis (PCA) was applied to reduce the number of features. The number of PCA dimensions that captured at least 80% of the variance was chosen, so for visual characteristics, only two dimensions ("visual_0", "visual_1") were sufficient.

Social Attributes
-------------------------

These attributes were obtained from the socioeconomic level of the 2012 Census, the proportion of immigrant residents from the 2017 Census, the 2020 constitutional plebiscite, and the first round of the 2021 presidential elections, all estimated at the block level. Lastly, data on surname distribution based on the alpha index by Bro, N., Mendoza, M. (2021) were obtained:

    - prom_nse: (float) Average socioeconomic level.
    - edad_prom: (float) Average age.
    - porcentaje_inmigrantes: (float) Proportion of immigrant residents.
    - prop_apruebo_promedio: (float) Proportion of residents who voted "approve" in the 2020 Constitutional Plebiscite.
    - mapuche_prom: (float) Average proportion of residents with a Mapuche surname.
    - elite_prom: (float) Average proportion of residents with an upper-class surname.

Principal Components Analysis (PCA) was applied to reduce the number of features. The number of PCA dimensions that captured at least 80% of the variance was chosen, so for social characteristics, only two dimensions ("social_0", "social_1") were sufficient.

Land Use Attributes
-------------------------

These attributes correspond to how the state classifies different areas of the city for tax declaration purposes. The following attributes were obtained:

    - prop_uso_A: (float) Proportion of land use designated for Armament.
    - prop_uso_C: (float) Proportion of land use designated for Commerce.
    - prop_uso_D: (float) Proportion of land use designated for Sports.
    - prop_uso_E: (float) Proportion of land use designated for Education.
    - prop_uso_F: (float) Proportion of land use designated for Forestry.
    - prop_uso_G: (float) Proportion of land use designated for Hospitality.
    - prop_uso_H: (float) Proportion of land use designated for Housing.
    - prop_uso_I: (float) Proportion of land use designated for Industry.
    - prop_uso_K: (float) Proportion of land use not coded.
    - prop_uso_L: (float) Proportion of land use designated for Storage.
    - prop_uso_M: (float) Proportion of land use designated for Mining.
    - prop_uso_O: (float) Proportion of land use designated for Business.
    - prop_uso_P: (float) Proportion of land use designated for Government.
    - prop_uso_Q: (float) Proportion of land use designated for Worship.
    - prop_uso_S: (float) Proportion of land use designated for Health.
    - prop_uso_T: (float) Proportion of land use designated for Transport.
    - prop_uso_V: (float) Proportion of land use designated for Other.
    - prop_uso_W: (float) Proportion of land use designated for Vacant.
    - prop_uso_Z: (float) Proportion of land use designated for Parking.
    - total_m2_manzana: (float) Total square meters used by the block.


Principal Components Analysis (PCA) was applied to reduce the number of features. The number of PCA dimensions that captured at least 80% of the variance was chosen, so for soil characteristics, four dimensions ("suelo_0", "suelo_1", "suelo_2", "suelo_3") were needed.

Usage 
------------

To access the dataset, simply use the following function:

```
   from SpatialCluster.datasets import load_manzana_data
   df = load_manzana_data()
```

Depending on the method you want to use, you can format the data appropriately using the following functions:

If you want to use the KNN method, use this function.

```
   from SpatialCluster.preprocess.data_format import attributes_with_zone_format
   features_position, features_X = attributes_with_zone_format(df, zona = "comuna")
```

If you want to use any other method offered by SpatialCluster, use this function.

```
   from SpatialCluster.preprocess.data_format import attributes_format
   features_position, features_X = attributes_format(df)
```