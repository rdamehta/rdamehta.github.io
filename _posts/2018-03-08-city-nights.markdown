---
title:  "Battle of the Clusters"
subtitle: "A Comparison of 3 Common Clustering Algorithims"
author: "Ravi"
avatar: "img/authors/the-wire-couch.png"
image: "img/clusters.jpg"
date:   2018-03-08 12:12:12
---


## Battle of the Clusters
---

I wanted to visually test three of the clustering algorithms that are commonly used on 7 data sets that are specifically designed to evaluate clustering algorithm effectiveness.

The three algorithims I'm going to use are 
K-means: k-means clustering.
Agglomerative clustering: hierarchical clustering (bottom up).
DBSCAN: density-based clustering.

Clustering, I believe, is particularly suited for visual representations, and it's very easy to gain an intuition on how each algorithim performs based on visuals.


For ease of use the 7 datasets I generated have 2 dimensions, an X and y coordinate. Remember that in unsupervised learning methods like clustering, there generally will not be "true labels."  I provided them here as colors simply as a convenience to be able to compare with he algorithims 



## Here are the 7 datasets clustered by color. We are going to see how close the clustering algorithms can get to these images.



![png](img/cluster_images/DBSCAN-vs-kmeans-vs-hierarchical_7_0.png)



![png](img/cluster_images/DBSCAN-vs-kmeans-vs-hierarchical_7_1.png)



![png](img/cluster_images/DBSCAN-vs-kmeans-vs-hierarchical_7_2.png)



![png](img/cluster_images/DBSCAN-vs-kmeans-vs-hierarchical_7_3.png)



![png](img/cluster_images/DBSCAN-vs-kmeans-vs-hierarchical_7_4.png)



![png](img/cluster_images/DBSCAN-vs-kmeans-vs-hierarchical_7_5.png)



![png](img/cluster_images/DBSCAN-vs-kmeans-vs-hierarchical_7_6.png)




### Flame

Which algorithm (visually) performs best?

<img src="img/cluster_images/DBSCAN-vs-kmeans-vs-hierarchical_14_0.png" alt="flame" style="width: 700px;height: 700px"/>


DBSCAN performed the best. The great thing about DBSCAN is that we can really tune its hyperparameters: epsilon (the distance between samples) and miniminum number of core samples needed to define a cluster.

Interestingly Kmeans and the heirarchal algorithims performed similarly. Looking at the center of the Kmeans we see the centers that the algorithm eventually converged on are 'off' in comparison to how we as humans visually see a flame.

### Agg

Which algorithm (visually) performs best?


<img src="img/cluster_images/DBSCAN-vs-kmeans-vs-hierarchical_16_0.png" alt="flame" style="width: 700px;height: 700px"/>


You can reallllyy tune DBSCAN, here I had epsilon (our distance between samples in a cluster) to be 0.218 and had the min number of sampels as 13.

Out of the box though, kmeans, and heirarchical clustering didn't do a bad job. you can see by how they grouped their clusters that both of these use distance metrics primarily. K means uses distances from a center point 'X', while Agglomerative/Heirarchal see which points are closest togethor, creates a group and then adds members by calculating the shortest distance from any member of the new group to another point not in the group. We set the groups to 7, so the algorithim stops when it has seven groups.


### Comp

Which algorithm (visually) performs best?


<img src="img/cluster_images/DBSCAN-vs-kmeans-vs-hierarchical_18_0.png" alt="flame" style="width: 700px;height: 700px"/>


DBSCAN performs best, but really, none of them are perfect. This demonstrates something that we should be aware of when using unsupervised clustering algorithims. is that clusters or groups with different distances, or densities will be seen as different groups. In this case, the red dots in the DBSCAN image are considered outliers or not belonging to a group.

### Jain


<img src="img/cluster_images/DBSCAN-vs-kmeans-vs-hierarchical_20_0.png" alt="flame" style="width: 700px;height: 700px"/>


I found this one really fascinating. I could have probably fine tuned DBSCAN even more, but regardless it found 3 groups instead fo two. again highlighting the issue with clusters that have intradistances between points. AKA if cluster A has a distance of 1, and cluster B has a distance 2, this is problematic for our algorithm.

I like how Kmeans and Agglomerative/Heirarchal attempt this. You can clearly see kmeans takes a mean centered approach and heirarchal takes a bottom up approach. 

### Pathbased


<img src="img/cluster_images/DBSCAN-vs-kmeans-vs-hierarchical_22_0.png" alt="flame" style="width: 700px;height: 700px"/>



DBSCAN for the win, theres a general theme isn't there?

### r15

my favorite data set of them all. Reminds of playing paintball.


<img src="img/cluster_images/DBSCAN-vs-kmeans-vs-hierarchical_24_0.png" alt="flame" style="width: 700px;height: 700px"/>

Kmeans and Agglomerative/Heirarchal perform perfectly right out of box. DBSCAN does well here too.
I'd say this is a threeway tie.


### Spiral

The spiral is where we can really see DBSCAN shine and gain some intuition on how the algorithm works


<img src="img/cluster_images/DBSCAN-vs-kmeans-vs-hierarchical_26_0.png" alt="flame" style="width: 700px;height: 700px"/>


### Future considerations
I'd love to see how Affinity Propogation holds up on these data sets. Maybe in the future I'll do a 4 way battle ala Mario Kart style!
