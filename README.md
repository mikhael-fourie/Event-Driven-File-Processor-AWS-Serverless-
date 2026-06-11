
S3 Event-Driven File Processor

A serverless, event-driven automation workflow built on AWS. Automatically 
reacts to file uploads in S3 — sending an email notification with file 
metadata and copying the file to a backup bucket, with no server management 
required.

---

## Architecture
S3 (PUT Object Event)
↓
AWS Lambda
↙     ↘
SNS Email   Backup S3 Bucket

---

## What it does

When a file is uploaded to the source S3 bucket, a Lambda function is 
triggered automatically. It:

- Sends an email notification via SNS containing the source bucket, 
  filename, file size, upload IP address, and event timestamp
- Copies the uploaded file to a designated backup S3 bucket
- Logs all activity to CloudWatch

---

## Services used

- **Amazon S3** — file storage and event trigger
- **AWS Lambda** — serverless event processing (Python, Boto3)
- **Amazon SNS** — email notifications
- **Amazon CloudWatch** — logging and monitoring

---

## Configuration

| Environment Variable | Description |
|---|---|
| `BACKUP_BUCKET_NAME` | Target backup S3 bucket |
| `SNS_TOPIC_ARN` | SNS topic ARN for email notifications |

---

## IAM permissions required

The Lambda execution role requires `sns:Publish`, 
`s3:GetObject`, `s3:PutObject`, and `s3:ListBucket`.

---

## Stack

AWS · Lambda · S3 · SNS · CloudWatch · Python · Boto3 · IAM
