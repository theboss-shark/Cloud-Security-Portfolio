

# Validation and Test Results

## Environment
- AWS Region: us-east-1
- Compute: Amazon EC2 Linux
- Storage: Amazon S3
- Authentication: EC2 instance IAM role

## Test 1 — Identity Verification
Command: `aws sts get-caller-identity`
Expected: The EC2 assumed-role identity is returned.
Result: Passed (see evidence/04-identity-verification.png).

## Test 2 — S3 Listing and Download
Commands:
- `aws s3 ls s3://p1-ec2-s3/`
- `aws s3 cp s3://p1-ec2-s3/Cloud-Security-Lab.txt downloaded.txt`

Expected: Listing and download succeed.
Result: Passed (see evidence/05-s3-access-success.png).

## Test 3 — Upload
Command:
`aws s3 cp Cloud-Security-Lab.txt s3://p1-ec2-s3/Cloud-Security-Lab.txt`

Expected: Upload succeeds.
Result: Capture and record the successful upload.

## Test 4 — Unauthorized Deletion
Command:
`aws s3 rm s3://p1-ec2-s3/Cloud-Security-Lab.txt`

Expected: AccessDenied because the role lacks s3:DeleteObject.
Result: Denied (see evidence/06-unauthorized-action-denied.png).
