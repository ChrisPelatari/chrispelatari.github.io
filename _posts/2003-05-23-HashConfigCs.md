---
layout: post
title: HashConfigCs
---
I just made a change to some code I wrote a while back that generates a text file with strong encryption/decryption keys for use in a machine.config or web.config.

The change was minor, but when I first used it I didn't intend to tell anyone about it, but nor did I have a blog. Basically, all I did was add a little code to the MSDN example that walks you thru the process of defining strong &lt;machineKey/&gt; elements for inter-host forms authentication (among other things).

It's a command-line exe that takes 3 arguments:

1. number of bytes to make the decryption key
2. number of bytes to make the validation key
3. output file name.

The example given by MSDN is great, and there aren't any code changes as far as the logic for creating the keys go. I wanted to be able to copy/paste the results tho, so I added some pretty trivial filestream code to it. If one of you two is interested, ping me. Oh yeah, the code is in C#.