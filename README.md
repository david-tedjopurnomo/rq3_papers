# RQ3 Papers Read 

**Haitao Yuan, Guoliang Li, Zhifeng Bao, and Ling Feng. 2020. [Effective Travel Time Estimation: When Historical Trajectories over Road Networks Matter](https://baozhifeng.net/papers/sigmod20-deepod.pdf). SIGMOD 2020**

This paper explores the usage of a neural network to perform OD travel time estimation. That is, given a pair of origin and destination points, and a departure time, predict the travel time of the trip. 

Prof. Bao has recommended an improvement to this task. In addition to predicting the travel time, we can also predict the travel path. I will elaborate more on the "Promising Ideas" section below. 

**Fuat Basık, Hakan Ferhatosmanoğlu, and Buğra Gedik. 2020. [SLIM: Scalable Linkage of Mobility Data](https://dl.acm.org/doi/10.1145/3318464.3389761). SIGMOD 2020**

This paper explores a unique problem of mobility data linkage. Mobility data linkage is synonymous to entity resolution. Given two location datasets (i.e. usage records from a location-based service), mobility data linkage finds entities (i.e. users) that has exactly one location data in both datasets. 

It is surely a unique problem, but I don't find it too interesting. 

**Shuang Wang and Hakan Ferhatosmanoglu. 2021. [PPQ-Trajectory: Spatio-temporal Quantization for Querying in Large Trajectory Repositories](http://vldb.org/pvldb/vol14/p215-wang.pdf). VLDB 2021 (preprint).**

This paper explores the problem of approximate and exact spatio-temporal queries over compressed trajectories. I haven't read too much about it, but I don't think this is a good topic to explore because it's too similar to the second research question. Additionally, approaching this problem using a deep neural network doesn't make sense because using a vector representation is inherently approximation-based. 

**An Yan and Bill Howe. 2019. [Fariness in Practice: A Survey on Equity in urban Mobility](http://sites.computer.org/debull/A19sept/p49.pdf). IEEE Data Engineering Bulletin.**

**An Yan and Bill Howe. 2020. [Fairness-Aware Demand Prediction for New Mobility](https://ojs.aaai.org//index.php/AAAI/article/view/5458). AAAI 2020.**

These two papers explore the topic of fairness in machine learning in the context of spatio-temporal prediction. In particular, the latter paper explores the usage of a hybrid Convolutional Neural Network to perform fairness-aware demand prediction. It captures both region-based fairness gap (RFG) and individual-based fairness gap (IFG) as two metrics of fairness. 

While it is a novel and perhaps underexplored problem, the topic of machine learning fairness is not so interesting to me. I'll try to have a go at more papers to see if I'll be more interested, but this is low in the priority list compared to the other topics here. 

# Promising Ideas - Ordered by Priority 

**Priority 1: Step-by-step route recommendation** 

A similar, but different problem to the above. For a travel path prediction, we predict the most likely route, with the ground truth being the actual travel time and travel path. Thus, the metric of performance is in how closely our model predicts the travel time and travel path. However, for a route recommendation, there is no ground truth; the task is to minimize the travel time. 

This task uses map-matched trajectories because it is a better representation of road networks. Step-by-step recommendation takes in a pair of origin and destination points, and the departing time. In step-by-step recommendation, we predict the whole route not at once, but edge-by-edge. That is, given the current position and current timestamp, we calculate the best route at that time and traverse one edge through this route. Then, we update the current position and the current timestamp to simulate a vehicle moving through that edge. Then, we find the best route and simulate a vehicle moving one edge on that route again. We repeat this until we reach the destination. 

I would imagine that this task combines deep neural networks and graph theory. A deep neural network is used to predict the travel time of an edge at a certain time period (e.g. 5.00 to 5.30 PM). This will create a travel time dictionary. We use this dictionary in conjunction with graph theory to construct the optimal route and get the travel time. To compare this method with baseline models, we need to have a ground truth travel time for each edge. A simple approach is to take the mean travel time of all trajectories passing each edge. With the ground truth travel time for each edge calculated, we can compare our method with other baselines by getting the route recommendations and then summing the travel time of each edge. 

A difficulty with this problem is in justifying its novelty, since Google Maps may implement such approach already. Therefore, the tasks are: **doing some research on Google Maps' traffic information system and finding state-of-the-art route recommendation system to find how these kinds of research is typically done (i.e. ground truth, evaluation metric, current state-of-the-art, etc)**

**Priority 2: Fairness in Machine-Learning-based spatio-temporal applications**

Fairness in machine learning is a hot topic that is gaining traction. There is a good chance that papers covering this topic will be accepted easier. Currently, the topic of ride recommendation has been covered by the AAAI2020 paper above. **My task is to read the survey paper to find any other unexplored topics/subtopics in the fairness machine-learning-based spatio-temporal applications domain**. 

**Priority 3: Machine-learning-based map-matching** 

Since map-matching is inherently approximate, machine learning can be applied. We need to have a map-matching model that is robust to GPS errors and sampling rate. GPS errors may move an original point far enough that they are assigned to the wrong road and a very low sampling rate may cause two subsequent trajectory points to be mapped to two edges that are not connected, in which case we have to infer the missing point. **There are two tasks that needs to be done. The first is to identify if there are any current research that uses machine learning to perform map-matching. The second is to motivate the problem; finding out if thes GPS errors and sampling rate are a common occurence and how to formalize these problems** 

**Priority 4 (low priority): Travel time and travel path prediction**

Inspired by Prof. Bao's SIGMOD2020 paper. In addition to predicting the travel time given a pair of OD points, we also predict the route taken. I like this research problem because it can be extended to a full system if we would like to explore that option. Additionally, I don't think the prediction of both travel time and travel path is a commonly explored problem. 

The issue with this research topic is that once a travel path is predicted, predicting the travel time is trivial; we only need to find the average travel time for the edges in the predicted path and sum them together. Additionally, we need to also justify the need for these dual prediction. Is this a real and significant problem worth pursuing? 

**Priority 5 (low priority): Next path prediction**

This is a topic that was recommended by Prof. Bao, but there hasn't been any discussion regarding this in 12th November meeting. This is something that should be in very low priority, i.e. as a final resort. 
