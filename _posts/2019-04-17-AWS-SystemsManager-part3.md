---
layout: post
title:  "Parameter Store - AWS Systems Manager Part-3"
date:   2020-04-17 2:15:12 +0530
categories: AWS
---

This part is all about AWS SSM CLI and how we can create a parameter. Let's get straight down to business. 

This part does not cover aws cli configuration. Please refer this [link](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-configure.html) to set it up.



#### Using the AWS CLI to manage the parameters

_**Create a parameter**_

```
$ aws ssm put-parameter --name /dev/App1/DB_HOST --value dev-example-db-host.com --type String
```

**name** is your parameter path.

**value** is your hostname which is the secret value you want to avoid checking into Github.

**type** is the type of value you are storing in this parameter. In this case it is a simple string.

If you want to store a password which has to be secure and should not be stored as plain text. The command would be like,

```
$ aws ssm put-parameter --name /dev/App1/DB_PASS --value p@ssw0rd --type SecureString
```

Notice the --type is now a SecureString rather than a normal string.


_**Overwrite a parameter value**_

Everytime you create a new parameter your change version starts with 1. Something like this

```
{
    "Version": 1,
    "Tier": "Standard"
}
```

But what if you want to overwrite a new value?

```
$ aws ssm put-parameter --name /dev/App1/DB_PASS --value p@ssw0rd2 --type SecureString --overwrite
```

This will overwrite the old value and your new version will be,

```
{
    "Version": 2,
    "Tier": "Standard"
}
```


_**Querying parameters**_

We can query the parameters. We're going to use jq to filter the response.

```
$ aws ssm get-parameters-by-path --recursive --path /dev/App1/ | jq '.Parameters | map({Name,Value,Version})'
```

response:
```
[
  {
    "Name": "/dev/App1/DB_PASS",
    "Value": "AQICAHjH...",
    "Version": 2
  },
  {
    "Name": "/dev/App1/DB_HOST",
    "Value": "dev-example-db-host.com",
    "Version": 1
  }
]
```

Let's look at another command,

```
aws ssm get-parameter-history --name /dev/App1/DB_PASS --with-decryption | jq '.Parameters | map({Value,Version})'
```

here is the response for the above command

```
[
  {
    "Value": "p@ssw0rd",
    "Version": 1
  },
  {
    "Value": "p@ssw0rd2",
    "Version": 2
  }
]
```

Notice some change in the command from the previous one? "--with-decryption" option in the command while querying the parameter refers that the KMS key you used to encrypt the value you want the same key to decrypt and send it back in the response.

Now if you want just the value of that parameter and ignore all the json format, use the below command

```
aws ssm get-parameter --name /dev/App1/DB_HOST --region us-east-1| jq -r ".Parameter.Value")
```

**Output:**
```
dev-example-db-host.com
```


**Final command to add a parameter with all details**
```
aws --region us-east-1 ssm put-parameter --name /dev/App1/DB_HOST \
--value dev-example-db-host.com \
--type String \
--tags '[{"Key":"env","Value":"dev"},{"Key":"group","Value":"vip"}]' \
--description "Airflow Github OAuth Client Secret"
```

Our ultiamate goal now is to add all these parameter values to our configuration file. Check out [part-4]().