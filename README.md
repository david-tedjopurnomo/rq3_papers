# RQ3 Papers Read 
Papers I read for RQ3

**Haitao Yuan, Guoliang Li, Zhifeng Bao, and Ling Feng. 2020. [**Effective Travel Time Estimation: When Historical Trajectories over Road Networks Matter**](https://baozhifeng.net/papers/sigmod20-deepod.pdf). In Proceedings of the 2020 ACM SIGMOD International Conference on Management of Data (SIGMOD '20).**

This paper explores the usage of a neural network to perform OD travel time estimation. That is, given a pair of origin and destination points, and a departure time, predict the travel time of the trip. 

Prof. Bao has recommended an improvement to this task. In addition to predicting the travel time, we can also predict the travel path. I will elaborate more on the "Promising Ideas" section below. 



# Promising Ideas

**Travel time and travel path prediction**

Inspired by Prof. Bao's SIGMOD2020 paper. In addition to predicting the travel time given a pair of OD points, we also predict the route taken. 

**Step-by-step route recommendation** 

A similar, but different problem to the above. For a travel path prediction, we predict the most likely route, with the ground truth being the actual travel time and travel path. Thus, the metric of performance is in how closely our model predicts the travel time and travel path. However, for a route recommendation, there is no ground truth; the task is to minimize the travel time. 

This task uses map-matched trajectories because it is a better representation of road networks. Step-by-step recommendation takes in a pair of origin and destination points, and the departing time. In step-by-step recommendation, we predict the whole route not at once, but edge-by-edge. That is, given the current position and current timestamp, we calculate the best route at that time and traverse one edge through this route. Then, we update the current position and the current timestamp to simulate a vehicle moving through that edge. Then, we find the best route and simulate a vehicle moving one edge on that route again. We repeat this until we reach the destination. 

I would imagine that this task combines deep neural networks and graph theory. A deep neural network is used to predict the travel time of an edge at a certain time period (e.g. 5.00 to 5.30 PM). This will create a travel time dictionary. We use this dictionary in conjunction with graph theory to construct the optimal route and get the travel time. To compare this method with baseline models, we need to have a ground truth travel time for each edge. A simple approach is to take the mean travel time of all trajectories passing each edge. With the ground truth travel time for each edge calculated, we can compare our method with other baselines by getting the route recommendations and then summing the travel time of each edge. 
