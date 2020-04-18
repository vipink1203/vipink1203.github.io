---
layout: post
title:  "AWS SSM Parameter Store Basics Part-1"
date:   2020-04-17 1:40:12 +0530
categories: AWS
---

We already have a lot of online posts covering this topic but I wanted to write this in my own words just for the future reference. Goal of this post is to get down to AWS SSM - parameter store cli basics and then how we can populate a config file in EC2 instance with the values from the parameter store. 

This would be very useful when it comes to people/organisation who doesn't want to store their senstive information in any version control. 

### What is AWS SSM?

AWS Systems Manager in simple words is a service which allows you to view and control your infrastructure in AWS. You can find it's capabilities in this [link](https://docs.aws.amazon.com/systems-manager/latest/userguide/features.html).

### What is Parameter Store?

Parameter Store is a service which helps you arrange your data in a systematic hierarchical format for better reference. Data can be of any type like Passwords, Keys, URLs or Strings. Data can be stored as encrypted or as plain text. Storage is done in Key-Value Format. Parameter store comes integrated with AWS KMS.


Before we dive into CLI commands, I would recommend to go to the Systems Manager service in AWS portal and checkout parameter store. You will get a clear idea on how it works.

### Data Hierarchy

So let me start with an example/senario. Your boss calls you one day and he wants you to remove all the Database credentials from the Github repositories. You might say, all our repositories are private and no one can see except the organisation members and contributors. Good point, huh?

No, it seems like a good point to make but it's not a good practice to keep the senstive information in the repositories in plain text. Why does other teams in the organisation have to know other application credentials?

AWS SSM Parameter store comes to rescue. As said earlier you can store or arrange your data in a systematic hierarchical format for better reference. Imagine you have 2 applications App1 and App2, both have DB credentials you want to store to parameter store. Now what's the best way?

#### App1 Hierarchy
```
/dev/App1/DB_HOST
/dev/App1/DB_USER
/dev/App1/DB_PASS
/dev/App1/DB_NAME

/qa/App1/DB_HOST
/qa/App1/DB_USER
/qa/App1/DB_PASS
/qa/App1/DB_NAME

/prod/App1/DB_HOST
/prod/App1/DB_USER
/prod/App1/DB_PASS
/prod/App1/DB_NAME
```

#### App2 Hierarchy
```
/dev/App2/DB_HOST
/dev/App2/DB_USER
/dev/App2/DB_PASS
/dev/App2/DB_NAME

/qa/App2/DB_HOST
/qa/App2/DB_USER
/qa/App2/DB_PASS
/qa/App2/DB_NAME

/prod/App2/DB_HOST
/prod/App2/DB_USER
/prod/App2/DB_PASS
/prod/App2/DB_NAME
```

The format is simple - /{ENV}/{APP-NAME}/{PARAMETER}. But of course you can store any way you like. Having a proper nomenclature for naming each parameter would be easy when you have hundreds or thousands of parameters.

In the part-2, we will see how we can add a new parameter and it's value using AWS CLI.



