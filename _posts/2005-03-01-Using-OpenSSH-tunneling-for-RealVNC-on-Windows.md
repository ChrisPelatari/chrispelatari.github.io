---
layout: post
title: Using OpenSSH tunneling for RealVNC on Windows
---
I totally geeked out tonight. 

I was searching for something else and happened upon <a href="http://www.trekweb.com/~jasonb/articles/vnc_ssh.shtml">a 
tutorial</a> for tunneling VNC on windows, which led me to <a href="http://tech.erdelynet.com/ssh-vnc.html">another article</a> that was inspiration for the first article I found. Here was the problem with both: the webserver that I wanted to get to is behind an OpenBSD firewall. 

So, first things first: I added a rule to pf.conf that allowed ssh to be redirected to the private address of my webserver using rdr syntax:

<pre>rdr pass on $ext_if from any to $public_address port ssh \
-&gt; $private_address</pre>

This rule passes ssh calls bound for the external address to be sent to the 
internal network address (192.168.1.blah).

<h4>But what about ssh running on Windows?</h4>

Well, if you don't already have cygwin installed on the server, I ended up 
using <a href="http://sshwindows.sourceforge.net/">sshwindows </a>(linked from 
the <a href="http://openssh.org">OpenSSH </a>site under <a href="http://openssh.org/windows.html">Windows</a>) Just follow the instructions in readme.txt or quickstart.txt and you should be good to go there - it comes with an installer, so it was pretty easy to get up and running.

<h4>But what about the client on Windows?</h4>
For this, I use <a href="http://www.chiark.greenend.org.uk/~sgtatham/putty/">PuTTY</a>. I've used 
it for a while to ssh into my OpenBSD machines from windows. What I didn't know of is the Tunnel feature that sits near the end of the config setup tree...this is how the magic happens.

See, before, when I needed to get into a firewalled computer, I would just add rules to the firewall to punch temporary holes while I did what I had to do remotely. I know, bad Chris. Using OpenSSH to tunnel the traffic that would normally be sent unencrypted over the wire makes me feel a lot safer, even tho the server in question doesn't have a whole lot of goodies to look at. It's still important to **me.**

<h4>So how does the magic happen?</h4>

Using the tunnel feature of PuTTY, I added a link to port 5901 and mapped it to localhost:5900. Here's the rub: localhost in this case refers to the ssh server, not the computer the client is running from. The 5901 refers to the machine that the client is running from. This wasn't clear to me in either tutorial that I read thru. So you add the tunnel link to the SSH/tunels node of 
PuTTY and when you fire up VNC, have it sent to **localhost:1**. This was also not very clear from either article (but that just probably means I'm dense).

<h4>Is that it?</h4>
For VNC, yeah, it is. However, I also run a couple of applications on my 
network that contain sensitive data: namely SourceGear <a href="http://sourcegear.com/vault/index.html">Vault </a>and <a href="http://sourcegear.com/dragnet/index.html">Dragnet</a>. I want to get to these too! Can I do it in a similar way to the VNC deal? You betcha!

This time, for the tunnel link I specified an arbitrary (but often used) high port in PuTTY: 8000. I also wanted to point to the internal server (say, 192.168.1.2) so instead of specifying localhost:80 (which is already exposed -duh!) I pointed it to 192.168.1.2:80. 

Fire up PuTTY, login as some user that's configured for OpenSSH, and point my browser of choice to <a href="http://localhost:8000/dragnet">http://localhost:8000/dragnet</a>. Nice!