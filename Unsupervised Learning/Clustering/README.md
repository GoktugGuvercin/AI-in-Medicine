
## Clustering:

* Clustering is one of unsupervised learning algorithms used in medical imaging domain. It has an extensive usage area ranging from ilness-based 
stratification to the classification of pixels to make segmentation. It is an algorithm applicable in both image level and also pixel level. For example,
categorizing MRI scans into different groups depending on the severity of an illness is in the scope of image-level clustering. However, clustering
algorithms directly work on the samples with pre-defined features; hence, it requires an additional pre-processing step to extract representative feature
vectors of the images. Classification of pixels for tissue segmentation is, on the other hand, is an instance of pixel-level clustering scheme. Intensity,
spatial location, and average intensity of the patch around the pixel are the most commonly-used features to differentiate the pixels from one another for
clustering. Stratification and soft-tissue segmentation of brain MRIs are the most powerful candidates to these two examples.

* Brain MRI Stratification:
  * Normal
  * Mild Cognitive Impairment
  * Severe Cognitive Impairment (Alzheimer)

* MRI Soft Tissue Segmentation:
  * Gray Matter
  * White Matter
  * Cerebro-Spinal Fluid


* The motivation lying behind the usage of clustering algorithm in medical domain is the lack of labels in the dataset. In other words, we have classes in 
the dataset, but we do not know the labels of images. This prevents us from applying supervised learning; that's why, clustering can be an alternative 
approach.

* Some diseases may have multiple states, and if we do not know how many states they have, defining labels for them can be quite challenging. Besides, 
annotating medical dataset can require at least 2 experts in that domain and it is cumbersome process. This increase the tendency to use unsupervised 
learning more. 

* Clustering algorithms generally do not need to know how many classes there are, which makes them more convenient. However, even if we decide to adapt
unsupervised learning on our medical dataset, it is not possible to evaluate and assess the performance of the model without labels.

### 1) KMeans:

* KMeans is one of the most popular clustering algorithms. It tries to separate the samples $X =\\{x_1, \\ x_2, \\ x_3, \\ ..., \\ x_n \\}$ into $K$ number of disjoint groups (clusters) with equal variance, and while doing this it minimizes the cost function called as inertia. Each of these clusters is represented by its centroid $\mu_i$. KMeans clustering can be summarized with the following three steps. 


  * ***Step 1***: Initial cluster centroids are chosen randomly from dataset. How many centroid we will have depends on the number of clusters in the data. 
If we are able to visualize the scatter of dataset in 2D or 3D space, we can figure out how many number of clusters we have in that way. Otherwise, 
elbow-method and application-based rationale can be used. 

  * ***Step 2:*** The pairwise distance between data samples and centroids is computed, and then, data samples are assigned to the closest cluster centroid (Assignment Update)

  * ***Step 3:*** The coordinates of data samples in each cluster are averaged to update the location of corresponding cluster centroid. (Centroid Update)


* The steps 2 and 3 are repeated in a couple of iterations. In that way, the centroids get into their correct position. In this scheme, the step 2 and 3 are repeated in a couple of iterations until the centroids get into their correct position. If there is not so much alteration on the displacement of centroids, the algorithm would be converged and thereby being stopped. This process actually refers to the training stage in supervised learning methods. When new data samples are provided for us, they are just used for inference to find out which of these clusters they belong to. 

* One of the problems commonly observed in the applications of kmeans clustering is that they end up with local minima. In other words, the centroids settle in a position not good enough due to bad initialization. In this case, some data samples that need to be in same cluster would be partitioned into maybe 2 or 3 different clusters. To solve this problem, executing kmeans multiple times with different initializations and choosing the clusters with minimum cost is one of the recommended techniques. However, kmeans++ is more commonly used due to its improved initialization scheme. 

* The another downside of k-means algorithm is its being in favor of equally-sized clusters. In this case, kmeans tries to create a balance between the clusters, which leads some parts of dominant clusters in original data to be assigned to weak clusters.
