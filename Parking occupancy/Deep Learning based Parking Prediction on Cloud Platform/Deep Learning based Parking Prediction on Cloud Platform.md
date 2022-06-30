# Deep Learning based Parking Prediction on Cloud Platform
*2018 4th International Conference on Big Data Computing and Communications*
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
Unknown
## Model 
Long Short-Term Memory (LSTM) network
## Approach / Experient
This paper propose a cloud achitecture for real-time parking availability prediction. A LSTM is trained every 2 hours with the newly collected data for replacing the old one.
No significant algorithmic contribution, a pure system design paper.
### Evaluation metrics
+ Mean squred error (MSE)