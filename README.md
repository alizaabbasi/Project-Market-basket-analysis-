# Market-Basket Analysis using Spark and the SON Algorithm

A production-grade, distributed big data mining pipeline implemented in **Python 3** using **Apache Spark (PySpark RDD APIs)**. This project discovers frequent itemsets—specifically, frequent collaborating actor patterns—within an IMDB movie dataset.

---

## 📜 Project Requirements & Scope
As specified by the course syllabus, this implementation strictly adheres to the following constraints:
* **Distributed Architecture:** Implemented via Apache Spark leveraging low-level **RDD operations** (`mapPartitions`, `flatMap`, `reduceByKey`).
* **Algorithmic Framework:** Utilizes the two-pass **SON (Savasere, Omiecinski, and Navathe) Algorithm** to guarantee seamless horizontal scaling across data clusters without memory constraints.
* **Security Compliance:** Private Kaggle API credentials have been completely sanitized and replaced with dummy strings (`xxxxxx`) prior to deployment.

---

## 🧠 Algorithmic Framework Overview

### Market-Basket Formulation
* **Items:** Individual actors/stars.
* **Baskets:** The transactional group of primary cast members (`Star1`, `Star2`, `Star3`, `Star4`) within an individual movie row. 

### The Two-Pass SON Mechanism
1.  **Pass 1 (Local Candidate Mining):** The data RDD is divided into independent chunks using `.mapPartitions()`. Each partition runs a localized **Apriori Algorithm** utilizing a dynamically scaled down `local_support` threshold based on subset monotonicity. The localized frequent pairs are aggregated globally via `.distinct().collect()` to form a definitive Candidate Set.
2.  **Pass 2 (True Global Counting):** The candidate set is distributed efficiently to all cluster worker nodes using a memory-optimized Spark `.broadcast()` wrapper. The full RDD is scanned using `.flatMap()` to match transactions against candidates, and true support sums are accumulated via `.reduceByKey()`. Pairs failing to meet the `GLOBAL_SUPPORT` threshold are filtered out, mathematically guaranteeing zero false negatives.

---

## 🛠️ Step-by-Step Environment Setup & Execution

### Prerequisites
The entire environment is configured to run out-of-the-box inside a standard Jupyter environment like **Google Colab** using runtime-allocated clusters.

### Execution
1. Open the `.ipynb` notebook file inside Google Colab using the integrated badge helper.
2. Provision a Spark cluster session inside the script.
3. Replace the placeholder environment variables in the setup cell with your unique Kaggle API token credentials to pull down the automated `imdb-dataset-of-top-1000-movies-and-tv-shows` dependencies:
   ```python
   os.environ['KAGGLE_USERNAME'] = "your_actual_username"
   os.environ['KAGGLE_KEY'] = "your_actual_key"
