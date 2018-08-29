
# Clustering

## 1. Introduction

Clustering techniques are among the most popular unsupervised machine learning algorithms. The main idea behind clustering is that you want to group objects into similar classes, in a way that:

- intra-class similarity is high
- inter-class similarity is low

What does *similarity* mean? You should be thinking of it in terms of *distance*. The closer two points are, the higher their similarity.  

When thinking about clustering, is useful to make a distinction between *hierarchical* and *nonhierarchical* clustering algorithms:

- In cluster analysis, an **agglomerative hierarchical** algorithm starts with *n* clusters (where *n* is the number of observations, so each observation is a cluster), then combines the two most similar clusters, combines the next two most similar clusters, and so on. A **divisive** hierarchical algorithm does the exact opposite, going from 1 to *n* clusters.

- A **nonhierarchical** algorithm chooses *k* initial clusters and reassigns observations until no improvement can be obtained. How initial clusters and reassignemnts are done depends on the specific type of algorithm.

An essential understanding when using clustering methods is that you are basically trying to group data points together without actually knowing what the _actual_ cluster/classes are. This is also the main distinction between clustering and classification (which is a *supervised* learning method). This is why technically, you also don't know how many clusters you're looking for.

## 2. Non-hierarchical algorithms: k-means clustering

k means clustering is the most well-known clustering technique, and belongs to the class of non-hierarchical clustering methods. When performing k-means clustering, you're essentially trying to find $k$ cluster centers as the mean of the data points that belong to these clusters.
One thing about k means clustering that makes k means clustering challenging is that the number *k* needs to be decided upon before you start running the algorithm.

The k means clustering algorithm is an iterative algorithm that rearches for a pre-determined number of clusters within an unlabeled dataset, and basically works as follows:

**1.** Select k initial seeds  
**2.** Assign each observation to the clusted to which it is "closest"   
**3.** Recompute the cluster centroids  
**4.** Reassign the observations to one of the clusters according to some rule  
**5.** Stop if there is no reallocation.  

Two assumptions are of main importance for the k means clustering algorithm.

1. To compute the "cluster center", you calculate the (arithmetic) mean of all the points belonging to the cluster.
2. Reassigning works in a way that each point is closer to its own cluster center than to other cluster centers.

<center><h3>Visualization of K-Means Clustering Algorithm in Action</h3>
<img src='good-centroid-start.gif'></center>

## Advantages & Disadvantages of K-Means Clustering

The advantages of the K-Means Clustering approach are:

* Very easy to implement!
* With many features, K-Means is usually faster than HAC (as long as K is reasonably small).
* Objects are locked into the cluster they are first assigned, and can change as the centroids move around.  
* Clusters are often tighter than those formed by HAC. 

However, this algorithm also comes with several disadvantages to consider:

* Quality of results depends on picking the right value for K.  This can be a problem when we don't know how many clusters to expect in our dataset. 
* Scaling our dataset will completely change the results.  
* Initial start points of each centroid have a very strong impact on our final results. A bad start point can cause sub-optimal clusters (see example below)

<center><h3>K-Means Clustering Algorithm in With Bad Centroid Initialization</h3>
<img src='bad-centroid-start.gif'></center>


## 3. Hierarchical Agglomerative Clustering

hierarchical clustering refers to a collection of clustering algorithms that all build
upon the same principles: The algorithm starts by declaring each point its own cluster,
and then merges the two most similar clusters until some stopping criterion is
satisfied.  The algorithm for Hierarchical Aggolmerative Clustering works as follows:

1. Consider each object as a unique cluster.
2. Evaluate the pair-wise distance between all clusters.
3. Find the pair of clusters with the shortest distance, merge them into a new cluster.  
4. Evaluate the distances from this new cluster to all other clusters.
5. Repeat steps 2-5 until only a single giant cluster remains.  

Note that this describes the algorithm for a **_bottom-up_** approach.  Top-down approaches also exist, which are essentially the exact opposite of this--start with all data in one giant cluster and divide until all clusters consist of a single object.  However, it should be noted that the top-down approach is much more rare, and bottom-up tends to provide the best results in most cases. 

<img src='HAC-Dendrogram.png'>

##  Advantages & Disadvantages of HAC

HAC is useful as a clustering algorithm because:

* It produces an ordered relationship between clusters, which can be useful when visualized. 
* Smaller clusters are created.  This allows us to get a very granular understanding of our dataset, and zoom in at the level where the clusters make the most sense to us (note the coloration of the lines in the example dendrogram above).

However, this algorithm is also built on some assumptions with can be disadvantages:

* Results are usually dependent upon the distance metric used.  
* Objects can be grouped 'incorrectly' early on, with no way to relocate them.  For instance, consider two points that belong to separate clusters, but are both nearer to each other than the center of the cluster they actually belong to (both are near the "boundary" between their cluster and the opposing cluster). These will be incorrectly grouped as a cluster, which will throw off the clustering of the groups they actually belong to, as well. 
