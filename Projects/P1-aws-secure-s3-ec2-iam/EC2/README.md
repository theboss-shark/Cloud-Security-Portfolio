

# Amazon EC2 Configuration

This directory documents the EC2 Linux instance used to demonstrate secure access to Amazon S3 through AWS IAM.

## Purpose

Configure a compute instance that obtains temporary AWS credentials through its attached IAM instance role rather than relying on hardcoded access keys.

## Configuration Evidence

- EC2 instance state and instance type.
- Attached IAM role.
- Instance identity verification using AWS STS.
- AWS CLI execution environment.

## Security Considerations

- Attach only the IAM role required by the workload.
- Restrict network access through appropriately configured security groups.
- Avoid storing long-lived AWS credentials on the instance.
- Verify the active identity before performing S3 operations.

See `../Evidence/` for screenshots and `../Tests/` for validation results.
