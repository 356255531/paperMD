# Spatio-temporal Parking Behaviour Forecasting and AnalysisBefore and During COVID-19

**Authors:** Shuhui Gong, Xiaopeng Mo, Rui Cao, Yu Liu, Wei Tu, Ruibin Bai

**Conference:** DeepSpatial '21: 2nd ACM SIGKDD Workshop on Deep Learning for Spatiotemporal Data, Applications, and Systems

**Date:** 15 August 2021

## Goal

Use predictive model that use also spacial dependency rather than only consider temporal dependency

## Location

Ningbo, China

## Dataset: 

Data from 136 parking lots data of over onemillion records before and during COVID-19.
Half year time span, but data collected on sparse days.
After data cleaning it is provided the average occupancy per hour of each parking lot.

## Parking sensors

Yes

### Topological information

Spatial connection graph between parking lot is used

### Time granularity

Discrete time 

## Model 

1. Build the connection graph from different locations.
2. Use a temporal graph convolution network to make spatio-temporal forecasting.

## Approach / Experient

This approach introduces connection graph in order to model spacial dependencies between parking lots rather than baseline model which takes into account just the time-related features.
 (If one parking lot is full at a certain time, probably also a nearby parking lot will be full)

## Evaluation metrics

+ Root Mean Squared Error (RMSE)
+ Mean Absolute Error (MAE)
+ Mean Absolute Percentage Error (MAPE)
