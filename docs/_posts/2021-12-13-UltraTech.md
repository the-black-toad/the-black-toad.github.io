---
layout: post
title: "Ultratech | THM "
date: 2021-12-13 17:17:00 -0000
categories: CTF THM
---

<h2>Executive Summary</h2>

An api endpoint that can be tricked into allowing code execution allows us to strip creds from the server and then log onto the server. Once on the server, a user left in the docker group allows us to gain root.

<h2>Technical Details</h2>

<h2>Enumeration</h2>

Lets start with the classic nmap: 

nmap 10.10.124.243  
Starting Nmap 7.92 ( https://nmap.org ) at 2021-12-13 06:32 EST  
Nmap scan report for 10.10.124.243  
Host is up (0.090s latency).  
Not shown: 997 closed tcp ports (conn-refused)  
PORT     STATE SERVICE  
21/tcp   open  ftp  
22/tcp   open  ssh  
8081/tcp open  blackice-icecap  
  http    Node.js Express framework  
|_http-cors: HEAD GET POST PUT DELETE PATCH  
|_http-title: Site doesn't have a title (text/html; charset=utf-8).  
31331/tcp open  http    Apache httpd 2.4.29 ((Ubuntu))  
|_http-title: UltraTech - The best of technology (AI, FinTech, Big Data)  
|_http-server-header: Apache/2.4.29 (Ubuntu)  
  
Nmap done: 1 IP address (1 host up) scanned in 2.45 seconds   
  
8081 is an API with the following endpoints:   
auth, ping Auth and Ping  
  
So, we have a few interesting things standing out here. First, http running on a non-standard port. Some node.js running on 8081. Lets keep enumerating. Gobuster is our next stop.  

31331 is running a nice robots.txt with the following url hidden: utech_sitemap.txt  
this exposes the following endpoints  
/index.html /what.html   
/partners.html -> login form   

When we try to login the login form calls back to the auth api. Maybe this is vuln to a sqlmap/sql injection?  
I tried some various regular sql injections and then running sqlmap on everything on 8081. Nothing worked!  
So, the auth api seems to be strapped down fairly well. The ping api will let you run anything as long as we can figure out how to trick it. The source code is available to be looked at /js/api.js  
It keeps breaking so now we need to figure out how to exploit that. It is filtering on ; and I can't seem to get it to work. After a lot of different attempts, it turned out that you needed to escape the command with back ticks.  
Not sure why this worked! I will do some research on this. 

`ls` gets us the name of the file present in that api directory. Then we can use `cat` to read that file and we get the following hashes:  
r00t:      f357a0c52799563c7c7b76c1e7543a32)  - n100906 - this works for all logins, nice!  
admin:   0d0ea5111e3c1def594c1684e3b9be84 - mrsheafy  

<h2>Initial Foothold</h2>  

We can use the cracked hash to ssh onto the server. After looking in the normal places, I couldn't find anything. So, I checked the id of the user and we are in the docker group. Lets see if we can run anything interesting: find /home -group docker - So we can run docker commands. After some googling, it seems to be that this is a valid priv esc avenue. 

<h2>Priv Esc </h2>  

Lets look up gtfo bins and see if there is an exploit. There is!  

docker run -v /:/mnt --rm -it alpine chroot /mnt sh  

However, when we run this command we get an error that we cannot find the alpine image. Lets take a look at what docker images there are:  

docker images  
  
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE  
bash                latest              495d6437fc1e        2 years ago         15.8MB  
  
ok! So no alpine, lets replace it with bash.  

Boom! were in.  

Then, just navigate to the .ssh and read that key. Make sure you can count to 9.  


