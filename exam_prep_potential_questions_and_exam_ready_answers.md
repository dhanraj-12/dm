# Exam Prep: Potential Questions and Exam-Ready Answers

## Section 1: Classification — Basic Concepts

### Q1. Differentiate between Classification, Clustering, and Numeric Prediction. (3–5 marks)

* **Classification (Supervised Learning):** Uses a training set with predefined, known class labels to predict categorical (discrete or nominal) class labels for new data instances.

* **Clustering (Unsupervised Learning):** Class labels are unknown; partitions a dataset into subsets (clusters) whose data points share common characteristics without predefined classes.

* **Numeric Prediction / Regression (Supervised Learning):** Models continuous-valued functions to predict unknown or missing continuous numerical values rather than discrete class labels.

### Q2. Explain the two-step process of classification with an example. (5–7 marks)

Classification is performed in two steps:

1. **Model Construction (Training Phase):** Describes a set of predetermined classes. Each tuple in the training set belongs to a predefined class determined by the class label attribute. A classification algorithm analyzes the training set to build a classifier represented as IF-THEN classification rules, decision trees, or mathematical formulae.

2. **Model Usage (Testing and Prediction Phase):** Used to classify future or unknown objects. First, the model's accuracy is estimated using an independent test set by comparing known labels against predicted labels. Accuracy rate is the percentage of test samples correctly classified. If accuracy is acceptable, the model is used to classify new unseen data.

**Example:** Using a faculty training table `(Name, Rank, Years, Tenured)`, the classifier learns the rule: `IF rank = 'professor' OR years > 6 THEN tenured = 'yes'`. On an unseen tuple `(Jeff, Professor, 4)`, the model predicts `Tenured = 'yes'`.

### Q3. What is overfitting and generalization? Explain the roles of training, validation, and test sets. (4–5 marks)

* **Generalization:** The ability of a classifier to produce reasonable, accurate outputs for new ("never seen before") inputs not encountered during training.

* **Overfitting:** Occurs when a model learns the specific training data (including noise) rather than the underlying function, resulting in high performance on training data but poor accuracy on unseen data. It is avoided using independent subsets and early stopping.

* **Training Set:** A set of labeled examples used for learning/constructing the model.

* **Validation Set:** A set of labeled examples used to tune the architecture/parameters of a classifier, select models, and estimate error.

* **Test Set:** Used exclusively to assess the performance of the final classifier. It must be independent of the training set to provide an unbiased estimate of generalization error.

## Section 2: Decision Tree Induction

### Q4. Write and explain the basic algorithm for Decision Tree Induction along with its stopping conditions. (5–7 marks)

Decision Tree Induction is a greedy, nonparametric, rule-based classification method that constructs a tree in a top-down recursive divide-and-conquer manner:

1. At the start, all training examples are placed at the root node.

2. Attributes are categorical (continuous-valued attributes are discretized in advance).

3. A test attribute is selected using a heuristic or statistical attribute selection measure (such as Information Gain).

4. Examples are partitioned recursively based on the selected attribute's outcomes.

**Stopping Conditions:**

1. All samples for a given node belong to the same class.

2. No remaining attributes are available for further partitioning (majority voting is employed to classify the leaf).

3. There are no samples left.

### Q5. What is overfitting in decision trees? Differentiate between prepruning and postpruning. (4–5 marks)

Overfitting in decision trees occurs when an induced tree creates too many branches that reflect anomalies due to noise or outliers in the training data, leading to poor accuracy on unseen samples. Tree pruning addresses this via two approaches:

* **Prepruning:** Halts tree construction early by refusing to split a node if the split would cause the goodness measure to fall below a threshold. *Limitation:* It is difficult to choose an appropriate threshold.

* **Postpruning:** Removes branches from a "fully grown" tree to produce a sequence of progressively pruned trees, then uses an independent validation dataset to select the "best pruned tree."

### Q6. Why is decision tree induction popular? Briefly explain scalable methods like RainForest and BOAT. (5 marks)

Decision tree induction is popular because it offers relatively faster learning speed than other methods, converts easily into simple human-readable classification rules, can use SQL queries to access databases, and achieves comparable classification accuracy.

**Scalable Methods for Large Databases:**

* **RainForest:** Separates scalability aspects from tree quality criteria by building an AVC-list (`Attribute, Value, Class_label`). An **AVC-set** of attribute $X$ aggregates class label counts for $X$, and an **AVC-group** at node $n$ holds the AVC-sets of all predictor attributes at node $n$.

* **BOAT (Bootstrapped Optimistic Algorithm for Tree Construction):** Uses bootstrapping to create several smaller subsets that fit in memory, builds a tree for each subset, and combines them to construct a new tree $T'$ very close to the full-dataset tree. It is incremental and requires only two scans of the database.

## Section 3: Attribute Selection Measures

### Q7. Explain Information Gain, Gain Ratio, and Gini Index with their mathematical formulas. (6–8 marks)

1. **Information Gain (ID3):** Measures the reduction in uncertainty (entropy) achieved by splitting dataset $D$ on attribute $A$.

   * $\text{Info}(D) = -\sum_{i=1}^{m} p_i \log_2(p_i)$, where $p_i = \frac{\vert{}C_{i,D}\vert{}}{\vert{}D\vert{}}$.

   * $\text{Info}_A(D) = \sum_{j=1}^{v} \frac{\vert{}D_j\vert{}}{\vert{}D\vert{}} \times \text{Info}(D_j)$.

   * $\text{Gain}(A) = \text{Info}(D) - \text{Info}_A(D)$.

   * The attribute with the **highest Information Gain** is chosen.

2. **Gain Ratio (C4.5):** Normalizes Information Gain to overcome its bias toward multivalued attributes.

   * $\text{SplitInfo}_A(D) = -\sum_{j=1}^{v} \frac{\vert{}D_j\vert{}}{\vert{}D\vert{}} \times \log_2\left(\frac{\vert{}D_j\vert{}}{\vert{}D\vert{}}\right)$.

   * $\text{GainRatio}(A) = \frac{\text{Gain}(A)}{\text{SplitInfo}_A(D)}$.

   * The attribute with the **maximum Gain Ratio** is selected.

3. **Gini Index (CART):** Measures impurity of dataset $D$ containing $n$ classes for binary splits into $D_1$ and $D_2$.

   * $\text{gini}(D) = 1 - \sum_{j=1}^{n} p_j^2$.

   * $\text{gini}_A(D) = \frac{\vert{}D_1\vert{}}{\vert{}D\vert{}}\text{gini}(D_1) + \frac{\vert{}D_2\vert{}}{\vert{}D\vert{}}\text{gini}(D_2)$.

   * $\Delta\text{gini}(A) = \text{gini}(D) - \text{gini}_A(D)$.

   * The attribute with the **smallest** $\text{gini}_A(D)$ (or largest reduction in impurity $\Delta\text{gini}$) is chosen.

### Q8. Compare the three attribute selection measures and state their biases/limitations. (4–5 marks)

| Measure | Algorithm | Criterion | Primary Bias / Limitation | 
| ----- | ----- | ----- | ----- | 
| **Information Gain** | ID3 | Maximize $\text{Gain}(A)$ | Strongly biased towards attributes with a large number of distinct values. | 
| **Gain Ratio** | C4.5 | Maximize $\text{GainRatio}(A)$ | Tends to prefer unbalanced splits where one partition is much smaller than others. | 
| **Gini Index** | CART | Minimize $\text{gini}_A(D)$ | Biased toward multivalued attributes; struggles with large class counts; favors equal-sized partitions with purity in both. | 

### Q9. How is Information Gain computed for continuous-valued attributes? (3–4 marks)

To find the best split point for a continuous-valued attribute $A$:

1. Sort the values of attribute $A$ in increasing order.

2. Consider the midpoint between each pair of adjacent values as a possible split point: $\frac{a_i + a_{i+1}}{2}$.

3. Evaluate the expected information requirement $\text{Info}_A(D)$ for each possible split point.

4. Select the midpoint with the minimum expected information requirement (maximum Information Gain) as the split-point.

5. Partition $D$ into $D_1$ (tuples where $A \le \text{split-point}$) and $D_2$ (tuples where $A > \text{split-point}$).

## Section 4: Numerical Examples (Decision Trees)

### Q10. Given the `Buys_computer` dataset (14 tuples: 9 yes, 5 no), calculate Information Gain for `age` and identify the root node for the ID3 decision tree. (8–10 marks)

1. Total Entropy:
   

   $$
   \text{Info}(D) = I(9, 5) = -\frac{9}{14}\log_2\left(\frac{9}{14}\right) - \frac{5}{14}\log_2\left(\frac{5}{14}\right) = \mathbf{0.940}
   $$

2. Partition on `age`:

   * `age <= 30` (5 tuples: 2 yes, 3 no): $I(2, 3) = 0.971$.

   * `age = 31...40` (4 tuples: 4 yes, 0 no): $I(4, 0) = 0$.

   * `age > 40` (5 tuples: 3 yes, 2 no): $I(3, 2) = 0.971$.

3. Expected information after splitting on `age`:
   

   $$
   \text{Info}_{\text{age}}(D) = \frac{5}{14}(0.971) + \frac{4}{14}(0) + \frac{5}{14}(0.971) = \mathbf{0.694}
   $$

4. Information Gain for `age`:
   

   $$
   \text{Gain}(\text{age}) = 0.940 - 0.694 = \mathbf{0.246}
   $$

5. Comparing with other attributes: $\text{Gain}(\text{income}) = 0.029$, $\text{Gain}(\text{student}) = 0.151$, $\text{Gain}(\text{credit\_rating}) = 0.048$.

6. **Conclusion:** Since `age` has the highest Information Gain ($0.246$), `age` is selected as the root node. Resulting branches: `age <= 30` tests `student` (`no` $\to$ `no`, `yes` $\to$ `yes`); `age = 31...40` $\to$ `yes`; `age > 40` tests `credit_rating` (`excellent` $\to$ `no`, `fair` $\to$ `yes`).

### Q11. Compute the Gain Ratio for the `income` attribute from the `Buys_computer` dataset. (4–5 marks)

Given $\text{Gain}(\text{income}) = 0.029$, and `income` splits the 14 tuples into `low` (4), `medium` (6), and `high` (4):

1. Compute $\text{SplitInfo}$:
   

   $$
   \text{SplitInfo}_{\text{income}}(D) = -\frac{4}{14}\log_2\left(\frac{4}{14}\right) - \frac{6}{14}\log_2\left(\frac{6}{14}\right) - \frac{4}{14}\log_2\left(\frac{4}{14}\right) = \mathbf{1.557}
   $$

2. Compute $\text{GainRatio}$:
   

   $$
   \text{GainRatio}(\text{income}) = \frac{\text{Gain}(\text{income})}{\text{SplitInfo}_{\text{income}}(D)} = \frac{0.029}{1.557} = \mathbf{0.019}
   $$

### Q12. Find the best binary split for the `income` attribute in the `Buys_computer` dataset using the Gini Index. (5–6 marks)

1. Overall Gini Index:
   

   $$
   \text{gini}(D) = 1 - \left(\frac{9}{14}\right)^2 - \left(\frac{5}{14}\right)^2 = \mathbf{0.459}
   $$

2. Split on `{low, medium}` (10 tuples: 7 yes, 3 no) and `{high}` (4 tuples: 2 yes, 2 no):
   

   $$
   \text{gini}_{\{\text{low, medium}\}}(D) = \frac{10}{14}\left[1 - \left(\frac{7}{10}\right)^2 - \left(\frac{3}{10}\right)^2\right] + \frac{4}{14}\left[1 - \left(\frac{2}{4}\right)^2 - \left(\frac{2}{4}\right)^2\right] = \mathbf{0.443}
   $$

3. Comparing other splits: $\text{gini}_{\{\text{low, high}\}}(D) = 0.458$ and $\text{gini}_{\{\text{medium, high}\}}(D) = 0.450$.

4. **Conclusion:** Split on `{low, medium}` and `{high}` since it yields the lowest Gini Index ($0.443$).

## Section 5: Bayes' Theorem — Basics

### Q13. State Bayes' Theorem and explain each of its terms (Prior, Posterior, Likelihood, Evidence). (4–5 marks)

Bayes' Theorem provides a principled way to calculate conditional probability without requiring joint probability directly:

$$
P(H\vert{}\mathbf{X}) = \frac{P(\mathbf{X}\vert{}H) \times P(H)}{P(\mathbf{X})}
$$


Informally: $\text{Posterior} = \frac{\text{Likelihood} \times \text{Prior}}{\text{Evidence}}$.

* $P(H\vert{}\mathbf{X})$ **(Posterior / Posteriori Probability):** Probability that hypothesis $H$ (that $\mathbf{X}$ belongs to class $C$) holds given observed data sample $\mathbf{X}$.

* $P(\mathbf{X}\vert{}H)$ **(Likelihood):** Probability of observing data sample $\mathbf{X}$ given that hypothesis $H$ holds.

* $P(H)$ **(Prior Probability):** Initial probability of hypothesis $H$ before observing $\mathbf{X}$.

* $P(\mathbf{X})$ **(Evidence / Marginal Likelihood):** Probability that sample data $\mathbf{X}$ is observed (calculable via Total Probability Theorem: $P(B) = \sum_{i=1}^{M} P(B\vert{}A_i)P(A_i)$).

### Q14. Differentiate between Joint Probability and Conditional Probability. (3–4 marks)

* **Joint Probability** $P(A, B)$**:** The probability of two (or more) simultaneous events $A$ and $B$ occurring together. Calculated via the product rule $P(A, B) = P(A\vert{}B) \times P(B)$. It is **symmetrical**: $P(A, B) = P(B, A)$.

* **Conditional Probability** $P(A\vert{}B)$**:** The probability of one event $A$ occurring given that another event $B$ has already occurred. Calculated as $P(A\vert{}B) = \frac{P(A, B)}{P(B)}$. It is **not symmetrical**: $P(A\vert{}B) \neq P(B\vert{}A)$.

## Section 6: Prediction Based on Bayes' Theorem

### Q15. Explain how prediction is performed using Bayes' Theorem. Why can $P(\mathbf{X})$ be ignored during classification? (3–4 marks)

Given an $n$-dimensional tuple $\mathbf{X} = (x_1, x_2, \dots, x_n)$ and $m$ classes $C_1, C_2, \dots, C_m$, classification derives the **Maximum A Posteriori (MAP)** hypothesis: $\mathbf{X}$ is predicted to belong to class $C_i$ if and only if $P(C_i\vert{}\mathbf{X}) > P(C_k\vert{}\mathbf{X})$ for all $k \neq i$.

By Bayes' Theorem:

$$
P(C_i\vert{}\mathbf{X}) = \frac{P(\mathbf{X}\vert{}C_i) \times P(C_i)}{P(\mathbf{X})}
$$


Since $P(\mathbf{X})$ is constant for all classes, it does not affect the comparison among classes; therefore, only the numerator $P(\mathbf{X}\vert{}C_i) \times P(C_i)$ needs to be maximized.

### Q16. What is the practical difficulty in using pure Bayes' Theorem for classification? (2–3 marks)

Computing $P(\mathbf{X}\vert{}C_i)$ directly for an $n$-dimensional attribute vector requires initial knowledge of many joint/conditional probabilities, which involves significant computational cost.

## Section 7: Naïve Bayes Classifier

### Q17. Explain the Naïve Bayes Classifier and its class-conditional independence assumption. (4–5 marks)

The **Naïve Bayes Classifier** is a family of statistical classification algorithms based on Bayes' Theorem that assumes **class-conditional independence**—every pair of attributes is assumed to be mutually independent given the class label.

Thus:

$$
P(\mathbf{X}\vert{}C_i) = \prod_{k=1}^{n} P(x_k|C_i) = P(x_1|C_i) \times P(x_2|C_i) \times \dots \times P(x_n|C_i)
$$


This assumption greatly reduces computational cost because it only requires counting the individual class distributions.

### Q18. How does Naïve Bayes handle categorical vs. continuous-valued attributes? (4 marks)

* **Categorical Attribute** $A_k$**:** $P(x_k\vert{}C_i)$ is computed as the number of tuples in class $C_i$ having value $x_k$ for attribute $A_k$, divided by $\vert{}C_{i,D}\vert{}$ (the total number of tuples of class $C_i$ in $D$).

* **Continuous-Valued Attribute** $A_k$**:** $P(x_k\vert{}C_i)$ is computed assuming a Gaussian (Normal) distribution with mean $\mu$ and standard deviation $\sigma$ of attribute $A_k$ for class $C_i$:
  

  $$
  g(x, \mu, \sigma) = \frac{1}{\sqrt{2\pi}\sigma} e^{-\frac{(x - \mu)^2}{2\sigma^2}}, \quad P(x_k|C_i) = g(x_k, \mu_{C_i}, \sigma_{C_i})
  $$

### Q19. Explain the three types of Naïve Bayes Classifiers. (3–4 marks)

1. **Multinomial Naïve Bayes:** Mostly used for document classification (e.g., sports, politics, technology), where features are word frequencies in the document.

2. **Bernoulli Naïve Bayes:** Similar to Multinomial, but predictors are boolean variables (`yes`/`no`), such as whether a word occurs in the text or not.

3. **Gaussian Naïve Bayes:** Used when predictors take continuous numerical values assumed to be sampled from a Gaussian (normal) distribution.

## Section 8: Avoiding the Zero-Probability Problem

### Q20. What is the Zero-Probability (Zero Frequency) problem in Naïve Bayes? How does Laplacian correction solve it? Explain with an example. (4–5 marks)

Naïve Bayes requires every conditional probability in $P(\mathbf{X}|C_i) = \prod_{k=1}^{n} P(x_k|C_i)$ to be non-zero. If a categorical variable has a value in the test dataset not observed in the training dataset for a class, its probability becomes $0$, wiping out the entire product to $0$ (**Zero Frequency / Zero-Probability problem**).

**Solution — Laplacian Correction (Laplacian Estimator):** A smoothing technique that adds $1$ to the count of each case (and adds the number of distinct cases to the denominator).

**Example:** In $1000$ tuples where `income = low` ($0$), `medium` ($990$), and `high` ($10$), adding $1$ to each of the $3$ cases gives corrected probabilities: $P(\text{low}) = \frac{1}{1003}$, $P(\text{medium}) = \frac{991}{1003}$, $P(\text{high}) = \frac{11}{1003}$. These eliminate zero probability while remaining close to the uncorrected estimates.

## Section 9: Naïve Bayes Classifier — Advantages & Disadvantages

### Q21. State the advantages and disadvantages of the Naïve Bayes Classifier. (4–5 marks)

**Advantages:**

1. Easy to implement.

2. Obtains good results in most cases and outperforms other models when predictor independence holds.

3. Requires a small amount of training data, resulting in a shorter training period.

**Disadvantages:**

1. Assumes class-conditional independence among all attributes, causing a loss of accuracy.

2. Cannot model real-world dependencies among variables.

3. Suffers from the Zero Frequency problem when unseen categorical values appear in test data (requires Laplace estimation).

### Q22. Why does Naïve Bayes suffer from loss of accuracy in real-world datasets? How can dependencies among variables be modeled? (3–4 marks)

In real life, it is almost impossible to have predictors that are completely independent. Dependencies practically exist among variables—for example, in hospitals, patient profiles (age, family history), symptoms (fever, cough), and diseases (lung cancer, diabetes) are interdependent. Because Naïve Bayes assumes mutual independence, it cannot model these dependencies, leading to a loss of accuracy. Such dependencies can be modeled using **Bayesian Belief Networks**.

## Section 10: Numerical Examples (Bayes' Theorem & Naïve Bayes)

### Q23. Using the Naïve Bayes classifier, predict the class label for tuple $\mathbf{X} = (\text{age} \le 30, \text{income} = \text{medium}, \text{student} = \text{yes}, \text{credit\_rating} = \text{fair})$ from the `Buys_computer` dataset. (6–8 marks)

1. **Prior Probabilities:**

   * $P(\text{buys\_computer = "yes"}) = \frac{9}{14} = 0.643$

   * $P(\text{buys\_computer = "no"}) = \frac{5}{14} = 0.357$

2. **Conditional Probabilities:**

   * $P(\text{age} \le 30 \mid \text{yes}) = \frac{2}{9} = 0.222$ ; $\quad P(\text{age} \le 30 \mid \text{no}) = \frac{3}{5} = 0.6$

   * $P(\text{income = medium} \mid \text{yes}) = \frac{4}{9} = 0.444$ ; $\quad P(\text{income = medium} \mid \text{no}) = \frac{2}{5} = 0.4$

   * $P(\text{student = yes} \mid \text{yes}) = \frac{6}{9} = 0.667$ ; $\quad P(\text{student = yes} \mid \text{no}) = \frac{1}{5} = 0.2$

   * $P(\text{credit\_rating = fair} \mid \text{yes}) = \frac{6}{9} = 0.667$ ; $\quad P(\text{credit\_rating = fair} \mid \text{no}) = \frac{2}{5} = 0.4$

3. **Likelihoods** $P(\mathbf{X}|C_i)$**:**

   * $P(\mathbf{X} \mid \text{yes}) = 0.222 \times 0.444 \times 0.667 \times 0.667 = 0.044$

   * $P(\mathbf{X} \mid \text{no}) = 0.6 \times 0.4 \times 0.2 \times 0.4 = 0.019$

4. **Maximize** $P(\mathbf{X}|C_i) \times P(C_i)$**:**

   * For `"yes"`: $0.044 \times 0.643 = \mathbf{0.028}$

   * For `"no"`: $0.019 \times 0.357 = \mathbf{0.007}$

5. **Conclusion:** Since $0.028 > 0.007$, $\mathbf{X}$ belongs to class **`buys_computer = "yes"`**.

## Section 11: Model Evaluation and Selection

### Q24. What are the various issues affecting model selection in classification? (4–5 marks)

When comparing and selecting classifiers, the key issues are:

1. **Accuracy:** Ability of the classifier to correctly predict class labels.

2. **Speed:** Time required to construct the model (training time) and time required to use the model (classification/prediction time).

3. **Robustness:** Ability to handle noise and missing values.

4. **Scalability:** Efficiency in disk-resident databases (large datasets).

5. **Interpretability:** Level of understanding and insight provided by the model.

6. **Other Measures:** Goodness of rules, such as decision tree size or compactness of classification rules.

## Section 12: Classifier Evaluation Metrics

### Q25. Draw a confusion matrix and define Accuracy, Error Rate, Sensitivity, Specificity, Precision, Recall, and F-measure with their formulas. (6–8 marks)

**Confusion Matrix Structure:**

| Actual $\backslash$ Predicted | Predicted Positive ($C_1$) | Predicted Negative ($\neg C_1$) | Total | 
| ----- | ----- | ----- | ----- | 
| **Actual Positive (**$C_1$**)** | True Positives ($TP$) | False Negatives ($FN$) | $P$ | 
| **Actual Negative (**$\neg C_1$**)** | False Positives ($FP$) | True Negatives ($TN$) | $N$ | 
| **Total** | $P'$ | $N'$ | $\text{All} = P + N$ | 

**Metrics Formulas:**

* **Accuracy (Recognition Rate):** $\text{Accuracy} = \frac{TP + TN}{\text{All}}$ *(percentage of test tuples correctly classified)*

* **Error Rate:** $\text{Error Rate} = 1 - \text{Accuracy} = \frac{FP + FN}{\text{All}}$ *(percentage of test tuples misclassified)*

* **Sensitivity:** $\text{Sensitivity} = \frac{TP}{P} = \frac{TP}{TP + FN}$ *(True Positive recognition rate)*

* **Specificity:** $\text{Specificity} = \frac{TN}{N} = \frac{TN}{FP + TN}$ *(True Negative recognition rate)*

* **Precision (Exactness):** $\text{Precision} = \frac{TP}{TP + FP}$ *(percentage of tuples labeled positive that are actually positive)*

* **Recall (Completeness):** $\text{Recall} = \frac{TP}{TP + FN}$ *(percentage of actual positive tuples labeled positive)*

* **F-measure (**$F_1$**):** $F_1 = \frac{2 \times \text{precision} \times \text{recall}}{\text{precision} + \text{recall}}$ *(harmonic mean of precision and recall)*

* **Weighted** $F_\beta$**:** $F_\beta = \frac{(1 + \beta^2) \times \text{precision} \times \text{recall}}{\beta^2 \times \text{precision} + \text{recall}}$ *(assigns* $\beta$ *times more weight to recall than precision)*

### Q26. What is the class imbalance problem? Why are Sensitivity and Specificity preferred over Accuracy in such cases? (3–4 marks)

The **class imbalance problem** occurs when one class is rare (e.g., fraud or HIV-positive), leading to a significant majority of negative tuples and a small minority of positive tuples. In such cases, overall accuracy can be deceptively high even if the classifier misses most rare positive cases. **Sensitivity** (True Positive recognition rate, $\frac{TP}{P}$) and **Specificity** (True Negative recognition rate, $\frac{TN}{N}$) evaluate positive and negative class recognition separately, revealing true performance on the rare class.

## Section 13: Numerical Examples (Evaluation Metrics)

### Q27. Given a $2 \times 2$ confusion matrix for cancer detection ($TP = 90, FN = 210, FP = 140, TN = 9560$), compute Accuracy, Error Rate, Sensitivity, Specificity, Precision, Recall, and $F_1$-score. Comment on the classifier's performance. (6–8 marks)

**Totals:** $P = 90 + 210 = 300$; $N = 140 + 9560 = 9700$; $P' = 90 + 140 = 230$; $\text{All} = 10000$.

* **Accuracy:** $\frac{90 + 9560}{10000} = \mathbf{96.50\%}$ *(Note: slide prints* $96.40\%$ *due to textbook typo)*.

* **Error Rate:** $\frac{140 + 210}{10000} = \mathbf{3.50\%}$.

* **Sensitivity:** $\frac{90}{300} = \mathbf{30.00\%}$.

* **Specificity:** $\frac{9560}{9700} = \mathbf{98.56\%}$.

* **Precision:** $\frac{90}{230} = \mathbf{39.13\%}$.

* **Recall:** $\frac{90}{300} = \mathbf{30.00\%}$.

* $F_1$ **Score:** $\frac{2 \times 0.3913 \times 0.3000}{0.3913 + 0.3000} = \mathbf{33.96\%}$.

**Comment:** Despite high overall accuracy ($96.50\%$), the classifier performs poorly because Sensitivity/Recall is only $30.00\%$—it misses $70\%$ of actual cancer patients due to class imbalance.

## Section 14: Evaluating Classifier Accuracy — Holdout & Cross-Validation Methods

### Q28. Explain the Holdout method and $k$-fold Cross-Validation for evaluating classifier accuracy. (5–6 marks)

* **Holdout Method:** The dataset is randomly partitioned into two independent sets—a training set (typically $2/3$) used to construct the model, and a test set (typically $1/3$) used to estimate accuracy.

* $k$**-fold Cross-Validation:** The dataset is randomly partitioned into $k$ mutually exclusive subsets (folds) $D_1, D_2, \dots, D_k$ of approximately equal size ($k = 10$ is most popular). In the $i$-th iteration, $D_i$ is used as the test set while the remaining $(k - 1)$ subsets serve as the training set. Overall accuracy is estimated across all $k$ iterations.

### Q29. Write short notes on: (a) Random Subsampling, (b) Leave-One-Out Cross-Validation, and (c) Stratified Cross-Validation. (4–5 marks)

* **(a) Random Subsampling (Random Sampling):** A variation of the holdout method where holdout is repeated $k$ times, and overall accuracy is the average of the $k$ obtained accuracies.

* **(b) Leave-One-Out (LOO):** A special case of $k$-fold cross-validation where $k$ equals the total number of tuples in the dataset; suitable for small-sized datasets.

* **(c) Stratified Cross-Validation:** Folds are stratified so that the class distribution in each fold is approximately the same as in the initial dataset. Stratified $k$-fold cross-validation is recommended for accuracy estimation.

## Section 15: Ensemble Methods

### Q30. What are Ensemble Methods? Explain Bagging and Boosting, and compare them. (6–8 marks)

**Ensemble Methods** combine a series of $k$ learned models ($M_1, M_2, \dots, M_k$) to create an improved composite model $M^*$ with higher classification accuracy.

* **Bagging (Bootstrap Aggregation):** At each iteration $i$, a training set $D_i$ of $d$ tuples is sampled with replacement (bootstrap) from $D$, and classifier $M_i$ is learned. For an unknown sample $\mathbf{X}$, each $M_i$ returns its prediction and $M^*$ assigns the class with the majority vote (or average for continuous prediction). It is more robust to noisy data and improves accuracy over a single classifier.

* **Boosting:** Weights are assigned to each training tuple, and $k$ classifiers are learned iteratively. After $M_i$ is learned, weights are updated so the next classifier $M_{i+1}$ pays more attention to tuples misclassified by $M_i$. The final model $M^*$ combines votes weighted by each classifier's accuracy.

**Comparison:**

| Feature | Bagging | Boosting | 
| ----- | ----- | ----- | 
| **Sampling Mechanism** | Bootstrap sampling (independent, with replacement) | Iterative weighted sampling based on past error | 
| **Model Combination** | Equal-weight majority voting / averaging | Weighted voting based on individual model accuracy | 
| **Noise & Overfitting** | Robust to noise and less prone to overfitting | Can overfit to noisy data / misclassified outliers | 
| **Accuracy Level** | High accuracy improvement | Higher accuracy potential than Bagging | 

### Q31. Explain the AdaBoost algorithm along with its error rate and classifier vote weight formulas. (5–6 marks)

**AdaBoost** (Freund & Schapire, 1997) takes $d$ class-labeled tuples and initializes all tuple weights equally to $\frac{1}{d}$. It generates $k$ classifiers in $k$ rounds. In round $i$:

1. Tuples from $D$ are sampled with replacement to form training set $D_i$ of size $d$, with each tuple's selection probability based on its weight.

2. Classifier $M_i$ is derived from $D_i$ and its error rate is computed using $D_i$ as a test set:
   

   $$
   \text{error}(M_i) = \sum_{j=1}^{d} w_j \times \text{err}(\mathbf{X}_j)
   $$

   
   where $\text{err}(\mathbf{X}_j)$ is the misclassification error of tuple $\mathbf{X}_j$.

3. If a tuple is misclassified, its weight is increased; otherwise, its weight is decreased.

4. The weight of classifier $M_i$'s vote is:
   

   $$
   \log \frac{1 - \text{error}(M_i)}{\text{error}(M_i)}
   $$

### Q32. Explain Random Forest and its two construction methods (Forest-RI and Forest-RC). (4–5 marks)

**Random Forest** (Breiman, 2001) is an ensemble where each classifier is a decision tree generated using a random selection of attributes at each node to determine the split. During classification, each tree votes and the most popular class is returned.

**Two Construction Methods:**

1. **Forest-RI (Random Input Selection):** Randomly selects $F$ attributes as candidates for splitting at each node, using CART to grow trees to maximum size.

2. **Forest-RC (Random Linear Combinations):** Creates new attributes that are linear combinations of existing attributes, reducing correlation between individual classifiers.

**Key Advantages:** Random Forest has accuracy comparable to AdaBoost, is more robust to errors and outliers, is insensitive to the number of attributes selected at each split, and is faster than bagging or boosting.