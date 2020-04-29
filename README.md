# One-dimensional spatial convolutions of EEG data

## Introduction

EEG data are usually presented visually as two-dimensional data, one spatial and one temporal dimension. The recording skalp electrodes measures the cortical electrical field from positions in a three-dimensional space, roughly corresponding to a half sphere. Presenting the data with one spatial dimension results in spatial discontinuities. This logically results in disruption of spatial invariant features, possibly making analysis by convolutions harder.

<p align="center">
<img src="https://github.com/Svanteberg/Spatial-convolutions-of-EEG-data/blob/master/images/10-20_transform.png" width="50%">
</p>

There are 21! ways of ordering the electrodes of a 21 electrode montage, making it hard to explore and find the optimal order. Finding orders were neighboring electrodes in three dimensions are placed as close as possible in one dimension may result in better results when using convolutions. Transforming by taking the electrodes columnwise, using the same direction in the column, results in some neighboring electrodes ending upp as one-dimensional neighbors:

<p align="center">
<img src="https://github.com/Svanteberg/Spatial-convolutions-of-EEG-data/blob/master/images/col_orto.png" width="100%">
</p>

However, changing the direction between columns give neighbors that are spaced:

<p align="center">
<img src="https://github.com/Svanteberg/Spatial-convolutions-of-EEG-data/blob/master/images/col_anti.png" width="100%">
</p>

Below is an example of just using the order in which the channels are stored automatically by the recording system, resulting in large discontinuities: 

<p align="center">
<img src="https://github.com/Svanteberg/Spatial-convolutions-of-EEG-data/blob/master/images/tuh_order.png" width="100%">
</p>

## Method

<p align="center">
<img src="https://github.com/Svanteberg/Spatial-convolutions-of-EEG-data/blob/master/images/categories.png" width="100%">
</p>

<p align="center">
<img src="https://github.com/Svanteberg/Spatial-convolutions-of-EEG-data/blob/master/images/movie.gif" width="50%">
</p>

</p align="center">
max(|x<sub>2</sub>-x<sub>1</sub>,y<sub>2</sub>-y<sub>1</sub>|) > 1
</p>

## Results
