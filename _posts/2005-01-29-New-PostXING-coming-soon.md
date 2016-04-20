---
layout: post
title: New PostXING coming soon
---
<p>With the help of <a href="http://weblogs.asp.net/lkempe">Laurent Kempé</a>, 
I've traced down a bug in the PostXING FTP library (or rather my handling of it) 
and ended up changing the underlying FTP library code to the open source <a href="http://www.enterprisedt.com/products/edtftpnet/overview.html">edtFTPnet 
</a>library. This is a more complete library than the sample socket code that I 
was using before, and since it's LGPL licensed, I can link it into my code 
without affecting the license that PostXING is released under (which is 
zlib/libpng).</p>
<p>I also plan to add proxy support soon - the only hold up right now is that I 
like to at least dry run what I'm releasing before I put it out there, and I 
have no idea how to test if proxy code is going to work. Is there a such thing 
as a free proxy server that I can test against? I'm pretty resolved to, er, 
'borrowing' the functionality for proxy support from <a href="http://rssbandit.org">RssBandit </a>simply because the code works and has 
been a good reference for me before. So, I'm not worried about how to implement 
it, just on how to test it. Any ideas?</p>
<p class="media">[ Currently Playing : Move On - Jet - Get Born (4:20) 
]</p>