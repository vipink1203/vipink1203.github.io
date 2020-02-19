---
layout: post
title:  "Databricks-JupyterLab Integration"
date:   2020-02-19 7:11:40 +0530
categories: Databricks
---

This post will help you to connect Jupyter notebook with Databricks and run spark jobs remotely on Databricks.

## Prerequisites:

1. MAC or Linux machine
2. Recent version of Annaconda installed, greater than 4.7.5
3. Databricks-cli installed on the machine. Follow https://docs.databricks.com/dev-tools/cli/index.html to install
4. SSH key generated from ssh-keygen -t rsa (Databricks cli profile name and ssh key name should be same). 

> Note: the ssh key name should be id_${profile} where ${profile} is the profile name(databricks) stored in ~/.databrickscfg file. The ssh key should be present in ~/.ssh/id_${profile}

**Ex: Profile name in databricks config file:**

```
[databricks]
host = https://dbc-XXXXXX-YYYZ.cloud.databricks.com
token = {token}
```

The ssh key generated should have path of **~/.ssh/id_databricks** and public key must be **~/.ssh/id_databricks.pub**

## Instructions:

1. Run conda create -n databricks python=3.7 to create a new conda environment
2. conda activate databricks for switching to the newly created environment
3. pip install --upgrade databrickslabs-jupyterlab==1.0.9 to install the pip package
4. databrickslabs-jupyterlab -b will initialize the jupyterlab environment
5. databrickslabs-jupyterlab ${profile} -k will create a jupyter kernel specification for databricks. 
6. databrickslabs-jupyterlab ${profile} -l will start the jupyter notebook server with the remote spark configuration
7. To use the remote spark connection, choose the remote spark version available from the list in jupyter notebook console.

```
from databrickslabs_jupyterlab.connect import dbcontext
dbcontext()
```

Run the above cell in Jupyter notebook to initialise the connection to the Databricks and it will prompt for databricks token. Use the token configured in the Databricks CLI to complete the connection and start running your notebook.