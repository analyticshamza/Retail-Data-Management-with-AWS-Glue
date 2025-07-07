# Retail Data Management with AWS Glue

This project showcases my skills in building a complete ETL pipeline using **AWS Glue** and **Amazon S3** to process, clean, and analyze retail data. It demonstrates my ability to work with cloud-based data workflows and deliver analytical insights from raw datasets.

## 📌 Project Summary

In this project, I:

* Uploaded raw product and transaction data to Amazon S3
* Created AWS Glue **classifiers**, **crawlers**, and a **Visual ETL job**
* Performed an **inner join** on `Product ID` to combine transaction and product metadata
* Used **regex** to clean currency values in the `Sales` column
* Applied an **aggregate transformation** to calculate the average net sales grouped by product category and ship mode
* Stored the final output in **Parquet format** in an S3 output bucket
* Queried the output using **S3 Select** to confirm the transformation result

## ✅ Steps Performed

1. **Data Upload**

   * Uploaded `transactions.csv` to `transaction-files/` folder in an S3 bucket
   * Uploaded `product details.csv` to `product-files/` folder in the same bucket

2. **AWS Glue Setup**

   * Created a Glue database named `abc-retail`
   * Created two classifiers for reading CSV files with headers:

     * `txnClass` for `transactions.csv`
     * `cust_classifier` for `product details.csv`
   * Created two crawlers to import both datasets into the Glue Data Catalog

3. **Visual ETL Job**

   * Added Glue Data Catalog nodes for both tables
   * Joined the datasets on `Product ID` using an **Inner Join**
   * Dropped one duplicate `Product ID` column
   * Used **Regex Extractor** on `Sales` column to extract numeric values into a new column called `NetSales`
   * Applied **Aggregate** transformation:

     * Grouped by: `Product Category`, `Ship Mode`
     * Aggregated field: `NetSales`
     * Aggregation function: `Average`
   * Saved output to another S3 bucket in **Parquet format** with **Snappy compression**

4. **Result Verification**

   * Queried the `.parquet` output file using **S3 Select** with SQL:

     ```sql
     SELECT * FROM s3object
     ```
   * Confirmed correct aggregation with output:

     ```
     Fashion	Second Class	1274.702381
     ```

## 🖼️ Screenshots

You can find all key screenshots in the project submission, including:

| Step                     | Screenshot Description                            |
| ------------------------ | ------------------------------------------------- |
| S3 Bucket Setup          | Buckets and uploaded CSV files                    |
| Classifier Configuration | CSV classifier setup for transactions and product |
| Crawler Run Status       | Crawler creation and successful table generation  |
| Visual ETL Canvas        | Full layout of the ETL job with connected nodes   |
| Join Node Settings       | Join keys selected on `Product ID`                |
| Regex Extractor Settings | Regex used to clean `Sales` column                |
| Aggregate Settings       | Grouping and average aggregation on NetSales      |
| S3 Select Query          | Output query result confirming correct ETL flow   |

## 📄 Files Included

* `transactions.csv` — Raw sales transaction data
* `product details.csv` — Product metadata
* `Retail Data Management Project.pdf` — Project prompt and instructions

## 📝 Project Purpose

This project was completed to demonstrate hands-on skills in AWS Glue ETL pipeline design, data cleaning using regex, aggregation logic, and S3-based querying for analytics use cases.

## 📜 License

MIT License — see [LICENSE](LICENSE).
