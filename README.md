# AWS-Maths-Project

# 🚀 AWS Power of Math - Serverless Web Application

A fully serverless web application built on AWS that calculates the power of a number using **AWS Lambda**, exposes the functionality through **Amazon API Gateway**, stores calculation history in **Amazon DynamoDB**, and provides a simple **HTML frontend** for user interaction.

---

# 📖 Project Overview

This project demonstrates how multiple AWS services can work together to build a scalable, secure, and serverless application.

A user enters:

- Base Number
- Exponent

The request is sent to AWS Lambda through API Gateway.

Lambda:

- Calculates the result
- Saves the result in DynamoDB
- Returns the answer to the webpage

No EC2 instances are required.

---

# 🏗 Architecture

```
                   User
                     │
                     ▼
              HTML Frontend
                     │
                     ▼
            Amazon API Gateway
                     │
                     ▼
          AWS Lambda (Python 3.x)
                     │
                     ▼
             Amazon DynamoDB
```

---

# ⚙ AWS Services Used

| Service | Purpose |
|----------|----------|
| Amazon API Gateway | Receives HTTP requests |
| AWS Lambda | Performs calculation |
| Amazon DynamoDB | Stores calculation history |
| IAM | Provides secure permissions |
| HTML | User Interface |

---

# 📂 Repository Structure

```
AWS-Maths-Project/

│── index.html
│── index.zip
│── PowerOfMathFunction - ORIGINAL.txt
│── PowerOfMathFunction - Lambda-FINAL.txt
│── Execution Role Policy JSON.txt
│── README.md
```

---

# 🚀 Features

- Fully Serverless
- No Infrastructure Management
- Auto Scaling
- Secure IAM Permissions
- DynamoDB Integration
- API Gateway Integration
- Lightweight HTML Frontend

---

# 🛠 Prerequisites

Before deploying, make sure you have:

- AWS Account
- IAM User with AdministratorAccess (or equivalent)
- AWS Region selected
- Python 3.x Runtime
- Modern Web Browser

---

# 🚀 Deployment Guide

## Step 1 — Create DynamoDB Table

Open AWS Console

Navigate to

```
DynamoDB
```

Click

```
Create Table
```

Configuration

| Setting | Value |
|----------|-------|
| Table Name | PowerOfMathDatabase |
| Partition Key | ID (String) |

Leave remaining settings as default.

Click

```
Create Table
```

---

## Step 2 — Create IAM Role

Navigate to

```
IAM → Roles
```

Create a new role for

```
Lambda
```

Attach the execution role policy after replacing:

```
YOUR-TABLE-ARN
```

with your actual DynamoDB table ARN.

Example ARN

```
arn:aws:dynamodb:ap-south-1:123456789012:table/PowerOfMathDatabase
```

Also attach the managed policy:

```
AWSLambdaBasicExecutionRole
```

---

## Step 3 — Create Lambda Function

Go to

```
AWS Lambda
```

Click

```
Create Function
```

Configuration

Name

```
PowerOfMathFunction
```

Runtime

```
Python 3.13 (or latest available)
```

Execution Role

```
Use Existing Role
```

Select the role created earlier.

---

## Step 4 — Upload Lambda Code

Replace the default code with the contents of:

```
PowerOfMathFunction - Lambda-FINAL.txt
```

Deploy the function.

---

## Step 5 — Test Lambda

Create a test event.

Example

```json
{
  "base": 5,
  "exponent": 3
}
```

Expected Output

```json
{
  "statusCode": 200,
  "body": "Your result is 125.0"
}
```

Verify that a new item appears in the DynamoDB table.

---

## Step 6 — Create API Gateway

Navigate to

```
Amazon API Gateway
```

Create a

```
REST API
```

Create Resource

```
/power
```

Create Method

```
POST
```

Integration Type

```
Lambda Function
```

Choose

```
PowerOfMathFunction
```

Enable

```
Lambda Proxy Integration
```

Deploy API

Example Stage

```
prod
```

Your endpoint will look similar to

```
https://abcd1234.execute-api.ap-south-1.amazonaws.com/prod/power
```

---

## Step 7 — Enable CORS

Select the API Resource.

Choose

```
Enable CORS
```

Allow

- POST
- OPTIONS

Deploy the API again.

---

## Step 8 — Update HTML

Open

```
index.html
```

Replace the API URL with your deployed API Gateway endpoint.

Example

```javascript
const apiUrl = "https://abcd1234.execute-api.ap-south-1.amazonaws.com/prod/power";
```

Save the file.

---

## Step 9 — Host the Website

You can host the frontend using:

### Option 1 (Recommended)

Amazon S3 Static Website Hosting

### Option 2

GitHub Pages

### Option 3

Apache

### Option 4

Nginx

---

# 🧪 Testing

Open the webpage.

Enter

Base

```
4
```

Exponent

```
5
```

Click

```
Calculate
```

Expected Output

```
1024
```

Verify the calculation history is stored in DynamoDB.

---

# 📊 Sample Request

```json
{
    "base":7,
    "exponent":2
}
```

Response

```json
{
    "statusCode":200,
    "body":"Your result is 49.0"
}
```

---

# 🔒 Security

This project follows AWS security best practices:

- IAM Least Privilege
- Lambda Execution Role
- No hardcoded AWS credentials
- API Gateway acts as the public entry point
- DynamoDB is not publicly accessible

---

# 📈 Future Enhancements

- Add user authentication with Amazon Cognito
- Display calculation history on the webpage
- Add input validation
- Improve UI using Bootstrap or React
- Add CloudWatch monitoring
- Implement CI/CD with GitHub Actions
- Provision infrastructure with AWS CloudFormation or Terraform

---

# 🧹 Clean Up

To avoid AWS charges, delete the following resources after testing:

- Lambda Function
- API Gateway
- DynamoDB Table
- IAM Role (if no longer needed)
- S3 Bucket (if created)

---

# 📚 Learning Outcomes

By completing this project, you will learn:

- Serverless Computing
- AWS Lambda
- Amazon API Gateway
- Amazon DynamoDB
- IAM Roles and Policies
- Python with Boto3
- REST APIs
- Cloud Security Best Practices

---

# 👨‍💻 Author

**Anand Tiwari**

AWS Cloud | Linux | DevOps | Python | Serverless | Infrastructure Automation

---

## ⭐ If you found this project useful, please consider giving it a star!
