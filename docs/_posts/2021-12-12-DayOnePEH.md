---
layout: post
title: "Practical Ethical Hacking | TCM "
date: 2021-12-12 17:17:00 -0000
categories: Course
---

Taking notes on the course of of Practical Ethical hacking. This is just a blog post going over the first few sessions. 

Notekeeping is super important! 
Make sure that you have a good notekeeping application and some good notekeeping habits. Screenshots and organizations are nice and they speed things up. Sometimes 
clients will come back 6 months later and they want to know what you did at what time. Keepnote is the application that he uses. Cherrytree, OneNote, and Joplin.

Networking - the classic foundational skill. 
IP addresses are made up of 8 bytes and there are four quartets. 0-255 for each section. 4 billion possible ip addresses. 
IPv6 128 bits with large number of addresses. NAT is the solution for extending multiple IP addresses. 

Remember that there are different types of networks broken up to server different shapes of networks. 

|  Net. Numbers | Net. Mask | No. of Networks | No. Hosts |    
| --- | --- | --- | --- |
|Class A network | 10.0.0.0 | 255.0.0.0 | 126 | ~16,000,000 |
|Class B network | 172.16-31.0.0 | 255.255.0.0 | ~16,000 | ~65,000 |
|Class C network | 192.168.0-255.0-255 | 255.255.255.0 | ~2,000,000 | ~254 |

MAC Addresses - media access control or burned in address. Physical address that is tied to the manufacturer. Layer 2. 

TCP and UDP 
TCP - transmission control protocol. Connection oriented. FTP HTTP and HTTPS. Utilizes a three way handshake
UDP - user datagram protocol. Stream orientated. Video, dns, and VOIP.

The common ports 
SMB 139 + 445 the classic ports. Wannacry and Eternal Blue. See this a lot out in the wild.

Then, TCM goes through a great overview of subnetting including a very good chart. Having taken Keith Barker's course on youtube, I would recommend using a mixture of both of these methods. Subnetting just took repetition for me to really understand it. If you also take the time to work out the problems with a pen and paper that helps as well. Following that there is a discussion on how to get 
VMs set-up on your machine. But, hey, we use arch here so no need for that. 
