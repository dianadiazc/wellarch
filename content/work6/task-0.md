+++ 
title = "Task 0: Cost & Usage Report Configuration" 
chapter = false 
weight = 1 
+++

{{% notice info %}}
There are no activities you would need to perform in this task 0. In this task we will describe the Lab 5 environment you will be working on in the Tasks 1, 2 and 3
{{% /notice %}}

In this Lab 5 you will create cost analysis based on the reports generated by the **AWS Cost and Usage Report** service. These reports contains the most comprehensive set of AWS cost and usage data available, including additional metadata about AWS services, pricing, Reserved Instances, and Savings Plans.

For a detailed walkthrough of how to create a Cost and Usage Report please visit: https://docs.aws.amazon.com/cur/latest/userguide/cur-create.html

As part of this Lab 5 environment, we have automated some tasks such as:

* Upload sample report from a central repo to an S3 bucket

* Create a Glue Database

* Run a Glue Crawler to create a Glue Table, which will be used as data source for QuickSight

* Create Athena Data Source which will be used by Quicksight as the dataset for analyses


This is the Lab 5 environment diagram:

<img src="../images/wa-lab-task-0.png" alt="drawing" width="600"/>

In this Lab we are using **Cost and Usage Report** sample data.

A Cost and Usage Report includes:

* Account identifiers

* Invoice and Bill Information

* Usage Amount and Unit

* Rates and Cost

* Product Attributes (e.g., instance type, operating system, and region)

* Pricing Attributes (e.g., offer types, and lease lengths)

* Reservation identifiers and related details (for reserved instances only)

When you create a report, you have the option to define the data granularity (hourly, daily or monthly), which format the report files will have (text/csv or Parquet), compression type (Parquet, ZIP or GZIP) and optionally and integration with Analytics services to analyze the **Cost and Usage Report** data.

Supported integrations are:

* Amazon Athena

* Amazon Redshift

* Amazon QuickSight

If you would like to analize the data in your own environment, you can optionally download the sample file we will be using in the next Lab tasks

{{%attachments title="Download Sample Report" pattern=".*(parquet)"/%}}