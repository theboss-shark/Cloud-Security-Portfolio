# Project 1: Secure AWS EC2-to-S3 Access Using IAM

## Overview

This project demonstrates how to securely grant an Amazon EC2 instance access to a private Amazon S3 bucket using an IAM role and least-privilege permissions.

Instead of storing long-term AWS access keys on the instance, the EC2 instance obtains temporary credentials through its attached IAM role. Permissions are restricted to the specific S3 bucket and the required actions.

## Architecture

**EC2 (Ubuntu Linux) → IAM Instance Role → Least-Privilege IAM Policy → Private S3 Bucket**

The solution uses role-based access, private S3 storage, and permission testing to demonstrate secure cloud access.

See the [Architecture folder](Architecture/README.md) for architecture documentation and the diagram.

## AWS Services

- **Amazon EC2:** Ubuntu Linux virtual machine.
- **Amazon S3:** Private object storage.
- **AWS IAM:** Instance role, trust policy, and scoped permissions.
- **AWS STS:** Verification of the temporary assumed-role identity.
- **AWS CloudTrail:** Audit evidence, where the relevant data events are configured and verified.

## Security Controls

- S3 Block Public Access enabled.
- IAM role attached to the EC2 instance.
- No long-term AWS access keys stored on the instance.
- Permissions limited to the project bucket.
- `s3:ListBucket`, `s3:GetObject`, and `s3:PutObject` allowed.
- Object deletion not permitted by the project policy.
- Access tested through successful and unauthorized operations.

## Project Structure

| Folder | Contents |
|---|---|
| [Architecture](Architecture/README.md) | Architecture diagram and design explanation |
| [EC2](EC2/README.md) | EC2 configuration and security details |
| [Evidence](Evidence/README.md) | Screenshots supporting configuration and test results |
| [iam](iam/README.md) | IAM role, policy, and identity-verification evidence |
| [Test](Test/validation.md) | Validation commands, expected results, and troubleshooting |

## Validation Results

| Test | Expected result |
|---|---|
| Verify identity with `aws sts get-caller-identity` | Assumed IAM role is returned |
| List the project bucket with `aws s3 ls s3://p1-ec2-s3` | Allowed |
| Download an authorized object | Allowed |
| Upload an object | Allowed |
| Delete an object | Denied by the project IAM policy |

These results describe the intended lab behavior. Refer to the evidence and validation notes for the actual tests performed.

## Skills Demonstrated

- AWS IAM roles and trust relationships
- Least-privilege access policies
- EC2 instance security
- S3 bucket and object permissions
- Temporary credentials and AWS STS
- AWS CLI validation
- CloudTrail audit concepts
- Security documentation and evidence collection

## Cleanup

To avoid ongoing AWS charges, remove the lab resources when they are no longer required. Review dependencies before deleting the EC2 instance, IAM resources, S3 bucket contents, or CloudTrail resources created for this project.

## Disclaimer

This project was created for educational purposes in an AWS environment under my control. It demonstrates foundational cloud security practices and does not represent a production security audit.

## Author

**Cloud Security Portfolio — AWS Project 1**

GitHub: [@theboss-shark](https://github.com/theboss-shark)
