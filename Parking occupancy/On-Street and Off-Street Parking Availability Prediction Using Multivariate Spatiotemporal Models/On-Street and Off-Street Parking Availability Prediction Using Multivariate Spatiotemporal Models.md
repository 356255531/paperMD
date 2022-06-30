# On-Street and Off-Street Parking Availability Prediction Using Multivariate Spatiotemporal Models
*IEEE TRANSACTIONS ON INTELLIGENT TRANSPORTATION SYSTEMS*

## Dataset
### Form
Contineous time-series occupancy $\{O_1, ..., O_t\}$, where $O_t \in [0, 1]$ with a time duration $D_t$.
### Static parking sensors
Yes
### Topological information
The parking area has been clustered into different zones with simiar parking patterns. The spatial correlation has been derived using the geographical distance of two blocks.
### Time granularity
Each zone has different duration $D_t$.
### Location
San Francisco
## Model
Autoregressive model
## Approach / Experient
This paper propose to solve the problem of parking availability prediction using autoregressive models. One other important observation is that the prediction of parking occupancy is significantly correlated with its spatial and temporal values. The developed algorithm learns an autoregressive model that integrate the potential temporal and spatial correlation into the parking availability prediction based on its historical data.
### Evaluation metrics
This paper the developed method in three scenarios with the follwoing metrics,
+ Mean Absolute Percentage Error (MAPE)
+ Number of error occurance
## Comment
This paper is well-written and the comparison is more solid and reasonable.