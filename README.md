# Projet-Cloud
Auteurs : Elios, Tom, Joey

# Cloud Data Management Project

This project consists of a series of Java classes that interact with Amazon Web Services (AWS), particularly Amazon EC2 and S3, to manage cloud resources and process sales data. The main tasks include managing files on AWS S3 and processing CSV sales data for analysis.

## Overview

### Main Components:
1. **S3 Interaction**: Upload, download, list, and delete files from an S3 bucket.
2. **Data Processing**: Process CSV files to calculate profits and consolidate sales data.
3. **EC2 Interaction**: Start, stop, and manage EC2 instances on AWS.

### Technologies Used:
- AWS SDK for Java (`software.amazon.awssdk`)
- File I/O in Java
- CSV processing
- EC2 and S3 management via AWS SDK

## Class Breakdown

### `Client.java`

This class handles the following:
- Uploads a file to an AWS S3 bucket.
- Checks if the bucket exists; if not, it creates the bucket.
- Uses the AWS SDK to interact with S3, uploading files in binary form.

#### Key Methods:
- `main()`: The main function that builds the S3 client and uploads a file to the specified S3 bucket.

# Java Classes Overview

## Consolidator.java
This class consolidates data from multiple CSV files:

- **Reads sales data files from a specific directory.**
- **Sorts and aggregates store sales data.**
- **Writes the consolidated data to new CSV files.**

### Key Methods:
- `ReadFile()`: Reads CSV files and processes the sales data for stores and products.
- `WriteStores()`: Writes the sorted store data to a file.
- `WriteProducts()`: Writes the product data to a file.
- `SortStores()`: Sorts stores by their profit and writes the result.

---

## InfoProduct.java
This class represents a product's sales data:

- **Stores product quantity, price, and total profit.**
- **Includes methods for adding sales data and retrieving product information.**

---

## Main.java
This class automates the data processing and consolidation:

- **Scans for CSV files in a specified directory.**
- **Invokes Worker to process each file.**
- **Calls Consolidator to aggregate the results and save them in new CSV files.**

---

## Worker.java
This class processes individual CSV files:

- **Reads sales data for a specific store.**
- **Calculates the total profit for the store.**
- **Aggregates product sales information into a map.**
- **Writes the processed data back to a CSV file.**

---

## EC2 Management Classes
- **CreateEC2.java**: Creates a new EC2 instance with a specified AMI ID, instance type, and key pair. Tags the instance with a custom name.
- **StartStopEC2.java**: Starts or stops an EC2 instance based on its current state.

---

## S3 File Management Classes
- **S3ListBuckets.java**: Lists all the S3 buckets in the region.
- **S3RetrieveFile.java**: Downloads a file from a specified S3 bucket and deletes it after retrieval.
- **S3UploadFile.java**: Uploads a file to an S3 bucket. It also checks if the bucket exists before uploading.

---

## Workflow

### Uploading Data to S3
The **Client** class uploads CSV files containing sales data to an S3 bucket. The files are stored as binary data using the AWS SDK.

### Processing Sales Data
The **Main** class scans the sales data directory, processes each CSV file with **Worker**, and consolidates the results with **Consolidator**. The output is stored in the result directory.

### EC2 Instance Management
The **CreateEC2** and **StartStopEC2** classes manage EC2 instances by starting, stopping, or tagging instances based on the user’s input.

---

## Example Usage

### Uploading a file to S3
Run the Client class with the following arguments:

```bash
java Client 21112023 C:/path/to/data/01-10-2022-store3.csv

- `getObjectFile(String filePath)`: Reads the file from the given path and returns the content as a byte array for uploading.

```java
S3Client s3 = S3Client.builder().region(region).build();
PutObjectRequest putOb = PutObjectRequest.builder().bucket(bucketName).key(filename).build();
s3.putObject(putOb, RequestBody.fromBytes(getObjectFile(path + File.separator + filename)));
