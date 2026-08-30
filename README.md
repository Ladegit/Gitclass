# Data Engineering Fundamentals Assignment
## 1. A diagram of the conceptual pipeline for a telecom company called Beejan Technologies

<img width="1882" height="832" alt="Beejan Technologies Data Pipeline" src="https://github.com/user-attachments/assets/c6475811-550f-4c11-82e0-e810c10e24b2" />

## 2. A written explanation covering 
a. Design choices
b. Assumptions/thought process
c. Challenges/unknown
d. Any other information

## Answer
# Data Pipeline Design – Justification and Assumptions
# 1. Design Rationale
Based on my understanding of the telecom environment, I designed the pipeline to handle data from different sources such as network systems, CDRs, CRM, billing, digital channels, and enterprise applications.
My main consideration was that different data sources have different data volumes, frequencies, and business requirements. So, I did not use a single ingestion approach for all sources.
I adopted a hybrid batch-and-streaming architecture. Time-sensitive data such as network alarms, network telemetry, USSD transactions, and application events can be handled through streaming or near-real-time ingestion. Other data such as CDRs, billing, CRM, finance, and roaming data can be processed using batch or micro-batch pipelines where real-time processing may not be necessary.
This approach should help balance performance, scalability, complexity, and cost.
# 2. Storage and Processing
I considered a Data Lake/Lakehouse as the main storage layer because telecom companies can generate very large volumes of structured and semi-structured data. I used the Bronze, Silver, and Gold concept:
•	Bronze: Raw data retained close to its original format for traceability and reprocessing.
•	Silver: Cleaned, validated, standardized, and enriched data.
•	Gold: Business-ready data for reporting, analytics, and AI/ML.
For large analytical datasets, I assumed the use of formats such as Parquet because of their suitability for large-scale analytical workloads. For processing, I considered tools such as Spark/Databricks for large-scale batch and streaming transformations, while SQL/ETL tools can be used where appropriate.
# 3. Data Serving
I separated data storage from data serving. The storage layer focuses on where the data is kept, while the serving layer focuses on how the processed data is made available to consumers. Depending on the use case, data could be served through:
•	Data warehouses/data marts for BI and reporting.
•	Real-time analytical stores for operational dashboards.
•	APIs for application integration.
•	Curated datasets/features for AI and ML.
This provides flexibility because different consumers have different data access and latency requirements.
# 4. DataOps and Monitoring
I included DataOps because the pipeline needs to be reliable and maintainable after deployment.
The approach includes:
•	Git and version control.
•	CI/CD for pipeline deployment.
•	Automated data-quality checks.
•	Pipeline monitoring, logging, and alerting.
•	Data lineage and metadata.
•	Separate Development, UAT, and Production environments.
For example, if the number of CDR records received drops unexpectedly, a data-quality check should detect the issue and trigger an alert before incomplete data reaches the reporting layer.
# 5. Key Assumptions
Since detailed information about the customer's environment was not available, I made the following assumptions:
•	Telecom data volumes can be very large, particularly CDRs, network telemetry, and usage data.
•	Network data is generated more frequently than most enterprise data.
•	Network alarms and some transactions may require near-real-time processing.
•	Finance and other enterprise data can generally be processed periodically.
•	Data may come through APIs, databases, CSV, JSON, XML, logs, or SFTP.
•	Historical data will be required for reporting, trend analysis, and AI/ML.
•	The solution should be scalable to accommodate future data growth.
# 6. Key Challenges and Unknowns
The main information I would need to confirm before finalizing the design includes:
1.	Data Volume: How much data does each source generate daily, and what are the peak volumes?
2.	Latency: Which data requires real-time processing and how quickly does the business need it?
3.	Source Capabilities: Do the systems support APIs, CDC, database connections, files, or streaming?
4.	Data Quality: What existing issues exist with duplicates, missing values, inconsistent formats, or identifiers?
5.	Retention: How long does each type of data need to be stored?
6.	Existing Technology: What platforms, tools, and licenses does the customer already have?
7.	Security: What data privacy, access control, and regulatory requirements apply?
8.	Business Use Cases: Is the primary requirement BI, real-time monitoring, AI/ML, fraud detection, customer analytics, or a combination?
# 7. Overall Thought Process
The key questions guiding my design were:
How much data is generated? → How quickly is it generated? → How quickly does the business need it? → How should it be processed and stored? → How will it be consumed? → How will we monitor and maintain it?
I therefore see the proposed architecture as a conceptual design that provides a foundation for the solution. Further customer discovery would be required to validate the assumptions, determine the appropriate technologies, and properly size the final architecture.

