---
layout: post
title:  "Parameter Store - AWS Systems Manager Part-2"
date:   2020-04-17 2:15:12 +0530
categories: AWS
---

In [part-1](https://www.vipinkumar.me/aws/2020/04/16/AWS-SystemsManager-part1.html) we looked at what is parameter store and how you can arrange your data. In part-3, we will go through some basic CLI commands with which you can create new parameters.

First let's understand all the details within the parameter store, in that way it will be very easy for us to write the command without even looking at reference guides or cheetsheet.

### Parameter Store Details

###### Name, Description and Tier

![Name](/img/posts/parameterstore/parameterstore1.png =250x)

**Name** is where you enter your path. Remember in the previous post we saw the App hierarchy? Something like this -

```
/dev/App1/DB_HOST
```

So this is your parameter path and for the DB_HOST in this path is your key to which you will later add your value, in this case it is database hostname.

**Description** is where you enter a proper comment to identify what this parameter is used for.

**Tier** is something you want to choose carefully. It is nothing but the limit set as how many parameters you can use. The description is already self explanatory, but remember if you go for advanced option later you cannot change it back to standard the option.

![Type](/img/posts/parameterstore/parameterstore2.png)

**Type** is nothing but what type of value are you storing for this key. It can be a string, stringList or a secure string.
If you use a secure string, you will have to select a KMS key which should have proper policy attached to encrypt and decrypt the value of your key.

**Value** is where you will write your database hostname in this case since we are talking about the **DB_HOST** key.

![Tags](/img/posts/parameterstore/parameterstore3.png)

**Tags** - This is optional but it is always a best practice to add tags to all your resources.

That's all... Now let's cover the CLI part - [PART-3]()