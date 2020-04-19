---
layout: post
title:  "Send Application Logs to AWS CloudWatch"
date:   2020-02-18 10:15:40 +0530
categories: AWS
---

I recently had a requirement where developers wanted to see the application logs in the CloudWatch instead of logging to the server. I came across this aws documentation which does the same stuff I needed.

[AWS Documentation](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/Install-CloudWatch-Agent.html)


#### STEP 1: Create An EC2 Instance

1. Create an EC2 instance and attach a role to it.
2. Attach **CloudWatchAgentServerPolicy** managed policy to that role.
3. Login to the instance.
4. Find the right agent link for your OS by visiting the [link](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/download-cloudwatch-agent-commandline.html)

#### STEP 2: Download the Cloudwatch Unified Agent

```shell
    # wget https://s3.amazonaws.com/amazoncloudwatch-agent/amazon_linux/amd64/latest/amazon-cloudwatch-agent.rpm
```
Now the rpm has been downloaded, install it with the command,

```shell
    # rpm -U ./amazon-cloudwatch-agent.rpm
```

#### STEP 3: Configure the Cloudwatch agent

1. Configure the Cloudwatch agent with the help of a setup wizard:

```shell
    # /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-config-wizard
```

Choose all the default option except don't install statd, collectd and Memory Utilization metric. Select Yes when asked if you want to monitor log files and enter the path to that specific log file.

Make sure the log group name is not generic. You can provide your application name. 

Example: **prod-appname-nodejs-logs**

#### STEP 4: Finishing Line

Start the agent by running the below command,

```shell
    # /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -a fetch-config -m ec2 -c file:/opt/aws/amazon-cloudwatch-agent/bin/config.json -s
```

You have successfully configured the cloudwatch logs for your application now.

