# Parking Availability Prediction for Sensor-Enabled Car Parks in Smart Cities
*2015 IEEE Tenth International Conference on Intelligent Sensors, Sensor Networks and Information Processing (ISSNIP)*

## Dataset
### Form
Contineous time-series occupancy $\{O_1, ..., O_t\}$, where $O_t \in [0, 1]$ with a time duration $D_t$.
### Static parking sensors
Yes
### Topological information
The parking area has been clustered into different zones with simiar parking patterns. The connectivity of blocks are NOT used!
### Time granularity
Each zone has different duration $D_t$.
### Location
Melbourne and San Francisco
## Model 
+ Regression tree (RT)
+ Support vector regression (SVR)
+ Feed forward neural network (NN)
## Approach / Experient
This paper propose to solve the problem of parking availability prediction using machine learning. Author defines three feature sets and use three models to test on them.
### Evaluation metrics
+ Mean absolute error (MAE)
+ Root mean squared error (RMSE)
+ Coefficient of determination ($R^2$)