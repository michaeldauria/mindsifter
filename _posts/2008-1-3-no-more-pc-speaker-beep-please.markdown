--- 
layout: post
title: No More PC Speaker Beep Please
---
I hate that damn loud beeping noise coming from any machine, even more so from a VM that decided to crash my computer, but that's another article.

Here's how you remove the noises from an Ubuntu machine:

<pre><code>
 $ sudo rmmod pcspkr
 $ sudo vi /etc/modprobe.d/blacklist
</code></pre>

Now simply add the following line to the end:

<pre><code>
 blacklist pcspkr
</code></pre>

Done and done.
