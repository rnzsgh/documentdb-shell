# Amazon DocumentDB Shell

The following are instructions to install the v3.6 mongo shell for use with [Amazon DocumentDB (with MongoDB compatibility)](https://aws.amazon.com/documentdb/) on Amazon Linux 2. For more detailed information, see the [official docs](https://docs.aws.amazon.com/documentdb/latest/developerguide/getting-started.connect.html).

# Configure yum

Create a */etc/yum.repos.d/mongodb-org-3.6.repo* file with the following contents (requires sudo access):

```
[mongodb-org-3.6]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/amazon/2013.03/mongodb-org/3.6/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.6.asc
```

# Install

Run the following command to install the shell:

```
sudo yum -y install mongodb-org-shell
```

# Pull the certificate

For SSL access, download the AWS CA bundle by running:

```
curl -o rds-combined-ca-bundle.pem https://s3.amazonaws.com/rds-downloads/rds-combined-ca-bundle.pem
```

# Connect

Go to the [Amazon DocumentDB (with MongoDB compatibility)](https://console.aws.amazon.com/docdb/home#clusters) section of the console, click on your cluster and get the connection information. Then, you will execute something similar to:

```
mongo --ssl --host YOUR_HOSTNAME_PREFIX.docdb.amazonaws.com:27017 \
  --sslCAFile rds-combined-ca-bundle.pem \
  --username MY_USERNAME \
  --password MY_PASSWORD

```

# Note

DocumentDB does not appear to currently support public endpoints (which is good), so you must connect from an EC2 instance located in the same VPC.


