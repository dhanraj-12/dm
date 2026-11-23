# Cluster Analysis: Potential Exam Questions & Exam-Ready Answers

---

## Section 1: Cluster Analysis – Basic Concepts

### Q1. What is cluster analysis? Differentiate between supervised and unsupervised learning, and state what makes a clustering "good".

* **Definition of a Cluster:** A cluster is a collection of data objects that are similar (or related) to one another within the same group and dissimilar (or unrelated) to objects in other groups.
* **Definition of Cluster Analysis:** Cluster analysis (also known as clustering or data segmentation) is the process of finding similarities between data according to characteristics found in the data and grouping similar data objects into clusters.
* **Supervised vs. Unsupervised Learning:**
  * **Unsupervised Learning (Clustering):** There are no predefined classes; the algorithm learns by observations directly from the data.
  * **Supervised Learning (Classification):** Predefined class labels are provided; the algorithm learns by examples.
* **What Makes a Clustering "Good":**
  A good clustering method produces high-quality clusters characterized by:
  1. **High intra-class similarity:** Objects within the same cluster are cohesive (very similar).
  2. **Low inter-class similarity:** Objects in different clusters are distinctive (very dissimilar).
* **Factors Affecting Clustering Quality:**
  1. The similarity measure used by the method.
  2. Its implementation.
  3. Its ability to discover some or all of the hidden patterns.

---

### Q2. List the requirements and challenges of clustering in data mining.

Key requirements and challenges of cluster analysis include:

1. **Scalability:** Ability to cluster all the data in large databases rather than working only on small samples.
2. **Ability to deal with different types of attributes:** Must handle numerical, binary, categorical, ordinal, linked, and mixed attribute types.
3. **Discovery of clusters with arbitrary shape:** Many algorithms tend to find only spherical clusters; real-world data often contains arbitrary shapes.
4. **Ability to deal with noisy data and outliers:** Must be robust against missing, unknown, or erroneous data.
5. **Incremental clustering and insensitivity to input order:** Results should not depend on the order in which data records are fed, and new data should be incorporable incrementally.
6. **High dimensionality:** Handling datasets with a large number of attributes/dimensions (curse of dimensionality).
7. **Constraint-based clustering:** Ability to incorporate user-specified constraints and domain knowledge to determine input parameters.
8. **Interpretability and usability:** Clustering results must be easy to interpret, comprehend, and apply to practical problems.

---

### Q3. Briefly explain the major clustering approaches with examples.

1. **Partitioning Approach:** Constructs various partitions of the data and evaluates them using an optimization criterion (e.g., minimizing the sum of squared errors). *Typical methods:* $k$-means, $k$-medoids (PAM), CLARANS.
2. **Hierarchical Approach:** Creates a hierarchical decomposition (tree of clusters) of the set of data objects using either a bottom-up (agglomerative) or top-down (divisive) criterion. *Typical methods:* AGNES, DIANA, BIRCH, CHAMELEON.
3. **Density-Based Approach:** Groups points based on connectivity and local density functions, allowing discovery of arbitrary-shaped clusters and handling of noise. *Typical methods:* DBSCAN, OPTICS, DENCLUE.
4. **Grid-Based Approach:** Quantizes the object space into a finite number of cells forming a multi-level granularity grid structure; operations are performed on the grid. *Typical methods:* STING, WaveCluster, CLIQUE.
5. **Model-Based Approach:** Hypothesizes a mathematical/statistical model for each cluster and tries to find the best fit of the data to the model. *Typical methods:* EM, SOM, COBWEB.
6. **Frequent Pattern-Based Approach:** Clusters high-dimensional data based on the analysis of frequent patterns. *Typical method:* p-Cluster.
7. **User-Guided or Constraint-Based Approach:** Performs clustering while considering user-specified or application-specific constraints. *Typical methods:* COD (obstacles), constrained clustering.
8. **Link-Based Clustering:** Clusters objects that are linked together in various ways using massive link structures. *Typical methods:* SimRank, LinkClus.

---

### Q4. Explain the applications of clustering (both stand-alone and as a preprocessing tool).

Clustering is applied in two major ways:

* **Stand-Alone Applications (Data Understanding):**
  * **Biology:** Taxonomy of living organisms (kingdom, phylum, class, order, family, genus, and species).
  * **Information Retrieval:** Document clustering for organizing search results.
  * **Land Use:** Identification of areas of similar land use in earth observation databases.
  * **Marketing:** Discovering distinct customer segments to design targeted marketing campaigns.
  * **City Planning:** Identifying groups of houses by house type, value, and geographical location.
  * **Earthquake Studies:** Clustering observed earthquake epicenters along continental fault lines.
  * **Climate & Economic Science:** Finding atmospheric/ocean patterns and conducting market research.
* **Clustering as a Preprocessing Tool (Utility):**
  * **Summarization:** Preprocessing step for regression, PCA, classification, and association analysis.
  * **Compression:** Image processing via vector quantization.
  * **Finding K-Nearest Neighbors:** Localizing search to one or a small number of clusters to speed up queries.
  * **Outlier Detection:** Identifying outliers as points that lie far away from any cluster.

---

## Section 2: Partitioning Methods

### Q5. Explain the K-Means clustering algorithm with its steps, time complexity, strengths, and weaknesses.

* **Concept & Objective Function:** $K$-Means partitions a database $D$ of $n$ objects into $k$ clusters such that each cluster is represented by its centroid (mean point) and the sum of squared errors ($E$) is minimized:
  $$E = \sum_{i=1}^{k} \sum_{p \in C_i} (p - c_i)^2$$
  where $p$ is a data object in cluster $C_i$ and $c_i$ is the centroid of $C_i$.
* **Algorithm Steps:**
  1. Arbitrarily partition the objects into $k$ nonempty subsets.
  2. Compute seed points as the centroids (mean points) of the clusters in the current partitioning.
  3. Assign each object to the cluster with the nearest seed point (centroid).
  4. Repeat Steps 2 and 3 until the cluster assignments do not change.
* **Strength:** Highly efficient with time complexity $O(tkn)$, where $n$ is the number of objects, $k$ is the number of clusters, and $t$ is the number of iterations (normally $k, t \ll n$). Much faster than PAM $O(k(n-k)^2)$ and CLARA $O(ks^2 + k(n-k))$.
  *(Note: Often terminates at a local optimum rather than the global optimum.)*
* **Weaknesses:**
  1. Applicable only to objects in a continuous $n$-dimensional space (cannot directly handle categorical data; requires variants like $k$-modes for categorical data or $k$-prototype for mixed data).
  2. Requires specifying $k$ (the number of clusters) in advance.
  3. Highly sensitive to noisy data and outliers.
  4. Not suitable for discovering clusters with non-convex (arbitrary) shapes.

---

### Q6. Why is K-Means sensitive to outliers? How does K-Medoids (PAM) solve this problem?

* **Why K-Means is Sensitive to Outliers:** $K$-Means uses the mean value of all objects in a cluster as its reference point (centroid). An object with an extremely large or extreme value substantially pulls the mean away from the true center, distorting the data distribution and cluster boundaries.
* **How K-Medoids (PAM) Solves This:** Instead of using a calculated mean, $K$-Medoids uses a **medoid**—an actual, most centrally located object in the cluster—as the reference point. Because a medoid is an actual data point rather than an average, it is far less affected by extreme outlier values.
* **Steps of PAM (Partitioning Around Medoids):**
  1. Arbitrarily select $k$ objects as initial medoids.
  2. Assign each remaining non-medoid object to the cluster of the nearest medoid and compute the initial Total Cost (sum of distances).
  3. Select a non-medoid object $O_{\text{random}}$ and compute the total cost of swapping an existing medoid with $O_{\text{random}}$.
  4. Calculate the swapping cost $TC = \text{New Total Cost} - \text{Old Total Cost}$. If $TC < 0$ (quality improves), replace the medoid with $O_{\text{random}}$; otherwise, undo the swap.
  5. Repeat the reassignment and swapping steps until no change occurs.

---

### Q7. Compare K-Means and K-Medoids (PAM), and mention how PAM's scalability issue is addressed.

| Feature | K-Means | K-Medoids (PAM) |
| :--- | :--- | :--- |
| **Cluster Representative** | Centroid (mean point of cluster) | Medoid (actual, most centrally located object) |
| **Sensitivity to Outliers** | High (mean is easily distorted by extreme values) | Low (robust against noise and outliers) |
| **Data Types Supported** | Continuous numerical data only | Wide range of data types |
| **Time Complexity** | $O(tkn)$ — scales well for large datasets | $O(k(n-k)^2)$ — does not scale well for large datasets |

**Addressing PAM's Scalability Issue:**
Because PAM has high computational complexity on large datasets, two sampling-based improvements are used:

1. **CLARA (Clustering Large Applications):** Draws multiple samples of the dataset, applies PAM to each sample, and outputs the best clustering. Complexity: $O(ks^2 + k(n-k))$.
2. **CLARANS (Clustering Large Applications based on Randomized Search):** Uses randomized re-sampling of neighbors dynamically, modeling the search as a graph where each node is a set of $k$ medoids. More efficient and scalable than both PAM and CLARA.

---

## Section 3: Hierarchical Methods

### Q8. Differentiate between Agglomerative (AGNES) and Divisive (DIANA) hierarchical clustering. What is a dendrogram, and what are the limitations of standard hierarchical clustering?

| Aspect | AGNES (Agglomerative) | DIANA (Divisive) |
| :--- | :--- | :--- |
| **Approach** | Bottom-up | Top-down (inverse of AGNES) |
| **Starting State** | Every data object starts as its own individual cluster | All data objects start together in a single cluster |
| **Process** | Repeatedly merges the two clusters with the least dissimilarity (e.g., using single-link) | Repeatedly splits a cluster into smaller clusters |
| **Ending State** | All nodes eventually belong to a single cluster | Each node eventually forms a cluster on its own |

* **Dendrogram:** A tree diagram that illustrates how data objects are decomposed into several levels of nested partitioning. A specific clustering is obtained by cutting the dendrogram horizontally at a desired level, where each resulting connected component forms a cluster.
* **Limitations of Standard Hierarchical Clustering:**
  1. **Cannot undo previous steps:** Once a merge or split decision is made, it can never be undone or corrected later.
  2. **Poor scalability:** Has a time complexity of at least $O(n^2)$, where $n$ is the total number of objects, making it unsuitable for very large datasets.

---

### Q9. Explain the different ways to measure distance between two clusters in hierarchical clustering.

Given two clusters $K_i$ and $K_j$, the five standard inter-cluster distance measures are:

1. **Single Link (Nearest Neighbor):** The smallest distance between an element in one cluster and an element in the other.
   $$\text{dist}(K_i, K_j) = \min(t_{ip}, t_{jq})$$
2. **Complete Link (Farthest Neighbor):** The largest distance between an element in one cluster and an element in the other.
   $$\text{dist}(K_i, K_j) = \max(t_{ip}, t_{jq})$$
3. **Average Link (UPGMA):** The average distance between every element in one cluster and every element in the other.
   $$\text{dist}(K_i, K_j) = \text{avg}(t_{ip}, t_{jq})$$
4. **Centroid Distance:** The distance between the centroids (mean points) of the two clusters.
   $$\text{dist}(K_i, K_j) = \text{dist}(C_i, C_j)$$
5. **Medoid Distance:** The distance between the medoids (chosen centrally located objects) of the two clusters.
   $$\text{dist}(K_i, K_j) = \text{dist}(M_i, M_j)$$

---

### Q10. Explain the BIRCH algorithm. What is a Clustering Feature (CF) and a CF-Tree?

* **BIRCH (Balanced Iterative Reducing and Clustering Using Hierarchies):** A scalable hierarchical clustering method designed for large numerical datasets that incrementally constructs a CF-Tree for multiphase clustering.
* **Clustering Feature (CF):** A compact triple summarizing the statistics (0th, 1st, and 2nd moments) of a sub-cluster:
  $$CF = (N, LS, SS)$$
  where:
  * $N =$ Number of data points in the sub-cluster
  * $LS =$ Linear sum of the $N$ points: $\sum_{i=1}^{N} X_i$
  * $SS =$ Square sum of the $N$ points: $\sum_{i=1}^{N} X_i^2$
* **CF-Tree:** A height-balanced tree that stores clustering features for hierarchical clustering. Non-leaf nodes store the sums of the CFs of their children. It is governed by two parameters:
  1. **Branching Factor ($B$):** Maximum number of children per non-leaf node.
  2. **Threshold ($T$):** Maximum diameter of sub-clusters stored at the leaf nodes.
* **Two Phases of BIRCH:**
  * **Phase 1:** Scan the database to build an initial in-memory CF-Tree (a multi-level compression of the data that preserves inherent clustering structure). For each point, find the closest leaf entry, add the point and update CF, and split the leaf (and possibly parents) if diameter exceeds `max_diameter`.
  * **Phase 2:** Apply an arbitrary clustering algorithm to cluster the leaf nodes of the CF-Tree.
* **Strength:** Scales linearly with time complexity $O(n)$; finds good clustering in a single scan.
* **Weaknesses:**
  1. Handles only numeric data.
  2. Sensitive to the insertion order of data records.
  3. Tends to produce spherical clusters due to fixed leaf sizes and radius/diameter measures.

---

### Q11. How does CHAMELEON work? Why is it better at finding complex cluster shapes?

* **Overview:** CHAMELEON is a graph-based, two-phase hierarchical clustering algorithm that uses dynamic modeling to measure cluster similarity.
* **Two-Phase Framework:**
  1. **Phase 1 (Graph Partitioning):** Constructs a $K$-Nearest Neighbor ($K$-NN) sparse graph (where points $p$ and $q$ are connected if $q$ is among the top $k$ closest neighbors of $p$) and uses a graph-partitioning algorithm to split the objects into a large number of relatively small sub-clusters.
  2. **Phase 2 (Agglomerative Merging):** Repeatedly merges these sub-clusters using an agglomerative hierarchical clustering algorithm to find genuine clusters.
* **Why It Excels at Complex Shapes (Dynamic Modeling):**
  Unlike traditional methods that only look at absolute distance, CHAMELEON merges two clusters $C_1$ and $C_2$ **only** if **both** of the following are high relative to their internal characteristics:
  1. **Relative Interconnectivity:** The connectivity between $C_1$ and $C_2$ relative to the internal connectivity within $C_1$ and $C_2$.
  2. **Relative Closeness (Proximity):** The closeness between $C_1$ and $C_2$ relative to the internal closeness of items within $C_1$ and $C_2$.
  
  This dynamic adaptation allows CHAMELEON to discover natural clusters of arbitrary, complex shapes and varying densities.

---

### Q12. Write a short note on Probabilistic Hierarchical Clustering.

* **Motivation:** Standard algorithmic hierarchical clustering makes it difficult to choose a good distance measure, struggles with missing attribute values, and lacks a clear global optimization goal.
* **Concept:** Probabilistic hierarchical clustering uses generative probabilistic models (assuming data is generated by common distributions such as Gaussian or Bernoulli distributions) to measure distances between clusters. It is easy to understand, matches the efficiency of agglomerative clustering, and can handle partially observed/missing data.
* **Key Formulas:**
  * **Quality of $m$ clusters $\{C_1, \dots, C_m\}$:**
    $$Q(\{C_1, \dots, C_m\}) = \prod_{i=1}^{m} P(C_i)$$
    where $P()$ is the maximum likelihood.
  * **Distance between clusters $C_1$ and $C_2$:**
    $$\text{dist}(C_1, C_2) = -\log \left( \frac{P(C_1 \cup C_2)}{P(C_1) P(C_2)} \right)$$
* **Algorithm:** Start with each object in its own cluster. Iteratively find the pair of clusters $(C_i, C_j)$ that maximizes $\log \left( \frac{P(C_i \cup C_j)}{P(C_i) P(C_j)} \right)$. If this value is $> 0$, merge $C_i$ and $C_j$.

---

## Section 4: Density-Based Clustering – DBSCAN

### Q13. Explain the DBSCAN algorithm. Define core point, border point, noise, directly density-reachable, density-reachable, and density-connected.

* **Full Form & Concept:** DBSCAN (*Density-Based Spatial Clustering of Applications with Noise*) defines a cluster as a maximal set of density-connected points. It uses two parameters:
  * **$Eps$ ($\varepsilon$):** Maximum radius of the neighborhood.
  * **$MinPts$:** Minimum number of points required in an $Eps$-neighborhood.
* **Key Definitions:**
  1. **$Eps$-Neighborhood:** $N_{Eps}(p) = \{ q \in D \mid \text{dist}(p, q) \le Eps \}$.
  2. **Core Point:** A point $q$ whose $Eps$-neighborhood contains at least $MinPts$ points, i.e., $|N_{Eps}(q)| \ge MinPts$.
  3. **Border Point:** A point with fewer than $MinPts$ in its $Eps$-neighborhood, but which lies inside the neighborhood of a core point.
  4. **Noise (Outlier):** A point that is neither a core point nor a border point.
  5. **Directly Density-Reachable:** Point $p$ is directly density-reachable from point $q$ (w.r.t. $Eps, MinPts$) if $p \in N_{Eps}(q)$ **and** $q$ is a core point ($|N_{Eps}(q)| \ge MinPts$).
  6. **Density-Reachable:** Point $p$ is density-reachable from point $q$ if there is a chain of points $p_1, p_2, \dots, p_n$ (where $p_1 = q$ and $p_n = p$) such that each $p_{i+1}$ is directly density-reachable from $p_i$.
  7. **Density-Connected:** Point $p$ is density-connected to point $q$ if there exists a point $o$ such that both $p$ and $q$ are density-reachable from $o$.
* **DBSCAN Algorithm Steps:**
  1. Arbitrarily select an unvisited point $p$.
  2. Retrieve all points density-reachable from $p$ w.r.t. $Eps$ and $MinPts$.
  3. If $p$ is a core point, a cluster is formed.
  4. If $p$ is a border point, no points are density-reachable from $p$, so DBSCAN visits the next point in the database.
  5. Continue the process until all points have been processed.

---

### Q14. What are the advantages and limitations of DBSCAN compared to K-Means?

* **Advantages of DBSCAN over K-Means:**
  1. Discovers clusters of arbitrary shapes ($K$-Means only finds convex/spherical clusters).
  2. Effectively handles noise and outliers ($K$-Means is heavily distorted by outliers).
  3. Does not require specifying the number of clusters $k$ in advance.
  4. Requires only a single scan of the database.
* **Limitation of DBSCAN:** Highly sensitive to its input parameters ($Eps$ and $MinPts$). Even a small change in $Eps$ can drastically alter the clustering results, merging distinct clusters or fragmenting a single cluster.

---

## Section 5: Grid-Based Clustering – STING

### Q15. Explain the STING grid-based clustering method with its architecture, algorithm, advantages, and disadvantages.

* **Full Form & Architecture:** STING (*STatistical INformation Grid*, Wang et al., 1997) divides a spatial area into rectangular cells organized in a hierarchical, multi-resolution grid structure. Each cell at a higher level is partitioned into several smaller cells at the next lower level.
* **Precomputed Cell Statistics:** Statistical information for each cell is precomputed and stored beforehand to answer queries. Higher-level cell parameters are easily calculated from lower-level child cells:
  * **Numerical parameters:** `count`, `mean`, `s` (standard deviation), `min`, `max`.
  * **Distribution type:** `normal`, `uniform`, etc.
* **Top-Down Query Processing Algorithm:**
  1. Start from a pre-selected layer (typically near the top with a small number of cells).
  2. For each cell in the current level, compute the confidence interval (or estimated probability) of relevance to the query.
  3. Remove irrelevant cells from further consideration.
  4. Proceed to the next lower level and examine only the child cells of the remaining relevant cells.
  5. Repeat this process until the bottom layer is reached.
* **Advantages:**
  1. Query-independent (statistical summaries are precomputed).
  2. Easy to parallelize.
  3. Supports incremental updates.
  4. Very fast time complexity: $O(K)$, where $K$ is the number of grid cells at the lowest level.
* **Disadvantage:** All cluster boundaries are strictly horizontal or vertical; no diagonal boundaries can be detected.

---

### Q16. Why is STING fast, and what is its main limitation regarding cluster shapes?

* **Why STING is Fast:** Statistical information (`count`, `mean`, `s`, `min`, `max`, distribution) is precomputed and stored for each grid cell beforehand, making it query-independent. Processing time is $O(K)$, where $K$ is the number of grid cells at the lowest level—which is typically much smaller than the total number of raw data objects.
* **Main Limitation:** Because STING partitions space strictly into rectangular cells, all resulting cluster boundaries are either horizontal or vertical; it cannot detect diagonal boundaries.

---

## Section 6: Evaluation of Clustering & Silhouette Coefficient

### Q17. How do you assess clustering tendency? Explain the Hopkins Statistic.

* **Clustering Tendency:** Before applying a clustering algorithm, we assess whether a non-random structure actually exists in the dataset by measuring the probability that the data was generated by a uniform random distribution.
* **Hopkins Statistic ($H$):** A statistical test for spatial randomness on a dataset $D$:
  1. Sample $n$ points $(p_1, \dots, p_n)$ uniformly from the data space. For each $p_i$, find its nearest neighbor in $D$:
     $$x_i = \min \{ \text{dist}(p_i, v) \mid v \in D \}$$
  2. Sample $n$ points $(q_1, \dots, q_n)$ uniformly from $D$. For each $q_i$, find its nearest neighbor in $D - \{q_i\}$:
     $$y_i = \min \{ \text{dist}(q_i, v) \mid v \in D,\ v \ne q_i \}$$
  3. Calculate the Hopkins Statistic:
     $$H = \frac{\sum_{i=1}^{n} y_i}{\sum_{i=1}^{n} x_i + \sum_{i=1}^{n} y_i}$$
* **Interpretation:**
  * If $D$ is uniformly distributed (random, no clusters), $\sum x_i$ and $\sum y_i$ are close to each other, so $H \approx 0.5$.
  * If $D$ is highly skewed (strong clustering tendency), $H$ is close to $0$.

---

### Q18. Explain the methods used to determine the optimal number of clusters.

Three main methods are used to determine the number of clusters $k$:

1. **Empirical Method:** A simple rule of thumb for a dataset of $n$ points:
   $$\text{Number of clusters } (k) \approx \sqrt{\frac{n}{2}}$$
2. **Elbow Method:** Plots the sum of within-cluster variance against the number of clusters $k$. The optimal $k$ is chosen at the "turning point" (elbow) of the curve, where adding more clusters yields diminishing reductions in variance.
3. **Cross-Validation Method:**
   * Divide the dataset into $m$ equal parts.
   * Use $m - 1$ parts to build a clustering model.
   * Use the remaining $1$ part as a test set to evaluate quality (e.g., compute the sum of squared distances from each test point to its closest centroid).
   * Repeat $m$ times for different values of $k > 0$ and compare overall quality to select the $k$ that fits the data best.

---

### Q19. Differentiate between Extrinsic and Intrinsic methods of measuring clustering quality. Explain the 4 essential criteria for extrinsic measures.

| Aspect | Extrinsic Methods | Intrinsic Methods |
| :--- | :--- | :--- |
| **Type** | Supervised | Unsupervised |
| **Ground Truth** | Available (true class labels exist) | Unavailable (no ground truth labels) |
| **Basis of Evaluation** | Compares clustering output $C$ directly against ground truth $C_g$ | Evaluates how compact each cluster is and how well-separated clusters are |
| **Examples** | BCubed precision and recall | Silhouette coefficient |

**4 Essential Criteria for an Extrinsic Quality Measure $Q(C, C_g)$:**

1. **Cluster Homogeneity:** The purer each cluster is (containing objects from a single ground-truth category), the better.
2. **Cluster Completeness:** Objects belonging to the same category in the ground truth should be assigned to the same cluster.
3. **Rag Bag:** Putting a heterogeneous object into a pure cluster should be penalized more heavily than putting it into a "rag bag" (miscellaneous/other) category.
4. **Small Cluster Preservation:** Splitting a small ground-truth category into pieces is more harmful than splitting a large category into pieces.

---

### Q20. Explain the Silhouette Coefficient with its formula and interpret its values.

* **Overview:** The Silhouette Coefficient is an intrinsic (unsupervised) metric used to evaluate clustering quality when ground truth is unavailable. It measures both cluster compactness and cluster separation.
* **Components for a data object $o$ in cluster $C_i$:**
  1. **$a(o)$ — Compactness (Cohesion):** The average distance between $o$ and all other objects in its own cluster $C_i$:
     $$a(o) = \frac{\sum_{o' \in C_i,\, o' \ne o} \text{dist}(o, o')}{|C_i| - 1}$$
  2. **$b(o)$ — Separation:** The minimum average distance from $o$ to all objects in any other cluster $C_j$ ($j \ne i$):
     $$b(o) = \min_{j \ne i} \left\{ \frac{\sum_{o' \in C_j} \text{dist}(o, o')}{|C_j|} \right\}$$
* **Formula:**
  $$s(o) = \frac{b(o) - a(o)}{\max \{ a(o),\, b(o) \}}$$
* **Value Range & Interpretation ($-1 \le s(o) \le +1$):**
  * **Close to $+1$:** $a(o) \ll b(o)$ — the object is tightly packed within its own cluster and far from neighboring clusters (ideal clustering).
  * **Close to $0$:** $a(o) \approx b(o)$ — the object lies on the boundary between two clusters.
  * **Negative ($< 0$):** $a(o) > b(o)$ — the object is closer to another cluster than to its own (poor/misassigned clustering).
* **Overall Clustering Score:** Computed as the average of $s(o)$ across all objects in the dataset.

---

### Q21. Quick Numerical on Silhouette Coefficient: Given a data point $o$ with average intra-cluster distance $a(o) = 2$ and minimum average inter-cluster distance $b(o) = 5$, compute and interpret its Silhouette Coefficient.

* **Given:** $a(o) = 2$, $b(o) = 5$.
* **Formula:**
  $$s(o) = \frac{b(o) - a(o)}{\max \{ a(o),\, b(o) \}}$$
* **Calculation:**
  $$s(o) = \frac{5 - 2}{\max \{ 2,\, 5 \}} = \frac{3}{5} = 0.6$$
* **Interpretation:** Since $s(o) = 0.6$ is positive and reasonably close to $+1$, the data point $o$ is well-clustered (more compact within its own cluster than close to the nearest neighboring cluster).