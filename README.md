#🛍️ Retail Data Management with AWS Glue

A sample ETL project demonstrating how to use **AWS Glue** to extract, transform, and load retail data stored in Amazon S3.

## ⭐️ About This Project?

* Configure AWS Glue **Classifiers**, **Crawlers**, and **Visual ETL** jobs
* Understand **best practices** for working with CSV and Parquet in AWS
* Get hands‑on with:

  * **Joining** datasets
  * **Cleaning** currency values with **Regex**
  * **Aggregating** data for analytics
  * **Querying** Parquet outputs with **S3 Select**

## 📁 Repository Structure

```
├── data/
│   ├── transactions.csv
│   └── product details.csv
├── etl/
│   ├── glue_crawlers_setup.md    # Manual steps to configure classifiers & crawlers
│   ├── glue_visual_job_diagram.png
│   └── job_script_export.json    # Exported ETL job definition template
├── output/
│   └── run-*.parquet            # Sample output file
└── README.md                    # This file
```

## 🚀 Manual Setup in AWS Glue (Simplilearn Account)

1. **Upload data to S3**:

   * Create bucket `etl-cep-01`
   * Create subfolders `transaction-files/` and `product-files/`
   * Upload `transactions.csv` and `product details.csv` from the `data/` folder

2. **Set up AWS Glue**:

   * Create database: `abc-retail`
   * Create two CSV classifiers:

     * `txnClass` for transactions
     * `cust_classifier` for product details
   * Create IAM role `glue-role` with `AdministratorAccess`

3. **Configure Crawlers**:

   * **Crawler** `retail-crawl-txn` → Path `transaction-files/` → Classifier `txnClass`
   * **Crawler** `retail-crawl-product` → Path `product-files/` → Classifier `cust_classifier`

4. **Build Visual ETL Job**:

   * Add Glue Data Catalog nodes for both tables
   * **Join** node (Inner join on `Product ID`)
   * **Drop Fields** (drop duplicate `Product ID`)
   * **Regex Extractor** (`Sales` → `NetSales`, regex `\d+(\.\d+)?`)
   * **Aggregate** (group by `Product Category`, `Ship Mode`; avg of `NetSales`)
   * **Amazon S3** target (bucket `etl-cep-output-01`, format Parquet, compression Snappy)

5. **Run the Job** and verify output in S3:

   * Output file: `run-*.parquet`
   * Use S3 Select to query:

     ```sql
     SELECT * FROM s3object
     ```

## 📖 Additional Documentation

* See [etl/glue\_crawlers\_setup.md](etl/glue_crawlers_setup.md) for detailed manual setup steps.
* See `etl/glue_visual_job_diagram.png` for the ETL flow diagram.

## 📝 Contributing

Feel free to open issues or pull requests to improve data variety, add tests, or enhance documentation.

## 📜 License

MIT License — see [LICENSE](LICENSE).

