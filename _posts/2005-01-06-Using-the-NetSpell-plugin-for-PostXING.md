---
layout: post
title: Using the NetSpell plugin for PostXING.
---
<p>With the <a href="http://PostXING.url123.com/v1.1.5005.1">latest release</a> 
of <a href="http://PostXING.url123.com/main">PostXING</a>, a plugin architecture 
has been added to allow for external extensions such as the new <a href="http://PostXING.url123.com/nsv1.0.5005.1">NetSpellPlugin</a> that 
adds spell checking to PostXING.</p>
<p>All that is required to install the plugin is to add the .dll file to the 
plugins subdirectory of PostXING's install directory, for me that's 
C:\bin\PostXING\plugins. When you start PostXING, you should see a new button in 
the toolbar:</p>
<p><img src="/assets/images/newtoolbarbutton.gif" /></p>
<p>as well as a couple of entries in the plugins menu under the Tools main 
menu:</p>
<p><img src="/assets/images/newpluginsmenu.gif" /></p>
<p>I really wish that was all there was to it, but unfortunately there's more 
that needs to be done. As I've said before, the spell checker is pretty well 
useless without a good dictionary file. If you try to use the plugin 
straightaway you should see this:</p>
<p><img src="/assets/images/pleaseconfigurenetspell.gif" /></p>
<p>So how do you do that? By using the ... - Configure menuitem, of course! 
:) Before you configure, tho, you should download the correct (for you) .dic 
dictionary file by either going to <a href="http://www.loresoft.com/Applications/NetSpell/default.aspx">LoreSoft's 
NetSpell page</a>, <a href="http://www.loresoft.com/Applications/NetSpell/Articles/246.aspx">creating 
your own</a>, or downloading from <a href="http://vaultpub.sourcegear.com">http://vaultpub.sourcegear.com</a> if you 
have <a href="http://sourcegear.com/vault/downloads.html">SourceGear's 
Vault Client</a> (at least version 3.0 at this time). Here's how to get the 
en-US.dic dictionary file from the command line:</p>
<p>Create a .bat file called getdic or whatever and put it either in your PATH 
or in SourceGear vault's install directory. Navigate to where vault.exe is 
located (for me it was cd C:\Program Files\SourceGear\Vault Client). Drop 
something like the following into the .bat file:</p>
<blockquote dir="ltr" style="MARGIN-RIGHT: 0px">
  <p>mkdir C:\tmp\vaultpub</p>
  <p>vault get -host vaultpub.sourcegear.com -user guest -password guest 
  -repository postxing -makewritable -destpath C:\tmp\vaultpub 
  $/ThirdParty/dic/en-US.dic</p></blockquote>
<p dir="ltr">Vault should tell you if you were successful or not in downloading 
the file. Note that the vault command above is all on one line. I don't know if 
the -makewritable is necessary or not, but this is what worked for me. Remember, 
if you prefer to blog in a different language (or a different, erm, dialect? of 
English) the ones available in vaultpub and from the NetSpell component itself 
are:</p>
<p dir="ltr">de-DE.dic<br />en-AU.dic<br />en-CA.dic<br />en-GB.dic<br />en-US.dic<br />es-ES.dic<br />es-MX.dic<br />fr-FR.dic<br />it-IT.dic</p>
<p dir="ltr">Now that you've downloaded the correct dictionary file, go to Tools 
-&gt; Plugins -&gt; ...- Configure and you'll be greeted by this simple 
dialog:</p>
<p dir="ltr"><img src="/assets/images/thissimpledialog.gif" /></p>
<p dir="ltr">Above, we said download to C:\tmp\vaultpub(\en-US.dic) so navigate 
there and hit OK. (side note: this is necessary because depending on where 
PostXING is launched from, i.e. standalone or from the <a href="http://PostXING.url123.com/plugin1.0.5004.1">BlogThisUsingPostXINGPlugin</a>, 
NetSpell will look in a different path (I think the Application.StartupPath) for 
the default dictionary based on your cultureInfo. This way, you can blog in 
English no matter what your cultureInfo is set to.)</p>
<p dir="ltr">You should now be able to spell check any Post from PostXING using 
either the toolbar button or the menu item.</p>
<p class="media">[ Currently Playing : 99 Problems - Jay-Z - The Black Album 
(3:54) ]</p>