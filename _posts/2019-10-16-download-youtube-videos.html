---
layout: post
title:  "Download Videos From YouTube"
date:   2019-10-16 9:15:40 +0530
categories: scripting
---


I was searching for an easy way to download YouTube videos from the Linux command line and I found youtube-dl command but I had to download each video individually. Now, I wanted something that could download a list of videos. For that, I came up with a bash script that could take a file as input containing the video URLs.

First, let's get started with installing youtube-dl.

# STEP 1: INSTALLING YOUTUBE-DL

{% highlight ruby %}
> yum install -y youtube-dl
No package youtube-dl available.
Error: Nothing to do
{% endhighlight %}

If you get an error like above, use the below command.

{% highlight ruby %}
> wget https://yt-dl.org/downloads/latest/youtube-dl -O /usr/local/bin/youtube-dl
{% endhighlight %}

After downloading the script, set the executable permission.

{% highlight ruby %}
> chmod a+x /usr/local/bin/youtube-dl
{% endhighlight %}

Now, let's verify if the youtube-dl command works,

{% highlight ruby %}
> youtube-dl -h
{% endhighlight %}

If you get output from the above command, it's fine. Else, you have to copy/move the script file to /bin directory.

{% highlight ruby %}
> cp /usr/local/bin/youtube-dl /bin/
{% endhighlight %}

Verify again if the "youtube-dl -h" command works and hope it would work as it did for me.

# STEP 2: CREATE BASH SCRIPT

Now that we have installed the youtube-dl, let's create a bash script that will take input from a file.

{% highlight ruby %}
#!/bin/bash
while read videos
do
    youtube-dl $videos
done
{% endhighlight %}

Save the script. I saved it as "demo.sh".

That's it. Our script is ready now, but we are not finished yet.

# STEP 3: CREATE A FILE WITH VIDEO URLs
The final step would be creating a simple file that contains video URLs. Make sure each video URL is in separate lines.

{% highlight ruby %}
video1 url
video2 url
video3 url
{% endhighlight %}

Save the file with any name you want. For example, I saved the file as a video list.

# STEP 4: EXECUTE THE SCRIPT
Finally, we are ready to download the list of videos in single command from youtube.

{% highlight ruby %}
./demo < videolist
{% endhighlight %}

./demo -- This is our script

videolist -- Our file containing list of videos

< -- This is STDIN i.e we are giving the file as input for our script.

That's it.. :)