---
layout: post
title: "Linux Priv Esc | WP "
date: 2022-11-7 23:34:00 -0000
categories: WhitePaper SANS
---

<h2> The dirty Cow </h2> 

<p> Full title: Attack and Defend: Linux Privilege Escalation Techniques of 2016 </p>
<p> Author: Michael Long II </p>

<h2> Summary </h2>
<p> This was a great whitepaper covering some classic Linux privilege escalation techniques </p>
<p> The techniques that were covered were, COW (copy on write) vulns, wildcard injections, suids, sudo -ls, and physical attacks. </p>
<p> The two most interesting vulnerabilities are the dirty cow vuln and the LUKS vuln. The dirty cow is a race condition where the if the copy on write function is
  called enough times it will overwrite the original file. So, this could be used to add a user into /etc/shadow or other write protected files. The LUKS vuln 
  consisted of failing the password check 93 times were then the system would drop the user in a root shell. The filesystem is still protected, but further vulnerabilities 
  could be introduced. </p>
  
  <p> more on the dirty cow vuln: the race condition is caused by racing the madvise(MADV_DONTNEED) system call while
  having a the page of the executable mapped in memory. So there are two funcitons, one that is calling the madvise and the other that is reading the executable. <a> (https://github.com/dirtycow/dirtycow.github.io/blob/master/dirtyc0w.c) </a> In the madvise function, the function of the madvise system call is "used to give advice or directions to the kernel about the address range begging at address addr and with size length bytes." <a> (https://man7.org/linux/man-pages/man2/madvise.2.html) </a> So the madvise function calls that one million times. The second function of the code is writing to /proc/self/mem folder and reseting the file pointer to that memory position a million times. Call both of those functions in two threads and you have a race. Then at the same time, you open the filepath provided in read only. The result is that you can overwrite that file. see <a> https://github.com/dirtycow/dirtycow.github.io/wiki/VulnerabilityDetails for a better write up!! </a> </p>   
