Project done during internship. 
###   Use cases:
1. Find the orders which has been delayed than the expected delivery date. 
2. Find the Top 3 selling products of each category.
3. Find maximum spending customers for every month of last year.
4. Top 2 Highest earning sellers by each location.

Also some additional cases were added.


---

### How to Run This Project:

This project is designed to be executed within a **Databricks Lakehouse Environment**, leveraging Apache Spark for data processing.

**Prerequisites:**

1.  **Databricks Community Edition Account:** Ensure you have access to a Databricks Community Edition workspace.
2.  **Python 3.x:** Installed on your local machine (if using `databricks-connect` for local development).
3.  **Required Python Libraries:**
    * Install the necessary libraries using `pip`:
        ```bash
        pip install -r requirements.txt
        ```
        (Make sure to create a `requirements.txt` file at the root of the project by running `pip freeze > requirements.txt` from your development environment if you don't have one).
4.  **Olist Brazilian E-commerce Dataset:**
    * Download all `.csv` files from the [Kaggle Dataset Link](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce).
    * **Upload to Databricks File System (DBFS):**
        * Log in to your Databricks workspace.
        * Navigate to "Data" (left sidebar) -> "Create Table" -> "Upload File".
        * Upload all the downloaded CSVs. They will typically be stored under `/FileStore/tables/`. (Adjust paths in your scripts if you store them elsewhere).

**Execution Steps on Databricks:**

1.  **Import Project to Databricks:**
    * **Option A (Manual Upload):** Create a new folder in your Databricks Workspace (e.g., `PROJECT-BRAZILIAN-E-COMMERCE`). Then, for each `.py` file:
        * Right-click on the folder -> "Create" -> "Import".
        * Select "File" and upload `project_orchestrator.py`, `use_case_1.py`, etc., as Python notebooks.
    * **Option B (Git Integration - Recommended for full project):** If your Databricks workspace is configured with Git integration, you can clone this entire GitHub repository directly into your workspace. This maintains the folder structure.

2.  **Attach to a Cluster:**
    * Ensure you have a running Databricks cluster (e.g., the default Community Edition cluster).
    * Attach all imported notebooks (`.py` files) to this cluster.
    * Verify that any required custom libraries (beyond the default Databricks Runtime) are installed on your cluster via the "Libraries" tab of the cluster configuration.

3.  **Run the Orchestrator:**
    * Open the `project_orchestrator.py` notebook in your Databricks workspace.
    * This script is designed to sequentially execute the logic for each use case.
    * **Run All:** Execute the entire `project_orchestrator.py` notebook. It will call functions or run the content of `use_case_X.py` scripts.

**Expected Outputs:**

Upon successful execution of `project_orchestrator.py`:

* **Data Outputs:** (Specify where your scripts save output data. Examples:)
    * Cleaned and transformed data should reside in Delta Lake tables within DBFS (e.g., `/mnt/delta/silver/`, `/mnt/delta/gold/`). You can query these using SQL in Databricks.
    * Specific results for each use case (e.g., delayed orders list, top products) might be saved as separate Delta tables or Parquet files.
* **HTML Report:** The `business_report.html` file within the `DAG & Report/` directory should be generated or updated, providing a summary of the findings from the use cases. (Explain how to view/access this, e.g., if it's saved to DBFS, you might need to download it or view it via Databricks File Browser if it supports HTML rendering).
* **Console Output:** Intermediate results or progress messages might be printed to the notebook's output console.

---

### Key Decisions / Design Considerations (Add more details here):

* **Data Ingestion Strategy:** (e.g., Why CSV upload? Mention the Medallion Architecture if you've implemented it in your code implicitly or explicitly.)
* **Data Transformation Approach:** (e.g., PySpark for scalability, specific joins performed, handling of data types, missing values.)
* **Use Case Implementation:** (Briefly explain the logic for each `use_case_X.py` - e.g., for "delayed orders," how is "delayed" defined? What Spark transformations are used?)
* **Orchestration:** (Briefly explain how `project_orchestrator.py` manages the workflow.)

---

### Enhancements & Future Work (Optional):

* Integrate Databricks Lakeflow (formerly Delta Live Tables) for robust pipeline definition.
* Implement MLflow for tracking experiments and managing models.
* Containerize the application for easier deployment.
* Explore more advanced ML models for specific use cases (e.g., time series forecasting for demand).
* Set up a scheduled Databricks Job for daily/weekly runs of the `project_orchestrator.py`.
* Implement data quality checks (e.g., using Great Expectations or Databricks expectations).
