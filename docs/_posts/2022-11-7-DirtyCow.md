---
layout: post
title: "Linux Priv Esc | WP "
date: 2022-11-3 23:52:00 -0000
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
  
  <p> more on the dirty cow vuln: 
