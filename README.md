# End-to-End-Azure-Data-Engineering Project

## Architecture
This project follows the **Medallion Architecture**, a data design pattern that enhances data quality through multiple stages:
- **Bronze Layer**: Raw data ingestion
- **Silver Layer**: Data transformation and cleansing
- **Gold Layer**: Aggregated and ready for downstream users like data analysts or data scientists

## Tools & Services Used
- **Azure Data Factory (ADF)**: To create data pipelines for data moving data
- **Azure Data Lake Storage Gen2 (ADLS)**: To store data in multiple containers corresponding to the Medallion layers
- **Azure Key Vault**: To store secrets
- **Azure Databricks**: To transform and process data before storing in Silver layer
- **Azure Synapse Analytics**: Data warehouse solution for serving the data to downstream users

## Data Source
The dataset is sourced from the following GitHub repository:
[Adventure Works Data Engineering Project](https://github.com/anshlambaoldgit/Adventure-Works-Data-Engineering-Project/tree/main/Data)

## Storage Setup
Created an Azure Data Lake Storage (ADLS) account with three containers: Bronze, Silver, and Gold. Data is stored in these containers at different processing stages.

## Bronze Layer
In this stage, data is extracted from the source and stored in the **Bronze Layer** as-is.
- Created a **dynamic data pipeline** using **Azure Data Factory (ADF)** to move data from the **GitHub API** to the **Bronze container in ADLS**.
- Used **Copy Data Activity** along with **LookUp** and **ForEach activities**.
- The pipeline dynamically fetches multiple datasets using a **JSON configuration file** (`parameters.json`), which stores parameters as key-value pairs.
- These parameters are passed dynamically into **Copy Data Activity** to configure source and sink settings without rewriting code.
- The pipeline structure can be seen in **pipeline.png**.
- Debugged and validated the pipeline execution to ensure correctness and efficiency, then **successfully published** it.

## Silver Layer
- Used **Service Principal Authentication** for **Databricks** to access **ADLS**.
- Registered an **App in Microsoft Entra ID** and assigned the **Storage Blob Data Contributor role**.
- Created a **secret for the app** and stored the **App ID, Directory ID, and secret** in **Azure Key Vault**.
- Created a **Databricks scope** linked to **Key Vault**.
- Used **Spark Config** for authentication and access to the **Bronze Layer data**.
- Applied **various transformations** and stored the **cleaned & processed data in the Silver Layer** (`silver_layer.ipynb`).

## Next Steps
- **Gold Layer:** Further transformations and aggregations will be applied to prepare analytics-ready data.
- The repository will be updated with the **Gold Layer processing details** once completed.

---
### Files Uploaded to GitHub:
1. **README.md** (this file)
2. **silver_layer.ipynb** (Data transformations in Databricks)
3. **parameters.json** (JSON file for dynamic pipeline configurations in ADF)

Further updates will be made after Gold Layer processing is completed.
