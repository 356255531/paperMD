# On-Street Parking Prediction Using Real-Time Data
*2018 21st International Conference on Intelligent Transportation Systems (ITSC)*
## Dataset
### Form
Contineous time-series occupancy $\{O_1, ..., O_t\}$ for each time stamp $t$, where $O_t \in [0, 1]$ with a time duration $D_t$.
### Static parking sensors
Yes
### Topological information
The parking area has been gridrized while each block should equipped with at least one sensor.  Each tile is a square with 500m sides
### Location
Los Angel
## Model 
recurrent neural networks (RNNs) 
## Approach / Experient
This paper presents four algorithms for on-street parking prediction
+  Algo 1 uses only the availability’s historical mean and standard deviation with no assumption on its distribution
+  Algo 2 assumes that availability is normally distributed
+  Algo 3 uses real-time information and models the availability variation as a normal random variable
+ Algo 4 uses real-time information but models vehicle arrivals and departures as non-homogeneous Poisson processes

### Evaluation metrics
+ Regression Metric: Mean absolute error (MAE)
+ Classification Metrics: False positive,  false negative rates ($FPR$ and $FNR$) and $Y = TPR − FPR$