---
layout: post
title: "Overlay Filesystem Exploit | THM "
date: 2021-11-25 12:30:00 -0000
categories: CTF THM
---

OverlayFS-CVE-2021-3493

<p> Here is a brief discription from the box itself on what the overlayFS is:  

"OverlayFS is a Linux kernel module that allows the system to combine several mount points into one, so that you can access all the files from each within one directory structure.

It's often used by live USBs, or some other specialist applications. One use is having a read only root file system, and another partition "overlayed" with that to allow applications to write to a temporary file system."


The documentation from kernel.org on the overlay filesystem states that an overlay filesystem tries to present a filesystem which is the result over overlaying one filesystem on top of the other.

An overlay system "overlays" an upper filesystem and a lower filesystem where the upper is writeable and the lower is hidden. In the case where an object is referenced
in both layers, the upper layer is the one that is writable.

The need for a union mount filesystem like this was identitified in 2009 and by 2014 it was merged into the linux kernel mainline. (wikipedia)

All the documentation points to LiveCDs as the primary usage of these overlay file systems.

Read here for a in-depth writeup on the exploit:
https://ssd-disclosure.com/ssd-advisory-overlayfs-pe/

The exploit is as easy as copying that code over, compiling it with gcc and running it.

But what does it actually do?

Essentially, when the check of the filesystem namespace is passed to another part of the program, it does not check privs. So if you set the some settings in the namespace, it will get passed up and executed.

In Linux 5.11, they moved the check back into the execution part which fixes the vuln.
</p>

