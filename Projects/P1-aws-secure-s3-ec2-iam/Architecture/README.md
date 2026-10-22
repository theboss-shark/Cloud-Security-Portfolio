

# Architecture and Design

This directory contains the architecture diagram and design documentation for the Secure EC2-to-S3 Access project.

The diagram illustrates how an Amazon EC2 Linux instance uses an attached IAM role and a least-privilege permissions policy to access a private Amazon S3 bucket.

## Architecture Components

- **Amazon EC2:** Executes AWS CLI operations.
- **IAM Instance Role:** Provides temporary credentials to the instance.
- **IAM Permissions Policy:** Restricts access to the required S3 actions and resources.
- **Amazon S3:** Stores objects with Block Public Access enabled.
- **AWS CloudTrail:** Records configured S3 data events for audit and investigation.

## Design Principle

Apply least privilege, avoid hardcoded AWS credentials, and keep S3 objects private.

## Files

- `AWS EC2 to S3 Security Flow Diagram.png` — Visual representation of the solution.

The diagram describes the intended design; refer to the project's evidence and validation results for verified behavior.
