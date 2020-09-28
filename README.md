# One-dimensional spatial convolutions of EEG data

## Introduction

EEG data are usually presented visually as two-dimensional data, one spatial and one temporal dimension. The recording skalp electrodes measures the cortical electrical field from positions in a three-dimensional space, roughly corresponding to a half sphere. Presenting the data in one spatial dimension results in spatial discontinuities. This may result in disruption of spatial invariant features, possibly making analysis by convolutions inefficient.

<p align="center">
<img src="https://github.com/Svanteberg/Spatial-convolutions-of-EEG-data/blob/master/images/10-20_transform.png" width="50%">
</p>

There are 21! ≈ 5.1•10<sup>19</sup> ways of ordering the electrodes of a 21 electrode montage, making it hard to explore and finding the optimal order. Finding orders were neighboring electrodes in three dimensions are placed as close as possible in one dimension may result in better results when using convolutions.

Transforming by taking the electrodes columnwise, using the same direction in the columns, results in some neighboring electrodes being parted and a filter of size 3 will miss a feature involving the electrodes (ortho-columnwise):

<p align="center">
<img src="https://github.com/Svanteberg/Spatial-convolutions-of-EEG-data/blob/master/images/col_orto.png" width="100%">
</p>

However, changing the direction between columns make the same electrodes one-dimensional neighbors (anti-columnwise):

<p align="center">
<img src="https://github.com/Svanteberg/Spatial-convolutions-of-EEG-data/blob/master/images/col_anti.png" width="100%">
</p>

Below is an example of just using the order in which the channels are stored automatically by the recording system, resulting in large discontinuities (original): 

<p align="center">
<img src="https://github.com/Svanteberg/Spatial-convolutions-of-EEG-data/blob/master/images/tuh_order.png" width="100%">
</p>

## Method

To test the hypothesis that the order of the electrodes affects the results when using convolutional networks, a simple data set was created. Eight spatial features was defined as

<p align="center">
<img src="https://github.com/Svanteberg/Spatial-convolutions-of-EEG-data/blob/master/images/categories.png" width="100%">
</p>

Data was generated by summing a field of random values with a feature, also having some random variation in amplitude:

<p align="center">
<img src="https://github.com/Svanteberg/Spatial-convolutions-of-EEG-data/blob/master/images/movie.gif" width="50%">
</p>

The data thus have no temporal variation.

As a measure of discontinuity, the Chebyshev distance D<sub>C</sub> was used. In this measure, neighbors of an electrode lie on the unit circle and all electrodes together form a 3x3 matrix. A discontinuity was then defined as when for two one-dimensional neighbors

<p align="center">D<sub>C</sub> = max(|x<sub>2</sub>-x<sub>1</sub>,y<sub>2</sub>-y<sub>1</sub>|) > 1</p>

in the two-dimensional grid approximation. The number of neighboring pairs in the one-dimensional array with D<sub>C</sub> > 1 was used to assess the degree of discontinuity of a transformation

<p align="center"><font size="20">∑<font><sub>k</sub>d<sub>k</sub>, d<sub>k</sub> = 1 if D<sub>C</sub> > 1 or else 0</p>

The minimum filter size F<sub>min</sub> to cover the unit circle in all cases is calculated as

<p align="center">F<sub>min</sub> = max<sub>i</sub>(max<sub>j,k</sub>(|F<sub>1D</sub>(x<sub>ij</sub>)-F<sub>1D</sub>(x<sub>ik</sub>)|)), j≠k</p>

where F<sub>1D</sub> is the transformation from two (or three) dimensions to one, i the electrode in the center of a unit circle and j and k are unique elements of the 3x3 matrix.

Using the above defined discontinuity measure, the ortho-columnwise transformation have 4, the anti-colmnwise 0 and the original ordering 18 discontinuities. The minimum filter sizes are 11, 11 and 20, respectively.

| Order | Discontinuities | Minimum filter size |
| :---: | :---: | :---: |
| Ortho-columnwise | 4 | 11 |
| Anti-columnwise | 0 | 11 |
| Original | 18 | 20 |


## Results

<p align="center">
<img src="https://github.com/Svanteberg/Spatial-convolutions-of-EEG-data/blob/master/images/chebyshev_tps_correlation_for_features.png" width="100%">
</p>
