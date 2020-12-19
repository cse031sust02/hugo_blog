---
date: "2017-09-12T16:05:22+06:00"
title: "Getting started with AWS"
---

---

## What is AWS?

Amazon Web Services (AWS) is a secure cloud services platform. It provides a broad set of infrastructure services, such as computing power, storage options, networking and databases. Millions of customers use AWS cloud [products](https://aws.amazon.com/products/) and [solutions](https://aws.amazon.com/solutions/) to build sophisticated applications.

**source** : https://aws.amazon.com/what-is-aws/

---

## Getting Started

#### Create a New Account
Go to https://portal.aws.amazon.com/billing/signup#

#### Get Hands On
These [10-Minute Tutorials](https://aws.amazon.com/getting-started/tutorials/) are simple “Hello, World!” technical documents to help you get hands-on with AWS.

--- 

## Most Used Services

### Amazon EC2

Amazon Elastic Compute Cloud ([Amazon EC2]((https://aws.amazon.com/ec2))) is the Amazon Web Service to create and run **virtual machines** (instances) in the cloud.

There are several ways to get started with Amazon EC2. We can use the AWS Management Console, the AWS Command Line Tools (CLI), or AWS SDKs.

We can follow the offical docs to get started with EC2 :

- [Getting Started with Amazon EC2](https://aws.amazon.com/ec2/getting-started/)
- [Launch a Linux Virtual Machine](https://aws.amazon.com/getting-started/tutorials/launch-a-virtual-machine/)

### Amazon RDS

Amazon Relational Database Service (Amazon RDS) is a managed service that enables developers to set up, operate, and scale a relational database in the cloud. It also automates time-consuming database administration tasks such as backups, software patching, automatic failure detection, and recovery. 

Amazon RDS supports Amazon Aurora, MySQL, MariaDB, Oracle, SQL Server, and PostgreSQL database engines.

- [Getting Started with Amazon RDS](https://aws.amazon.com/rds/getting-started/)
- [Create and Connect to a MySQL Database](https://aws.amazon.com/getting-started/tutorials/create-mysql-db/)

### Amazon Lambda

AWS Lambda lets us run code without thinking about servers. We just need to write the code*  and upload it to Lambda. Lambda takes care of everything required to run and scale the code with high availability. It is also possible to automatically trigger that code from other AWS services or from any web or mobile app.

> *AWS Lambda supports Java, Node.js, C#, and Python code, with support for other languages coming in the future.

![Lambda_HowItWorks](https://d1.awsstatic.com/Test%20Images/MasonTests/Lambda_HowItWorks.662f209027a4fdfde72164fde6f01f51127e8c21.png)

Image Source : [AWS](https://aws.amazon.com/lambda/)

- [Getting Started With Amazon Lambda](https://aws.amazon.com/lambda/getting-started/)
- [Run a Serverless "Hello, World!"](https://aws.amazon.com/getting-started/tutorials/run-serverless-code/)

### Amazon S3

Amazon Simple Storage Service(S3) is a storage platform. The goal of S3 is to store and retrieve any amount of data from anywhere (i.e, web sites, mobile apps, corporate applications, IoT etc).

AWS provides developer tools and SDKs for [different programming languages and platforms](https://aws.amazon.com/s3/getting-started/#sdk) such as Java, PHP, NodeJs, .NET, Python and Ruby. Also, there is a [a web-based interface](https://docs.aws.amazon.com/AmazonS3/latest/gsg/SigningUpforS3.html) for accessing and managing Amazon S3 resources.

- [Getting Started with Amazon S3](https://aws.amazon.com/s3/getting-started/)
- [Store and Retrieve a File using Amazon S3](https://aws.amazon.com/getting-started/tutorials/backup-files-to-amazon-s3/)

---

There are many more cool services AWS provides. Sometimes it is little bit difficult to understand the purpose of the services from the name. I found this [post](https://www.expeditedssl.com/aws-in-plain-english) very helpful to get an basic idea about different services of AWS.