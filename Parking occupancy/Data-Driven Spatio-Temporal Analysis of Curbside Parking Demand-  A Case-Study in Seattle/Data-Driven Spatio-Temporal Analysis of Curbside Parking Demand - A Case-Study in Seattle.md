# Data-Driven Spatio-Temporal Analysis of Curbside Parking Demand: A Case-Study in Seattle

**Authors:** Anner Fiez and Lillian J. Ratliff

**Conference:** Submitted to IEEE Transactions on Intelligent Transportation Systems

**Date:** Sat, 2 Dec 2017

## Goal

* Analyze spatio/temporal characteristics of park demand and aggregate similar areas  using Gaussian Mixture Models
* Use data to improve parking policies (cost of park during day), reduce traffic jam, pollution and fuel consumption in a city.

## Location

Seattle

## Dataset: 

Parking transaction data (pay station + pay by phone data), block-face  supply data, and GPS location of the block-faces.
Data collection goes from June,2016 to August,2017 and was provided made available from the Seattle Department of Transportation (SDOT). Nearly 14million of paid parking transactions recorded in Seattle in this period of time.

## Parking sensors

No parking sensors. Ground truth computed as: occupancy = active transactions/park supply.

### Topological information

The parking area has been clustered into different zones with simiar parking patterns. The connectivity of blocks are NOT used!

### Time granularity

Each zone has a different granularity, however the park demand similarities were computed on several time-frames: hours/days/seasons

## Model 

Gaussian Mixture Model

## Useful insights:
* Based on two cited surveys, on  average,  people  would  be  willing  to  park  max 3.07blocks far away from their destination or less than 5 min walk. ( average speed: 1.4m/s*60s*5=420m) -> Possible order of magnitude for our tesselation size
* the main drivers of park demands are:
    * Time of the day
    * day of the week 
    * seasonality
    * concentration of bars and restaurants
    * type of area (residential, commercial, industrial)
    * tourist attractions


