---
layout: post
title: "Practical Ethical Hacking | TCM "
date: 2021-12-12 17:17:00 -0000
categories: Course
---

Taking notes on the course of of Practical Ethical hacking. This is just a blog post going over the first few sessions.  

Notekeeping is super important!  
Make sure that you have a good notekeeping application and some good notekeeping habits. Screenshots and organizations are nice and they speed things up. He made the point that sometimes 
clients will come back 6 months later and they want to know what you did at what time. Keepnote is the application that he uses. Cherrytree, OneNote, and Joplin. ( I have started to use keepnote as it is a simple program ) Flameshot runs great on arch as well.  

Networking - the classic foundational skill.   
IP addresses are made up of 8 bytes and there are four quartets of these 8 bytes. Within each section, there are 0-255 possible values. There are 4 billion possible ipv4 addresses. IPv6 was introduced to solve this problem, but as they are non-human friendly addresses people tended to stay with IPv4 and use NAT. NAT is a solution for extending multiple IP addresses. 

Remember that there are different types of networks broken up to server different shapes of networks. 

|  Net. Numbers | Net. Mask | No. of Networks | No. Hosts |    
| --- | --- | --- | --- |
|Class A network | 10.0.0.0 | 255.0.0.0 | 126 | ~16,000,000 |
|Class B network | 172.16-31.0.0 | 255.255.0.0 | ~16,000 | ~65,000 |
|Class C network | 192.168.0-255.0-255 | 255.255.255.0 | ~2,000,000 | ~254 |
  
Heath has also provided the greatest memonic for the OSI stack: 
| # | phrase | layer | example | 
| --- | --- | --- | --- |
| 1 | Please | Physical | data cables, cat6 | 
| 2 | Do | Switching | MAC addreses | 
| 3 | Not | Networking | Ip addresses, routing |  
| 4 | Throw | Transport | TCP/UDP | 
| 5 | Sausage | Session | Session managment |  
| 6 | Pizza | Presentation | WMV | 
| 7 | Away | Application | HTTP, SMTP |   

MAC Addresses - media access control or burned in address. Physical address that is tied to the manufacturer. Layer 2. 

TCP and UDP 
TCP - transmission control protocol. Connection oriented. FTP HTTP and HTTPS. Utilizes a three way handshake
UDP - user datagram protocol. Stream orientated. Video, dns, and VOIP.

The common ports 
SMB 139 + 445 the classic ports. Wannacry and Eternal Blue. See this a lot out in the wild.

Then, TCM goes through a great overview of subnetting including a very good chart. Having taken Keith Barker's course on youtube, I would recommend using a mixture of both of these methods. Subnetting just took repetition for me to really understand it. If you also take the time to work out the problems with a pen and paper that helps as well. Following that there is a discussion on how to get 
VMs set-up on your machine. But, hey, we use arch here so no need for that.  

(I also figured out tables in markdown) 
