# A deep learning approach to real-time parking occupancy prediction in spatio-temporal networks incorporating multiple spatio-temporal data sources

**Authors:** Shuguan Yang, Wei Ma, Xidong Pi, Sean Qian

**Journal:** Transportation Research Part C: Emerging Technologies, Vol. 107

**Date:** Oct 2019

## Goal

Deep learning model for predicting block-level parking occupancy 30 min in advance using multiple data sources


## Dataset: 

Parking meter transactions, traffic speed data, roadway networks, and weather conditions --> Case study in Pittsburgh Downtown


### Topological information

The parking area has been clustered into different blocks.

## Model 

Graph-Convolutional Neural Networks (GCNN) to extract the spatial relations of traffic flow in large-scale networks, and utilizes Recurrent Neural Networks (RNN) with Long-Short Term Memory (LSTM) to capture the temporal features

## Useful insights:

* The model outperforms baseline methods including multi-layer LSTM and LASSO in the case study.

* The prediction model works better for business areas than for recreational locations.

* Incorporating traffic speed and weather data can significantly improve prediction performance.


