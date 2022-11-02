---
layout: post
title: "Antimalware Scan Interface Bypasses | WP "
date: 2022-11-1 23:58:00 -0000
categories: WhitePaper SANS
---

<h2>A New Attempt</h2> 

Instead of watching Netflix, I am going to be reading whitepapers from https://www.sans.org/white-papers/?focus-area=penetration-testing-red-teaming and trying to summarize them. 

<p> Full title: Antimalware Scan Interface Bypasses: Evading Detection to Perform Post Exploitation Activities</p>
<p> Author: Christopher Nourrie, cnourrie@gmail.com </p>

<h2> Summary </h2>

<p> This piece focused onthe AMSI and how to bypass it. The AMSI was designed by Windows to allow applications to integrate with any antimalware product thats present on the machine. 
  IT is integrated into User Account Control, powershell, wscript, csript, javascript vbs, and office vba macros. 
</p> 

<p> Essentially, there are three common ways to bypass AMSI. 
  Tricking it into returning a false scan result, patching exported functions in the .dll, and forcing an error. 
  These techniques are all currently picked up by AMSI as malicious. 
  However, the author provides some new ways to bypass these checks with simple code obsfucation tecnhniques by leveraging native powershell concat and replace functions.
  After applying them, the author is able to launch cobalt strike C2 commands that were previously blocked by AMSI.
</p>

<p> 
  I have just recently completed a few rooms on Try Hack Me about code obfuscation
  where they go over these concat and replace functions to evade antivirus. I am suprised that these work 
  well in the real world as well! 
</p>
