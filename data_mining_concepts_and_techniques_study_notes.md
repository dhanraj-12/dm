# Data Mining: Concepts and Techniques (3rd Edition)

**Authors:** Jiawei Han, Micheline Kamber, Jian Pei  
**Publisher:** Morgan Kaufmann Publishers (an imprint of Elsevier), 2012  
**ISBN:** 978-0-12-381479-1  

---

## Text Conventions & Companion Resources

* **Typographical Conventions:**
  * *Italic* font emphasizes defined terms.
  * **Bold** font highlights or summarizes main ideas.
  * `Monospace` / Sans serif font is used for reserved words.
  * **Bold italic** font ($\boldsymbol{X}, \boldsymbol{V}$) represents multidimensional quantities or vectors.
* **Online Resources:** Companion websites (`www.cs.uiuc.edu/~hanj/bk3` and `www.booksite.mkp.com/datamining3e`) provide chapter slides, companion chapters on advanced data mining, instructors' manuals, syllabi, supplemental reading lists, datasets/software links (e.g., IlliMine), figures, and errata.

---

## Chapter 1: Introduction to Data Mining

### 1.1 Data Growth & Sources
The explosive growth of available data volumes—measured in **petabytes** ($1\text{ petabyte} = 10^{15}\text{ bytes} = 1{,}000\text{ terabytes} = 10^6\text{ gigabytes}$)—stems from computerization and advanced data collection tools across:
* **Business:** Sales transactions (e.g., Wal-Mart handling hundreds of millions of transactions per week), stock trading, product descriptions, promotions, and customer feedback.
* **Science & Engineering:** Remote sensing, process measuring, scientific experiments, and environmental surveillance.
* **Telecommunications & Web:** Global backbone networks, billions of daily web searches, social media, blogs, and digital media.
* **Healthcare:** Medical records, patient monitoring, and medical imaging.

### 1.2 What Is Data Mining? (Knowledge Discovery Process)
Data mining is an essential step in the iterative **Knowledge Discovery in Databases (KDD)** process:
1. **Data cleaning** (removing noise and inconsistent data)
2. **Data integration** (combining multiple data sources)
3. **Data selection** (retrieving data relevant to the analysis task from the database)
4. **Data transformation** (transforming and consolidating data into forms appropriate for mining via summary or aggregation operations)
5. **Data mining** (applying intelligent methods to extract data patterns)
6. **Pattern evaluation** (identifying truly interesting patterns representing knowledge based on *interestingness measures*)
7. **Knowledge presentation** (using visualization and knowledge representation techniques to present mined knowledge to users)

### 1.3 Data Repositories
* **Data Warehouse:** A repository of information collected from multiple sources, stored under a unified schema, usually residing at a single site. Constructed via data cleaning, integration, transformation, loading, and periodic refreshing.
* **Transactional Database:** Stores transactions with one record per transaction (e.g., an *AllElectronics* `sales` table with `list of item IDs`). Because most relational databases do not support nested relations, transactional data are typically stored in flat files or unfolded into standard relational tables.

### 1.4 Classification Models & Web Search
* **Classification Model Representations:**
  * **IF-THEN Rules:** e.g., `IF age(X, "youth") AND income(X, "high") THEN class(X, "A")`.
  * **Decision Trees:** Flowchart-like tree structures splitting on attributes (`age?`, `income?`) down to class leaf nodes.
  * **Neural Networks:** Collections of neuron-like processing units with weighted connections.
  * Other methods include naïve Bayesian classification, support vector machines (SVMs), and $k$-nearest-neighbor classification.
* **Web Search Engines vs. Web Directories:** Web search engines return lists of *hits* (web pages, images, files) algorithmically (or via a hybrid approach), whereas web directories are maintained by human editors.

---

## Chapter 2: Data Visualization

### Hierarchical Visualization: "Worlds-within-Worlds" ($n$-Vision)
To visualize a 6-D dataset with dimensions $F, X_1, \dots, X_5$:
1. Fix dimensions $X_3, X_4, X_5$ to selected values $c_3, c_4, c_5$.
2. Visualize $F, X_1, X_2$ in a 3-D plot called an **inner world**.
3. Place the origin of the inner world at point $(c_3, c_4, c_5)$ inside an **outer world** (a 3-D plot of $X_3, X_4, X_5$).
4. Users can interactively move the origin of the inner world or change which dimensions are assigned to each level.

---

## Chapter 3: Data Preprocessing

### 3.1 Data Cleaning & Integration Tools
* **Data Migration Tools:** Allow simple transformations (e.g., replacing the string `"gender"` with `"sex"`).
* **ETL (Extraction/Transformation/Loading) Tools:** Allow users to specify transformations through a GUI, often supplemented by custom scripts for complex cleaning tasks.

### 3.2 Data Reduction Strategies
Data reduction produces a smaller representation of the dataset that yields the same (or nearly the same) analytical results.

1. **Dimensionality Reduction:** Reducing the number of random variables or attributes.
   * **Discrete Wavelet Transform (DWT):** Projects data onto a smaller space. Closely related to the Discrete Fourier Transform (DFT), but DWT generally achieves better lossy compression and preserves local detail because wavelets are localized in space.
   * **Principal Components Analysis (PCA):** Projects original data onto a smaller orthogonal space (often via Singular Value Decomposition).
   * **Attribute Subset Selection:** Detects and removes irrelevant, weakly relevant, or redundant attributes.
   * **Attribute Construction:** Derives a smaller set of more useful attributes from the original set.
2. **Numerosity Reduction:** Replacing original data volume with smaller representations.
   * **Parametric Methods:** Store only model parameters (e.g., regression, log-linear models) plus optional outliers.
   * **Nonparametric Methods:** Histograms, clustering, sampling, and data cube aggregation (e.g., aggregating quarterly sales into annual sales).
3. **Data Compression:**
   * **Lossless:** Original data can be reconstructed without any information loss.
   * **Lossy:** Only an approximation of the original data can be reconstructed.

### 3.3 Data Transformation & Discretization
* **Normalization / Standardization:** Scales numeric attributes to a smaller common range such as $[-1, 1]$ or $[0.0, 1.0]$ to prevent attributes with larger measurement scales (e.g., *annual salary* vs. *age*) from dominating distance-based algorithms (neural networks, nearest-neighbor classifiers, clustering).
* **Discretization & Concept Hierarchy Generation:** Replaces raw numeric or nominal values with intervals or higher-level conceptual labels (e.g., replacing raw `age` with `youth`, `adult`, `senior`). Techniques include binning, histogram analysis, cluster analysis, decision tree analysis, and correlation analysis.

---

## Chapter 4: Data Warehousing and OLAP

### 4.1 Multidimensional Data Model & Data Cubes
Data cubes are $n$-dimensional metaphors for multidimensional data storage (not limited to 3-D).

#### Table 4.2: 2-D View of *AllElectronics* Sales (`location = "Vancouver"`, in thousands of dollars)
| `time` (quarter) | Home Entertainment | Computer | Phone | Security |
| :--- | :---: | :---: | :---: | :---: |
| **Q1** | 605 | 825 | 14 | 400 |
| **Q2** | 680 | 952 | 31 | 512 |
| **Q3** | 812 | 1023 | 30 | 501 |
| **Q4** | 927 | 1038 | 38 | 580 |

#### Table 4.3: 3-D View of *AllElectronics* Sales (`time`, `item`, `location`, in thousands of dollars)
| `time` | Chicago (HE / Comp / Ph / Sec) | New York (HE / Comp / Ph / Sec) | Toronto (HE / Comp / Ph / Sec) | Vancouver (HE / Comp / Ph / Sec) |
| :--- | :---: | :---: | :---: | :---: |
| **Q1** | 854 / 882 / 89 / 623 | 1087 / 968 / 38 / 872 | 818 / 746 / 43 / 591 | 605 / 825 / 14 / 400 |
| **Q2** | 943 / 890 / 64 / 698 | 1130 / 1024 / 41 / 925 | 894 / 769 / 52 / 682 | 680 / 952 / 31 / 512 |
| **Q3** | 1032 / 924 / 59 / 789 | 1034 / 1048 / 45 / 1002 | 940 / 795 / 58 / 728 | 812 / 1023 / 30 / 501 |
| **Q4** | 1129 / 992 / 63 / 870 | 1142 / 1091 / 54 / 984 | 978 / 864 / 59 / 784 | 927 / 1038 / 38 / 580 |

* **Cuboid:** A data cube representing a specific subset of dimensions (group-by).
* **Lattice of Cuboids:** All possible cuboids for a set of dimensions (e.g., `time`, `item`, `location`, `supplier`).
  * **Base Cuboid:** Lowest level of summarization (e.g., 4-D cuboid `time, item, location, supplier`).
  * **Apex Cuboid (0-D):** Highest level of summarization, denoted by `all` (total sales across all dimensions).

### 4.2 OLAP Operations & Starnet Query Model
* **Roll-up:** Summarizing data by climbing up a concept hierarchy (e.g., `location`: cities $\rightarrow$ countries) or reducing dimensions (**generalization**).
* **Drill-down:** Navigating to more detailed data by stepping down a concept hierarchy (e.g., `time`: quarters $\rightarrow$ months) or adding dimensions (**specialization**).
* **Starnet Model:** Consists of radial lines emanating from a central point, where each line represents a concept hierarchy for a dimension (`location`, `customer`, `item`, `time`) and each abstraction level is called a **footprint** (e.g., `day` $\rightarrow$ `month` $\rightarrow$ `quarter` $\rightarrow$ `year`).

### 4.3 ROLAP vs. MOLAP Storage
* **ROLAP (Relational OLAP):** Stores data in relational tables using **base fact tables** (lowest abstraction level) and **summary fact tables** (aggregated data).
* **MOLAP (Multidimensional OLAP):** Uses array-based multidimensional storage engines for fast indexing. Often uses a two-level storage representation: dense subcubes stored as arrays and sparse subcubes stored with sparse matrix compression.
* **Attribute-Oriented Induction:** Produces generalized relations that can be presented as cross-tabulations, bar/pie charts, or quantitative characteristic rules.

---

## Chapter 5: Data Cube Technology

### 5.1 Cube Cells & Full Cube Computation
* **Ancestor & Descendant Cells:** For example, 1-D cell $a = (\text{Jan}, *, *, 2800)$ and 2-D cell $b = (\text{Jan}, *, \text{Business}, 150)$ are *ancestors* of 3-D cell $c = (\text{Jan}, \text{Chicago}, \text{Business}, 45)$. Here, $b$ is a *parent* of $c$, and $c$ is a *child* of $b$.
* **Full Cube Computation:** Precomputing all cells of all cuboids is exponential in the number of dimensions: an $n$-dimensional data cube contains $2^n$ cuboids.

### 5.2 Bottom-Up Computation (BUC) for Iceberg Cubes
BUC recursively outputs iceberg cube cells satisfying a minimum support threshold (`min_sup`):

```text
Algorithm: BUC(input, dim)
Output: Recursively output iceberg cube cells satisfying min_sup.

1.  Aggregate(input); // Compute measure (e.g., count) and place in outputRec
2.  if input.count() == 1 then // Optimization
        WriteDescendants(input[0], dim);
        return;
    endif
3.  write outputRec;
4.  for (d = dim; d < numDims; d++) do // Partition each dimension
5.      C = cardinality[d];
6.      Partition(input, d, C, dataCount[d]); // Create C partitions for dimension d
7.      k = 0;
8.      for (i = 0; i < C; i++) do // For each value of dimension d
9.          c = dataCount[d][i];
10.         if c >= min_sup then // Test the iceberg condition
11.             outputRec.dim[d] = input[k].dim[d];
12.             BUC(input[k .. k + c - 1], d + 1); // Aggregate on next dimension
13.         endif
14.         k += c;
15.     endfor
16.     outputRec.dim[d] = all;
17. endfor
```

### 5.3 Query Expansion & Prediction Cubes
* **Intracuboid Query Expansion:** Expands sample size by including nearby cells in the *same* cuboid along dimensions that are uncorrelated or weakly correlated with the measure.
* **Prediction Cubes:** At granularity $\langle l_1, \dots, l_d \rangle$ (e.g., $\langle \text{year}, \text{state} \rangle$), each cell stores the predictiveness of attribute set $\boldsymbol{V}$ evaluated on the subset defined by that cell.
* **Probability-Based Ensemble (PBE):** Builds models only for the finest-grained cells and uses OLAP-style bottom-up aggregation to compute coarser-grained cells. Works efficiently when the scoring function is **distributively** (e.g., kernel density-based classifiers) or **algebraically** (e.g., naïve Bayes) decomposable.

### 5.4 Discovery-Driven Exploration of Data Cubes
Uses precomputed exception indicators to guide users during OLAP navigation:
* **`SelfExp`:** Degree of surprise of the cell's value relative to other cells at the same level (visualized via background color).
* **`InExp`:** Degree of surprise beneath the cell at lower levels of aggregation (visualized via box thickness and color).
* **`PathExp`:** Degree of surprise along each drill-down path.

#### Example: Change in Sales for *IBM Desktop Computer* per Region
| Region | Feb | Mar | Apr | May | Jun | Jul | Aug | Sep | Oct | Nov | Dec |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **North** | $-1\%$ | $-3\%$ | $-1\%$ | $0\%$ | $3\%$ | $4\%$ | $-7\%$ | $1\%$ | $0\%$ | $-3\%$ | $-3\%$ |
| **South** | $-1\%$ | $1\%$ | $-9\%$ | $6\%$ | $-1\%$ | **$-39\%$** | $9\%$ | **$-34\%$** | $4\%$ | $1\%$ | $7\%$ |
| **East** | $-1\%$ | $-2\%$ | $2\%$ | $-3\%$ | $1\%$ | $18\%$ | $-2\%$ | $11\%$ | $-3\%$ | $-2\%$ | $-1\%$ |
| **West** | $4\%$ | $0\%$ | $-1\%$ | $-3\%$ | $5\%$ | $1\%$ | $-18\%$ | $8\%$ | $5\%$ | $-8\%$ | $-1\%$ |

* **Expected Value Model:** For a 3-D cube with dimensions $A, B, C$, the expected value of cell $(i, j, k)$ is a function of statistical coefficients $\gamma, \gamma_i^A, \gamma_j^B, \gamma_k^C, \gamma_{ij}^{AB}, \gamma_{ik}^{AC}, \gamma_{jk}^{BC}$ derived from higher-level group-bys.

---

## Chapters 6 & 7: Frequent Pattern Mining & Advanced Pattern Mining

### 6.1 Market Basket Analysis & Association Rules
Each item is represented as a Boolean variable, and each basket as a Boolean vector. Buying patterns are expressed as **association rules** (e.g., customers who buy computers also tend to buy antivirus software).

### 7.1 Multilevel & Multidimensional Association Rules
* **Concept Hierarchies:** Primitive-level items often have very low support. Generalizing items along a hierarchy (e.g., Level 0 `all` $\rightarrow$ Level 1 `Computer` $\rightarrow$ Level 2 `Laptop` $\rightarrow$ Level 3 `Dell` $\rightarrow$ Level 4 `Dell Studio XPS 16 Notebook`) enables discovering stronger associations.
* **Data Cubes for Multidimensional Mining:** Cells of an $n$-dimensional cuboid (e.g., `age`, `income`, `buys`) store support counts of corresponding $n$-predicate sets to compute support and confidence.

### 7.2 Pattern Compression & Summarization
* **Closed Patterns:** Lossless compression of frequent patterns.
* **Max-Patterns:** Lossy compression of frequent patterns.
* **Pattern Clustering ($\delta$-cluster):** Groups frequent patterns by similarity and support, selecting a representative pattern per cluster (finding the minimum set of representatives is NP-Hard).
* **Redundancy-Aware Top-$k$ Patterns:** Balances both *significance* and *mutual independence* (nonredundancy), unlike:
  * **Traditional Top-$k$:** Relies solely on significance (can produce clustered, redundant patterns).
  * **$k$-Summarized Patterns:** Relies solely on nonredundancy (selects representatives from $k$ clusters).

### 7.3 Pattern Exploration & Quantitative Rules
* **Semantic Annotations:** Automatically generated dictionary-like context descriptions and links to semantically similar patterns to aid interpretation.
* **Quantitative Association Rules:** Example of an exceptional pattern:
  $$\text{sex} = \text{female} \Rightarrow \text{mean wage} = \$7.90/\text{hr} \quad (\text{overall mean wage} = \$9.02/\text{hr})$$
* **Cube Gradient Analysis:** Extracts pairs of similar cells (ancestors, descendants, or 1-D siblings) associated with substantial changes in a measure.

---

## Chapter 8: Classification: Basic Concepts

### 8.1 Overview
Classification learns a mapping function $y = f(\boldsymbol{X})$ that predicts the class label $y$ of a given tuple $\boldsymbol{X}$ (represented as rules, decision trees, or mathematical formulas).

### 8.2 Interactive Decision Tree Construction: PBC
**Perception-Based Classification (PBC)** uses a pixel-oriented **circle segments** visualization to map $d$-dimensional data objects into $d$ circle segments (one per attribute), coloring each pixel by class label.
* **Split Screen:** Displays the *Data Interaction* window (circle segments) and *Knowledge Interaction* window (current decision tree).
* Unlike traditional binary-split algorithms, PBC allows users to interactively specify **multiple split-points** for numeric attributes.

### 8.3 Rule Extraction from Decision Trees
* One **IF-THEN** rule is created for each path from the root to a leaf node.
* Splitting criteria along the path are logically ANDed to form the rule antecedent (`IF`), and the leaf node's class forms the consequent (`THEN`).

### 8.4 Model Evaluation: The `.632` Bootstrap
* Samples a dataset of $d$ tuples **uniformly with replacement** $d$ times to form the training set (bootstrap sample).
* On average, **$63.2\%$** of the original tuples appear in the training sample, and the remaining **$36.8\%$** form the test set.

### 8.5 Key References & Repositories
* **Decision Tree Algorithms:** ID3, C4.5, C5.0 (Quinlan), and CART (Breiman et al.).
* **Benchmark Repositories:** UCI Machine Learning Repository (`www.ics.uci.edu/~mlearn/MLRepository.html`) and KDD Archive (`http://kdd.ics.uci.edu`).

---

## Chapter 9: Classification: Advanced Methods

### 9.1 Bayesian Belief Networks (BBN)
Unlike naïve Bayesian classifiers, BBNs do **not** assume class conditional independence.
* **Conditional Probability Table (CPT):** Each variable $Y$ has a CPT specifying $P(Y \mid \text{Parents}(Y))$. For example:
  $$P(\text{LungCancer} = \text{yes} \mid \text{FamilyHistory} = \text{yes}, \text{Smoker} = \text{yes}) = 0.8$$
* **Queries:** Can return full probability distributions, answer *probability of evidence* queries, and *most probable explanation* queries.
* **Training with Hidden Variables (Gradient Descent):** Let $w_{ijk} \equiv P(Y_i = y_{ij} \mid U_i = u_{ik})$ be the CPT weights. To maximize $P_w(D) = \prod_{d=1}^{|D|} P_w(\boldsymbol{X}_d)$, compute gradients of $\ln P_w(D)$:
  $$\frac{\partial \ln P_w(D)}{\partial w_{ijk}} = \sum_{d=1}^{|D|} \frac{P(Y_i = y_{ij}, U_i = u_{ik} \mid \boldsymbol{X}_d)}{w_{ijk}}$$

### 9.2 Classification by Backpropagation
A **multilayer feed-forward neural network** consists of an **input layer**, one or more **hidden layers**, and an **output layer**. Given enough hidden units and training samples, it can closely approximate any function.

#### Network Topology & Preprocessing
* Normalize continuous input attributes to $[0.0, 1.0]$.
* Encode discrete attributes with one input unit per domain value (one-hot encoding).

#### Backpropagation Algorithm
1. **Forward Propagation:**
   * Input layer: $O_j = I_j$.
   * Hidden/Output layer net input:
     $$I_j = \sum_i w_{ij} O_i + \theta_j$$
   * Activation (logistic / sigmoid squashing function):
     $$O_j = \frac{1}{1 + e^{-I_j}}$$
2. **Error Backpropagation:**
   * Output layer unit $j$ (with target $T_j$):
     $$\text{Err}_j = O_j(1 - O_j)(T_j - O_j)$$
   * Hidden layer unit $j$ (summing over units $k$ in the next higher layer):
     $$\text{Err}_j = O_j(1 - O_j) \sum_k \text{Err}_k w_{jk}$$
3. **Weight and Bias Updates** (with learning rate $l \in (0, 1]$):
   $$\Delta w_{ij} = (l)\,\text{Err}_j\,O_i, \quad w_{ij} = w_{ij} + \Delta w_{ij}$$
   $$\Delta \theta_j = (l)\,\text{Err}_j, \quad \theta_j = \theta_j + \Delta \theta_j$$

#### Example 9.1: Sample Forward Pass Calculations
Given tuple $\boldsymbol{X} = (1, 0, 1)$, class label $1$, and learning rate $l = 0.9$:

| $x_1$ | $x_2$ | $x_3$ | $w_{14}$ | $w_{15}$ | $w_{24}$ | $w_{25}$ | $w_{34}$ | $w_{35}$ | $w_{46}$ | $w_{56}$ | $\theta_4$ | $\theta_5$ | $\theta_6$ |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| $1$ | $0$ | $1$ | $0.2$ | $-0.3$ | $0.4$ | $0.1$ | $-0.5$ | $0.2$ | $-0.3$ | $-0.2$ | $-0.4$ | $0.2$ | $0.1$ |

| Unit $j$ | Net Input $I_j$ | Output $O_j$ |
| :---: | :--- | :--- |
| **4** | $0.2 + 0 - 0.5 - 0.4 = -0.7$ | $1 / (1 + e^{0.7}) = 0.332$ |
| **5** | $-0.3 + 0 + 0.2 + 0.2 = 0.1$ | $1 / (1 + e^{-0.1}) = 0.525$ |
| **6** | $(-0.3)(0.332) - (0.2)(0.525) + 0.1 = -0.105$ | $1 / (1 + e^{0.105}) = 0.474$ |

* **Interpretability (Inside the Black Box):** Neural networks can be interpreted via **network pruning**, **activation value clustering** for hidden nodes, **rule extraction**, and **sensitivity analysis**.

### 9.3 Other Advanced Classification Methods
* **Support Vector Machines (SVM):** Transform training data into a higher dimension to find a separating hyperplane using essential tuples called *support vectors*.
* **Classification Using Frequent Patterns:** Uses frequent attribute-value combinations (which often achieve higher information gain than single features).
* **$k$-Nearest-Neighbor ($k$-NN):** Assigns the most common class (or average real value for numeric prediction) among the $k$ closest training tuples. Attributes are typically normalized using **min-max normalization**:
  $$v' = \frac{v - \min_A}{\max_A - \min_A}$$
* **Pool-Based Active Learning:** Iteratively trains a model on labeled set $L$, selects the most informative queries from unlabeled pool $U$, and requests labels from an *oracle* (e.g., human annotator).
* **Transfer Learning:** Extracts knowledge from one or more *source tasks* (e.g., camera sentiment reviews) and applies it to a *target task* (e.g., TV reviews) even when data distributions differ.
  * **Instance-Based Transfer Learning (`TrAdaBoost`):** Extends AdaBoost by reweighting source-domain data to filter out instances that differ greatly from the target domain, requiring fewer labeled target tuples.

---

## Chapters 10 & 11: Cluster Analysis

### 10.1 Hierarchical Clustering & BIRCH
Hierarchical methods organize objects into a tree of clusters. **BIRCH** minimizes I/O using a multiphase approach:
* **Phase 1:** Scans the database to build an in-memory **CF-tree** (Clustering Feature tree), a multilevel compression preserving clustering structure.
* **Phase 2:** Applies a clustering algorithm to the leaf nodes of the CF-tree to remove sparse outliers and group dense clusters.

### 10.2 Grid-Based Query Answering
Computes statistical parameters and confidence intervals top-down across hierarchical grid layers, pruning irrelevant cells at each level before retrieving data in the remaining relevant bottom-layer cells.

### 11.1 Probabilistic Model-Based Clustering & Biclustering
* **Probabilistic Models:** Infer latent probability density functions (e.g., $f_1, f_2$) from observed attributes when categories overlap or are not explicitly labeled.
* **Biclustering:** Originally developed for **gene expression data**, simultaneously clustering genes (genotypes) and conditions (phenotypes).

### 11.2 Spectral Clustering (Ng-Jordan-Weiss Algorithm)
1. Construct an affinity matrix $W$.
2. Define diagonal matrix $D$ where:
   $$D_{ii} = \sum_{j=1}^{n} W_{ij}$$
   and compute the normalized matrix:
   $$A = D^{-1/2} W D^{-1/2}$$
3. Find the $k$ leading **eigenvectors** of $A$ satisfying $A\boldsymbol{v} = \lambda\boldsymbol{v}$ (where $\lambda$ is the eigenvalue).
4. Cluster the data in the new $k$-dimensional space and project the cluster assignments back to the original data.

---

## Chapter 12: Outlier Detection

### Distance-Based Outlier Detection: Nested Loop vs. CELL Method
The nested loop method is costly because it checks objects one-by-one against the entire dataset. The **CELL method** organizes objects into a grid and applies two pruning rules for $DB(r, \pi)$-outliers (where $a$ is the count in cell $C$, $b_1$ is the count in level-1 neighbor cells, and $b_2$ is the count in level-2 neighbor cells):
* **Level-1 Cell Pruning Rule:** If $a + b_1 > \lceil \pi n \rceil$, then **no object** in $C$ is a $DB(r, \pi)$-outlier.
* **Level-2 Cell Pruning Rule:** If $a + b_1 + b_2 < \lceil \pi n \rceil + 1$, then **all objects** in $C$ are $DB(r, \pi)$-outliers.

For very large disk-resident datasets (to avoid random disk accesses), a 3-scan sampling method uses ~1% main memory: (1) sample centroids with replacement and partition $D$, (2) identify candidate outliers, and (3) verify all $DB(r, \pi)$-outliers.

---

## Chapter 13: Trends and Complex Data Types

* **Time-Series Similarity Search & Subsequence Matching:** Finds sequences or subsequences differing only slightly from a query sequence. Typically relies on dimensionality reduction via **DFT**, **DWT**, or **SVD/PCA**, retaining the strongest transformed coefficients as features.
* **Social & Information Networks:** Organizing networks by similarity and clusters allows **OLAP on networks** (drilling down or dicing across abstraction levels) and tracking network evolution.
* **Sequential Pattern Mining in E-Commerce:** Uncovers time-ordered purchase behaviors (e.g., customers buying a digital camera are likely to buy a printer, memory card, or photo-editing software within 3 months) to power targeted recommendations and coupons.