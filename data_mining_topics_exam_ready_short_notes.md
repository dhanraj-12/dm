# Data Mining: Exam-Ready Short Notes

---

## 1. Multidimensional Data Analysis
* **Definition:** Analyzing data across multiple dimensions (perspectives) simultaneously rather than in flat, 2-D tables.
* **Data Cube:** Core $n$-dimensional structure storing precomputed measures (e.g., `total_sales`, `count`) across dimensions like *Time*, *Location*, and *Item*.
* **Cuboids:**
  * **Base Cuboid:** Lowest level of summarization (most detailed).
  * **Apex Cuboid (0-D):** Highest level of summarization (`all`).
* **Key OLAP Operations:**
  * **Roll-up:** Summarizing data by climbing up a concept hierarchy (e.g., City $\rightarrow$ Country).
  * **Drill-down:** Navigating to finer details (e.g., Quarter $\rightarrow$ Month).
  * **Slice & Dice:** Selecting a subcube by filtering on one or more dimensions.
  * **Pivot (Rotate):** Reorienting the multidimensional view of data.
* **Applications:** Business Intelligence (BI), sales forecasting, and financial reporting.

---

## 2. Mining Spatial Data
* **Definition:** Discovering implicit, interesting patterns and relationships from **geographic or location-based data** (maps, GPS, satellite imagery, GIS).
* **Key Characteristics:**
  * Deals with spatial objects (points, lines, polygons) and spatial relationships (distance, direction, adjacency, containment).
  * **Spatial Autocorrelation:** Nearby objects tend to have similar properties.
* **Key Techniques:**
  * **Spatial Clustering:** Grouping geographically close regions with similar attributes.
  * **Spatial Association Rules:** Finding co-located features (e.g., *houses near schools and parks have higher prices*).
  * **Spatial Classification & Trend Analysis:** Predicting labels or changes across regions.
* **Applications:** Urban planning, crime hotspot detection, weather/environmental monitoring, and retail store site selection.

---

## 3. Mining Multimedia Data
* **Definition:** Extracting meaningful patterns and knowledge from unstructured **images, audio, and video** datasets.
* **Key Challenge:** High dimensionality, large storage size, and lack of structured attributes.
* **Key Techniques:**
  * **Feature Extraction:** Converting raw media into numeric features—color histograms, texture, and shape (for images); pitch, tempo, and energy (for audio).
  * **Content-Based Image/Video Retrieval (CBIR):** Searching media using visual/audio similarity rather than text tags.
  * **Multimedia Classification & Clustering:** Grouping or labeling images, speech, or video frames.
* **Applications:** Facial recognition, medical image diagnosis (X-ray/MRI tumor detection), CCTV anomaly detection, and visual product search.

---

## 4. Mining Time-Series and Sequential Data

### A. Time-Series Data
* **Definition:** Sequence of data values recorded at **regular, uniform time intervals** (e.g., hourly, daily, monthly).
* **Components:** Long-term **Trend**, **Seasonal** variations, **Cyclic** movements, and **Irregular/Random** noise.
* **Key Techniques:** Similarity search, subsequence matching, forecasting, and dimensionality reduction using **DFT** (Discrete Fourier Transform), **DWT** (Discrete Wavelet Transform), or **SVD/PCA**.
* **Applications:** Stock market prediction, weather forecasting, and ECG/heart-rate monitoring.

### B. Sequential Data
* **Definition:** Ordered list of events occurring over time (not necessarily at equal intervals).
* **Key Technique:** **Sequential Pattern Mining** (e.g., GSP, PrefixSpan) to find frequent order-based patterns.
* **Applications:** Market basket sequences (*Camera $\rightarrow$ Memory Card $\rightarrow$ Printer*), DNA/biological sequence analysis, and customer clickstream analysis.

---

## 5. Mining Text Datasets (Text Mining)
* **Definition:** Extracting structured, actionable knowledge from **unstructured text** (emails, reviews, social media, articles).
* **Preprocessing Steps:** Tokenization, stop-word removal, stemming/lemmatization, and vector representation (e.g., Bag-of-Words, TF-IDF).
* **Key Techniques:**
  * **Text Classification:** Assigning predefined categories (e.g., spam vs. non-spam).
  * **Text Clustering:** Grouping similar documents without predefined labels.
  * **Sentiment Analysis (Opinion Mining):** Determining whether text expresses positive, negative, or neutral sentiment.
  * **Information Extraction & Summarization:** Pulling entities, keywords, or concise summaries.
* **Applications:** Spam filtering, customer feedback analysis, news categorization, and chatbots.

---

## 6. Web Mining
* **Definition:** Applying data mining techniques to discover useful patterns from the **World Wide Web**.
* **Three Main Categories:**
  1. **Web Content Mining:** Extracting information from actual web page contents (text, images, audio, video, structured tables).
  2. **Web Structure Mining:** Analyzing hyperlink structures (nodes = pages, edges = links) to find authoritative pages and communities (e.g., PageRank, HITS).
  3. **Web Usage Mining:** Analyzing server logs, clickstreams, and search histories to understand user behavior.
* **Applications:** Search engine ranking, personalized product recommendations, targeted advertising, and website layout optimization.

---

## Quick Revision Summary Table

| Topic | Data Type | Core Techniques / Keywords | Main Example |
| :--- | :--- | :--- | :--- |
| **Multidimensional Analysis** | Structured / Data Warehouse | Data Cube, OLAP (Roll-up, Drill-down) | Sales by Time, Region, Product |
| **Spatial Data Mining** | Maps, GPS, Satellite (GIS) | Spatial Clustering, Association, Autocorrelation | Crime hotspots, Store location |
| **Multimedia Data Mining** | Images, Audio, Video | Feature Extraction, CBIR, Classification | Face ID, Medical X-ray analysis |
| **Time-Series & Sequential** | Time-stamped / Ordered events | Trend analysis, DFT/DWT, Sequential Patterns | Stock prediction, DNA sequences |
| **Text Mining** | Unstructured written text | NLP, TF-IDF, Sentiment Analysis | Spam filter, Review analysis |
| **Web Mining** | Web pages, Links, Logs | Content, Structure (PageRank), Usage Mining | Search ranking, Recommendations |