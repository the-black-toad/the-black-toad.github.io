---
layout: post
title: "Ninja Skills | THM "
date: 2021-11-21 13:02:00 -0000
categories: CTF THM
---

<h3>Executive Summary</h3>

<p> This box was set-up to practice searching and manipulating files. </p>

<h3>Technical Details</h3>

<p> 
  
We are presented with a list of files and then a set of questions that could be answered by any of these files.

The files are:
    8V2L
    bny0
    c4ZX
    D8B3
    FHl1
    oiMO
    PFbD
    rmfX
    SRSq
    uqyw
    v2Vb
    X1Uy

And they are located somewhere on the box. So, our first task should be locating each file. We
can do that easily with the find command.
  
find / -type f -name file_name 2>/dev/null

So, lets break this command down. -type f = only look for files -name = name of the file we are looking for 2>/dev/null send all errors to null so we can read our output easier.

Now we could type this out for each file, but that is lame and I am lazy so lets create a little script that cycles through each file and operates this command on each one. Lets create a bash script and put in a for loop.


Then we can create a simple http server with python3 -m http.server and transport the script because there isn't a text editor live on the box. We run our script and we get:

/etc/8V2L
/mnt/c4ZX
/mnt/D8B3
/var/FHl1
/opt/oiMO
/opt/PFbD
/media/rmfX
/etc/ssh/SRSq
/var/log/uqyw
/home/v2Vb
/X1Uy

nice!! Now we can start answering questions because we know where our files are. Now we run into another issue where we need to run commands on all the files and compare the results. We can
modify the script to have the file path in the array and then each command we need. This lets us quickly evaluate the group.
</p>
