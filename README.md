# Big Data Clustering TP

## Step 1: Environment Setup

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

### Step 1.4: Basic K-means Test

**scikit-learn test:**

- Load a small dataset (Iris) and run K-means to verify local clustering works.

**PySpark test:**

- Convert the same dataset to a Spark DataFrame.
- Run K-means to verify distributed clustering works.

---

### Step 1.5: Notes

- Both scikit-learn and PySpark K-means should run successfully.
- scikit-learn is fast and simple for small datasets.
- PySpark is scalable and suitable for large datasets.
- Environment setup is now verified and ready for the next steps of the project.
