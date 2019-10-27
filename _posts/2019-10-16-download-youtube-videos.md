---
layout: post
title:  "Download Videos From YouTube"
date:   2019-10-16 9:15:40 +0530
categories: scripting
background: '/img/posts/Youtube.png'
---

I was searching for an easy way to download YouTube videos from the Linux command line and I found youtube-dl command but I had to download each video individually. Now, I wanted something that could download a list of videos. For that, I came up with a bash script that could take a file as input containing the video URLs.

First, let's get started with installing youtube-dl.


#### STEP 1: INSTALLING YOUTUBE-DL

```shell
    # yum install -y youtube-dl 
    No package youtube-dl available
    Error: Nothing to do
```

If you get an error like above, use the below command.

```shell
    # wget https://yt-dl.org/downloads/latest/youtube-dl -O /usr/local/bin/youtube-dl
```

After downloading the script, set the executable permission.

```shell
    # chmod a+x /usr/local/bin/youtube-dl
```

Now, let's verify if the youtube-dl command works,

```shell
    # youtube-dl -h
```

If you get output from the above command, it's fine. Else, you have to copy/move the script file to /bin directory.


```shell
    # cp /usr/local/bin/youtube-dl /bin/
```

Verify again if the `youtube-dl -h` command works and hope it would work as it did for me.

#### STEP 2: CREATE BASH SCRIPT

Now that we have installed the youtube-dl, let's create a bash script that will take input from a file.

```shell
    #!/bin/bash
    while read videos
    do
        youtube-dl $videos 
    done
```

Save the script. I saved it as `demo.sh`.

That's it. Our script is ready now, but we are not finished yet.

#### STEP 3: CREATE A FILE WITH VIDEO URLs

The final step would be creating a simple file that contains video URLs. Make sure each video URL is in separate lines.

```
    video1 url <br>
    video2 url <br>
    video3 url <br>
```

Save the file with any name you want. For example, I saved the file as a video list.

#### STEP 4: EXECUTE THE SCRIPT

Finally, we are ready to download the list of videos in single command from youtube.

```shell
    # ./demo < videolist
```

`./demo` -- This is our script
`videolist` -- Our file containing list of videos
`<` -- This is STDIN i.e we are giving the file as input for our script.
That's it.. :smile: