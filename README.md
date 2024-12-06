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
- `getObjectFile(String filePath)`: Reads the file from the given path and returns the content as a byte array for uploading.

```java
S3Client s3 = S3Client.builder().region(region).build();
PutObjectRequest putOb = PutObjectRequest.builder().bucket(bucketName).key(filename).build();
s3.putObject(putOb, RequestBody.fromBytes(getObjectFile(path + File.separator + filename)));
