---
layout: post
title: "Mitigation Techniques to Bypass AV | WP "
date: 2022-11-2 23:28:00 -0000
categories: WhitePaper SANS
---

<h2>More AV Bypass!! </h2> 

<p> Striking from the Shadows!
<p> Full title: Striking from the Shadows: Applying and Analyzing
Mitigation Techniques to Bypass Antivirus Payload
Detection </p>
<p> Author: Matthew O'Rouke matthew@orou.ke </p>

<h2> Summary </h2>

<p> In contrast to the piece reviewed last night, this piece takes a quantitative
  approach. The Author created a research experiment to gauge what mitigation techniques
 are more effective. The author selected a few different mitigation techniques. MSFVenom
 Veil Framework by Chris Truncer, Hyperion by NullSec, and Shellter. Then, he used them to 
 attempt to evade detection on the following AVs: BitDefender, Defender, Kapersky, McAfee
 Norton, and TrendMicro. Bit Defender, Defender, and Kasperky doing the best, with TrendMicro in
  last. He also submitted the payloads to virus total. MSFVenom doing the best here are evading detection </p> 
  
  <p> One interesting finding was that "stacking mitigation techniques does not significantly
  contribute towards a lowered detection rate." An example is that a payload that is encrypted with MSFVenom 
  and one with the Shellter mitigation technique get picked up with the same flag in kapersky. So, the 
  code flow is the triggering factor not specific strings in the binary. </p>
  
  <p> My takeaways: It is refreshing to see a research experiment that is layed out in a logically manner like this
  and executed as such. Also, it reinforced that custom shellcode is the way to go. </p> 
 
