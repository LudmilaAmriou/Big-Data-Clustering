# Big Data Clustering TP

## Detailed Report

For a comprehensive overview of datasets, benchmarks, visualizations, and analysis, see the full report:  
[Big Data Clustering Detailed Report](https://ueve-my.sharepoint.com/:w:/g/personal/20253305_etud_univ-evry_fr/IQCXKE0qHYCTQ5Pb3KnbyJ6HAaAg_GOQMRNMdHZKts6yIPM?e=n0kecG)

## Environment Setup

This project requires **Apache Spark** and **scikit-learn** to run K-means clustering on small, medium, and large datasets. The following steps guide you through the setup process.

---

### Step 1.1: Create a Virtual Environment

1. Open a terminal and navigate to the project folder.
2. Create a virtual environment to isolate dependencies:
   - Use `python3 -m venv venv`.
3. Activate the virtual environment:
   - Linux / Mac: `source venv/bin/activate`
   - Windows: `venv\Scripts\activate`
4. Verify that the environment is active before installing packages.

---

### Step 1.2: Install Required Packages

Install the following Python packages in your virtual environment:

- `pyspark` → distributed K-means
- `scikit-learn` → local K-means comparison
- `matplotlib` & `seaborn` → visualization
- `pandas` → data handling
- `jupyter` → notebook environment

---

### Step 1.3: Verify Installation

1. Open Python or a Jupyter notebook.
2. Import the installed packages to confirm they work:
   - `pyspark`, `sklearn`, `matplotlib`, `pandas`
3. Check the version numbers to ensure correct installation.
4. Resolve any errors before proceeding.

---

### Step 1.4: Running the Notebook

1. Open `notebooks.-means.ipynb` in **Jupyter** or **Colab**.
2. **Important:** All imports (packages, Spark session, utility functions) are in a **single cell** at the beginning of the notebook.
   - Make sure to **run this cell first** every time you open the notebook, otherwise subsequent cells will fail.
3. Run cells sequentially to execute:
   - Benchmarking
   - Cluster visualizations
   - Performance plots
4. Modify `k` values or dataset subsets in code as needed.
5. **Tip:** Preferably run the notebook on **Google Colab** for memory safety and optional GPU usage, especially for large datasets.

### Step 1.5: Basic K-means Test

**scikit-learn test:**

- Load a small dataset (Iris) and run K-means to verify local clustering works.

**PySpark test:**

- Convert the same dataset to a Spark DataFrame.
- Run K-means to verify distributed clustering works.

---

### Step 1.6: Notes

- Both scikit-learn and PySpark K-means should run successfully.
- scikit-learn is fast and simple for small datasets.
- PySpark is scalable and suitable for large datasets.
- Environment setup is now verified and ready for the next steps of the project.

## Step 2: Datasets

The project uses three categories of datasets:

1. **Small datasets**

   - **Iris**: 150 samples × 4 features, 3 classes  
     Used to illustrate clustering performance with true labels and visualize cluster alignment.
   - **Wine**: 178 samples × 13 features, 3 classes

2. **Medium datasets**

   - **MNIST-10k**: 10,000 samples × 784 features, 10 classes  
     Only a subset (2,000 samples) is visualized for clarity.
   - **Titanic numeric**: 891 samples × 7 numeric features  
     No true labels available; evaluation relies on silhouette score only.

3. **Large & Very Large datasets**
   - **Higgs-100k**: 100,000 samples × 28 features
   - **Synthetic-500k-PCA**: 500,000 samples × 20 features, reduced via PCA to 5 dimensions
   - **Synthetic-1M-PCA**: 1,000,000 samples × 20 features, reduced via PCA to 5 dimensions

---

## Step 3: K-means Benchmarking

- **k values used:** `3`, `5`, `8` for small datasets and Higgs; `5` and `10` for very large datasets due to memory considerations.
- Both **scikit-learn** and **PySpark** implementations are benchmarked for:

  - Execution time
  - Number of iterations / training cost
  - Memory usage (Δ MB)
  - CPU usage (Δ %)
  - Inertia (only for scikit-learn; PySpark does not expose it)
  - Silhouette score

- **Visualization** is performed for datasets with true labels (Iris, Wine, MNIST subset), showing **side-by-side comparison** of true labels vs. predicted clusters, aligned with unified colors.

---

## Step 4: Quality Assessment & Visualization

- **Silhouette scores** guide the selection of the best `k`.
- **Aligned colors** between true labels and cluster labels improve clarity.
- **Side-by-side plots** show true classes and K-means results for each `k`.
- Runtime, memory, CPU, and silhouette comparisons are visualized using **matplotlib** and **seaborn**.

**Example Summary of Benchmark Results**

The table below summarizes **execution time**, **iterations/cost**, **memory & CPU usage**, and **silhouette scores** for all datasets and frameworks:

| Dataset            | Framework | Time (sec) | Iterations/Cost | Memory Δ MB | CPU Δ % | Silhouette |
| ------------------ | --------- | ---------- | --------------- | ----------- | ------- | ---------- |
| Higgs-100k         | Sklearn   | 1.712      | 127.5           | 0.001       | -14.7   | 0.021      |
| Higgs-100k         | Spark     | 45.806     | 2,623,853.8     | 0.007       | 17.2    | 0.038      |
| Iris               | Sklearn   | 0.003      | 8.667           | 0.0         | 32.5    | 0.379      |
| Iris               | Spark     | 1.748      | 122.416         | 0.0         | 60.3    | 0.580      |
| MNIST-10k          | Sklearn   | 1.348      | 51.0            | 0.0         | 6.467   | 0.023      |
| MNIST-10k          | Spark     | 16.622     | 6,041,504.99    | 0.0         | 4.3     | 0.021      |
| Synthetic-1M-PCA   | Spark     | 164.936    | 5,592,396.88    | 0.019       | 0.567   | 0.644      |
| Synthetic-500k-PCA | Spark     | 108.741    | 2,613,885.69    | 0.016       | 0.333   | 0.670      |
| Titanic-numeric    | Sklearn   | 0.004      | 8.333           | 0.0         | -22.0   | 0.280      |
| Titanic-numeric    | Spark     | 1.638      | 577.298         | 0.0         | 4.567   | 0.359      |
| Wine               | Sklearn   | 0.004      | 6.333           | 0.0         | -16.9   | 0.216      |
| Wine               | Spark     | 1.533      | 1,126.691       | 0.0         | 26.1    | 0.378      |

**Interpretation:**

- **Sklearn** is very fast for small datasets (Iris, Wine, Titanic), but Spark is slower due to distributed overhead.
- **Spark** scales better for large datasets (Synthetic-500k/1M), but shows high iterations/cost values due to its distributed computation.
- **Silhouette scores** indicate clustering quality; for small datasets, Spark sometimes produces better separation (e.g., Iris: 0.580 vs 0.379).
- **Memory usage** appears negligible in the table because `psutil` measurement granularity is too low for these operations in Colab.
- **CPU %** may be negative for Sklearn if the notebook was idle before running, or small/medium datasets do not fully utilize all cores in Spark.

> Overall, this table provides a quick overview of **performance vs. clustering quality** across datasets and frameworks.

---

## Step 5: Limitations

- **Very large datasets** cannot be fully visualized due to size.
- **Titanic numeric** has no true labels for clustering evaluation.
- **Colab environment** is used for memory safety and GPU availability.
- **PySpark CPU usage** may appear low for small/medium datasets due to Spark overhead and task scheduling.
- **PySpark Inertia** is not directly available, so comparisons with scikit-learn inertia are limited.

---

## Step 6: Notes

- scikit-learn is fast and simple for **small datasets**.
- PySpark is scalable and suitable for **large datasets**, but introduces overhead for small datasets.
- PCA is used for large synthetic datasets to reduce dimensionality and avoid memory issues.
- All benchmarking and visualizations are included in the notebook.

---

## References

- [scikit-learn KMeans](https://scikit-learn.org/stable/modules/generated/sklearn.cluster.KMeans.html)
- [PySpark MLlib KMeans](https://spark.apache.org/docs/latest/ml-clustering.html#k-means)
- Google Colab for memory-safe execution
- [Spark for KMeans clustering optimization](https://medium.com/operations-research-bit/cutting-edge-clustering-techniques-a-spark-driven-approach-to-k-means-clustering-optimization-96f15b1f68ad)
- [K-Means Clustering using PySpark Python](https://www.geeksforgeeks.org/machine-learning/k-means-clustering-using-pyspark-python/)
- [K-Means clustering on the handwritten digits data using Scikit Learn in Python](https://www.geeksforgeeks.org/machine-learning/k-means-clustering-on-the-handwritten-digits-data-using-scikit-learn-in-python/)
