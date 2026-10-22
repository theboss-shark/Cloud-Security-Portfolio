
# AWS Cloud Security Project 01 — Secure EC2, S3 & IAM

**Focus:** AWS Cloud Security | IAM | Least Privilege | S3 Security

## Project Overview

This hands-on project demonstrates how an Amazon EC2 Linux instance accesses a private Amazon S3 bucket through an attached IAM role and a custom permissions policy.

The project focuses on role-based authentication, resource-scoped permissions, secure object storage, and verification of allowed and denied operations.

## Objectives

- Configure an EC2 Linux instance with an IAM instance role.
- Secure an S3 bucket using Block Public Access.
- Apply a custom least-privilege IAM policy.
- Verify the active AWS identity using AWS STS.
- Validate S3 listing, uploading, downloading, and denied deletion.
- Document security configurations and test evidence.

## Architecture

EC2 Linux → IAM Instance Role → Custom IAM Policy → S3 Bucket

The instance uses temporary credentials provided through its attached role rather than hardcoded AWS access keys.


## AWS Services

| Service | Purpose |
|---|---|
| Amazon EC2 | Linux workload |
| Amazon S3 | Object storage |
| AWS IAM | Roles, trust policies and permissions |
| AWS STS | Identity verification |
| AWS CLI | Access and validation tests |
| AWS CloudTrail | API activity auditing, where configured |

## Security Controls

- Role-based access without hardcoded credentials.
- S3 permissions scoped to the intended bucket and objects.
- Block Public Access enabled.
- Object deletion excluded from the custom role policy.
- Allowed and denied operations tested.
- CloudTrail S3 data events configured for auditing, if verified.

## Implementation

1. Create the S3 bucket and configure security settings.
2. Create an IAM role trusted by EC2.
3. Attach the custom S3 permissions policy.
4. Attach the role to the EC2 instance.
5. Verify the identity with `aws sts get-caller-identity`.
6. Test S3 access through the AWS CLI.
7. Verify that object deletion is denied.
8. Capture screenshots and document results.

Policy files are available under `iam/`; test evidence is available under `evidence/`.

## Validation Results

| Test | Expected result |
|---|---|
| STS identity verification | EC2 assumed role returned |
| List intended S3 bucket | Allowed |
| Upload an object | Allowed |
| Download an object | Allowed |
| Delete an object | Denied |

These expected outcomes must match the final test results. See `tests/validation.md` for the recorded evidence.

## Repository Structure

- `iam/` — IAM permissions and trust policies
- `evidence/` — Sanitized screenshots
- `tests/` — Validation commands and outcomes

## Security Considerations

- Never commit credentials, private keys, tokens, or credential files.
- Keep S3 Block Public Access enabled.
- Apply least-privilege permissions.
- Review explicit denies, bucket policies and other applicable permission controls when troubleshooting.
- Redact account identifiers and public IP addresses from public evidence where appropriate.

## Cleanup

Remove test objects when no longer required. Terminate the EC2 instance and remove unused resources when the lab is complete. Empty and delete the S3 bucket only when its contents are no longer needed. Detach and delete unused IAM resources after checking their dependencies.

## Skills Demonstrated

Amazon EC2 · Amazon S3 · AWS IAM · IAM Roles · Least Privilege · AWS STS · AWS CLI · CloudTrail · Security Validation · Technical Documentation

## Author

Sana Ullah Qureshi

**Portfolio focus:** AWS Cloud Security and Secure Cloud Infrastructure
