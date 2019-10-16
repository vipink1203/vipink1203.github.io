---
layout: post
title:  "List The Current PHP Handler - cPanel"
date:   2019-10-16 10:55:40 +0530
categories: cPanel
---

A PHP handler is a type of Apache module that contains libraries that the Apache webserver uses to interpret and run PHP code. Types of PHP handlers available in cPanel servers are CGI, DSO, suPHP, & FastCGI.

In this tutorial, we will see how to list the current working PHP handler using command line.

First ssh into the server as the root user. Then run the command below,
{% highlight ruby %}
/usr/local/cpanel/bin/rebuild_phpconf --current
{% endhighlight %}

### Example:
{% highlight ruby %}
root@home[~]# /usr/local/cpanel/bin/rebuild_phpconf --current
Available handlers: suphp dso cgi none
DEFAULT PHP: 5
PHP4 SAPI: none
PHP5 SAPI: suphp
SUEXEC: enabled
RUID2: not installed
{% endhighlight %}

We can also list the available PHP handlers using the same command,

{% highlight ruby %}
/usr/local/cpanel/bin/rebuild_phpconf --available
{% endhighlight %}

### Example:
{% highlight ruby %}
root@home [~]# /usr/local/cpanel/bin/rebuild_phpconf --available
Available handlers: suphp dso cgi none
PHP4 SAPI: not installed
PHP5 SAPI: cgi-fcgi
SUEXEC: available
RUID2: not available
{% endhighlight %}

In the next tutorial, we will see how to change the PHP handler in cpanel server and will use a script to fix permissions for all the user accounts.

Once this script is executed after changing the PHP handler you will never run into WordPress plugin or theme installation errors.

