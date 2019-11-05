---
layout: post
title:  "Python Script to Decrypt Encrypted File With AWS KMS"
date:   2019-10-25 1:33:40 +0530
categories: scripting
---

In this post, you will learn how to encrypt an SSH private key using KMS and how to use Python to decrypt the encrypted SSH key.

This would be useful for the use cases such as when creating a Lambda function and you don't want to place the plain text SSH private key to do some operations on the server.


Let's begin..

## Step 1:

Create a KMS key in your AWS account. It's pretty easy and you can use this [AWS Documentation](https://docs.aws.amazon.com/kms/latest/developerguide/create-keys.html#create-keys-console) for reference.


## Step 2:

Now you can use the aws-cli to encrypt the SSH private key as shown below.

```Shell
    aws kms encrypt --key-id 7fmcesd6-c4ff-7b01-b11c-5h2e91h1b301 --plaintext fileb://privateKey.pem --output text --query CiphertextBlob | base64 --decode > EncryptedFile
```

After you run this command, the encrypted text is stored to **EncryptedFile** file

## Step 3:

You can find the python script [here](https://github.com/vipink1203/Python-Scripts/blob/master/kms-decrypt.py).

Place the EncryptedFile along with the python script and run it.

I used Python 3.5 version, didn't test with Python 2. Feel free to do so.

Will post another one where we will create a Lambda function to support this use case.