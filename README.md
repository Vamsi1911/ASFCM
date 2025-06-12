## An overview of the project is provided below.

### About The Project

This project introduces **Adaptive Shadowed Fuzzy C-Means (ASFCM)**, an advanced clustering algorithm designed to improve upon traditional Fuzzy C-Means (FCM) and Shadowed Fuzzy C-Means (SFCM). The core of ASFCM is its ability to dynamically adjust the fuzzifier value, 'm', to strike a balance between cluster compactness and resilience to outliers. By integrating concepts from shadowed sets and fuzzy entropy, ASFCM offers a more robust and accurate approach to clustering, particularly for datasets containing noise and ambiguity.

This research was conducted at Hanyang University under the guidance of Professor Frank. For a more detailed look into the research, you can visit our Notion page: [Research on ASFCM](https://ink-pink-60d.notion.site/Research-on-ASFCM-2108a82df0fb8026af0dfc0fd29feac9?source=copy_link)

-----


### Methodology

The ASFCM algorithm enhances clustering through a multi-faceted approach:

  * **Shadowed C-Means (SCM):** Builds upon Fuzzy C-Means by incorporating shadowed sets, which helps in managing uncertainty by classifying data points into core, exclusion, and shadow (uncertainty) regions. This reduces the influence of outliers on the cluster centroids.
  * **Fuzzy Entropy for Thresholding:** Instead of traditional methods, ASFCM uses fuzzy entropy minimization to determine the optimal thresholds that define the shadow, elevated, and reduced areas of a fuzzy set. This leads to a more precise representation of cluster boundaries. We specifically use Liang et al.'s definition of fuzzy entropy due to its minimal entropy loss.
  * **Adaptive Fuzzifier (m):** The fuzzifier 'm' controls the degree of fuzziness in the clustering. ASFCM introduces an adaptive mechanism to adjust 'm' based on clustering quality metrics like the Davies-Bouldin Index (DBI) and Xie-Beni Index (XBI).The adjustment is performed using a gradient descent approach, ensuring an optimal balance is maintained.
  ***Outlier Detection:** Entropy is a key measure of uncertainty, and outliers typically exhibit the highest entropy as they don't strongly belong to any single cluster. ASFCM identifies potential outliers by flagging points with the highest entropy values (e.g., top 2.5% of data corresponding to k=1.96 in a normal distribution). The algorithm monitors the average entropy of these outliers; a significant drop indicates they are being pulled into a specific cluster, at which point the adaptation of 'm' is halted to prevent distortion.

-----



### Key Features

  * **Dynamic Fuzzifier Adjustment:** Automatically finds an optimal 'm' value for better cluster performance.
  * **Robust Outlier Handling:** Utilizes shadowed sets and entropy to minimize the impact of noisy data.
  * **Improved Cluster Accuracy:** Achieves more compact and well-separated clusters compared to other methods.
  * **Efficient Centroid Calculation:** Integrates rough and shadowed set theory for more efficient computation.

-----



### Results

Our experiments demonstrate that ASFCM outperforms several other clustering algorithms, including HCM, FCM, RCM, RFCM, and SCM.The performance was evaluated using standard cluster validity indices such as the Davies-Bouldin Index (DBI), Xie-Beni Index (XBI), and the Silhouette Index (SI) on datasets like Iris and Vowel.

For the **Iris dataset** with 3 clusters, ASCM achieved the best scores with a DBI of **0.2760** and an XBI of **0.0169**. Similarly, with 6 clusters, ASCM showed superior performance with a DBI of **0.0644** and an XBI of **0.1247**.

A key finding is the importance of initialization. The best results are often achieved by initializing the cluster centers using standard FCM (with m=2). The algorithm then proceeds to find an optimal 'm' value. For instance, in one of our test cases, an optimal 'm' of approximately 6 was identified, which allowed for the accurate determination of at least one cluster center.

-----



### Future Work and Challenges

One of the challenges observed is that while one cluster center is accurately identified, others may oscillate between different convergence points, especially in datasets with clusters of similar density.

Our ongoing work focuses on refining the methodology to address this:

  * **Iterative Refinement:** One promising approach is to first run ASFCM to identify the "true" core points of the most stable cluster. These points can then be "fixed" by setting their membership values to 1 for that cluster and 0 for all others in subsequent iterations. The algorithm is then re-run on the remaining data points to resolve the positions of the other cluster centers.
  * **Bounded Approach:** For clusters with similar densities where the range of membership values might not be a reliable separator, a more bounded approach for adjusting 'm' is being explored. This involves iteratively reducing 'm' until an optimal value is reached based on metrics like the average membership value of a cluster.
