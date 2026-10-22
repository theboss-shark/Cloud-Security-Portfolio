

# AWS Identity and Access Management

This directory contains the IAM configuration used to authorize the EC2 instance to access the project's S3 bucket.

## Components

- **Permissions Policy:** Defines the allowed S3 actions and resource ARNs.
- **Trust Policy:** Allows the EC2 service to assume the IAM role.

## Access-Control Design

The custom permissions policy allows:

- `s3:ListBucket` on the intended bucket.
- `s3:GetObject` on objects within that bucket.
- `s3:PutObject` on objects within that bucket.

The policy does not grant `s3:DeleteObject`.

## Security Objective

Demonstrate resource-scoped permissions and least-privilege access without embedding long-lived AWS credentials in the workload.

## Files

- `s3-access-policy.json` — Custom S3 permissions policy.
- `ec2-trust-policy.json` — EC2 role trust policy.

The files should match the final policy configuration actually deployed in AWS.
