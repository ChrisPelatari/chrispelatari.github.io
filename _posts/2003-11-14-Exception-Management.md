---
layout: post
title: Exception Management
---
<p>I've been using the <a href="http://msdn.microsoft.com/library/default.asp?url=/library/en-us/dnbda/html/emab-rm.asp">Exception Management Application Block</a> for quite some time now, and for general purpose it's great. Especially when I need some detailed information about exceptions generated from an asp.net application, EMAB's got my back.</p>
<p>The only problem that I've had so far (barring non-perfectly formed configSections) I ran into today, and it had to do with Registry Access. I'm in the midst of deploying a windows forms application that uses the EMAB, but the user I wanted to deploy to was not an administrator (and <u>really</u> shouldn't be.) So, I had to :</p>
<ul>
<li>rebuild my installer, removing the custom action to install EMAB</li>
<li>log the user out</li>
<li>log in as administrator</li>
<li>run cmd: cd C:\%windir%\microsoft.net\framework\v1.1.4322\</li>
<li>installutil "Path to EMAB"</li>
<li>let the user log back in before we could test things.</li>
</ul>
<p>What a pain in the ass! Maybe I'm just spoiled from all of this xcopy <strike>sh</strike> deployment bru-haha.;) Anyways, I hope that .NET becomes easier for non-administrators to use...okay, maybe that's a gross generalization, but the point is that <i>Registry Access</i> never crossed my mind as an issue to resolve, because I'm always running in "God Mode" and therefore never really worry about these things.</p>
<p>Funny thing is that I created a fake User in the same group as the target user and deployed the application to a test machine before I ever put the app on the target machine - the installer and everything worked like a charm, but shouldn't have (unless EMAB was already installed:)...Okay, I need to blog more b/c this is turning into a rant. All I really wanted to do was outline what I needed to do to get EMAB installed for a non-administrator. Shh! If you're still reading, don't tell, aiight?</p>
<div class="media">-= Currently Jammin: Psycho - System Of A Down - toxicity :=-</div>