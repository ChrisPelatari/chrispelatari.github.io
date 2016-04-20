---
layout: post
title: "CodeSnip: Getting Currently Playing info from Windows Media Player using the blogging power toy."
---
I don't know whom this would benefit but someone building a blog posting tool 
for the desktop, but anyway here's the code that I converted from the jscript 
example that comes with the Windows Media Player [blogging](http://download.microsoft.com/download/A/D/A/ADA9E33F-2EB2-412A-A378-38C22C89055D/creativity_wmpblogging.exe) 
[powertoy](http://www.microsoft.com/windowsxp/downloads/powertoys/wm_create.mspx) :

<pre><font color="#0000ff">using</font> System;
<font color="#0000ff">using</font> Microsoft.Win32;

<font color="#0000ff">public</font> <font color="#0000ff">class</font> MediaPlayerInfo
	{

		<font color="#0000ff">public</font> <font color="#0000ff">static</font> <font color="#0000ff">string</font> GetCurrentlyPlayingMedia(){
			RegistryKey regKey = Registry.CurrentUser;
			regKey = regKey.OpenSubKey(<font color="#004884">"Software\\Microsoft\\MediaPlayer\\CurrentMetadata"</font>);

			<font color="#0000ff">string</font> displayString = <font color="#004884">"&lt;div class='media'&gt;[ Currently Listening to: "</font>;

			<font color="#0000ff">bool</font> hasMetadata = <font color="#0000ff">false</font>;

			<font color="#0000ff">string</font> trackInfo = <font color="#004884">""</font>;

			<font color="#0000ff">try</font>{
				trackInfo = regKey.GetValue(<font color="#004884">"Title"</font>).ToString();

				<font color="#0000ff">if</font>(trackInfo.Length != 0){
					hasMetadata = <font color="#0000ff">true</font>;

					displayString += trackInfo + <font color="#004884">" "</font>;
				}
			}<font color="#0000ff">catch</font>{
				<font color="#0000ff">try</font>{
					trackInfo = <font color="#004884">""</font>;
					trackInfo = regKey.GetValue(<font color="#004884">"Name"</font>).ToString();

					<font color="#0000ff">if</font>(trackInfo.Length != 0){
						hasMetadata = <font color="#0000ff">true</font>;

						displayString += trackInfo + <font color="#004884">" "</font>;
					}
				}<font color="#0000ff">catch</font>{}
			}

			<font color="#0000ff">try</font>{
				trackInfo = <font color="#004884">""</font>;
				trackInfo = regKey.GetValue(<font color="#004884">"DurationString"</font>).ToString();

				<font color="#0000ff">if</font>(trackInfo.Length != 0){
					hasMetadata = <font color="#0000ff">true</font>;

					displayString += <font color="#004884">"("</font> + trackInfo + <font color="#004884">")"</font>;
				}
			}<font color="#0000ff">catch</font>{}

			<font color="#0000ff">try</font>{
				trackInfo = <font color="#004884">""</font>;
				trackInfo = regKey.GetValue(<font color="#004884">"Author"</font>).ToString();

				<font color="#0000ff">if</font>(trackInfo.Length != 0){
					hasMetadata = <font color="#0000ff">true</font>;

					displayString += <font color="#004884">" by "</font> + trackInfo;
				}
			}<font color="#0000ff">catch</font> {}

			<font color="#0000ff">try</font>{
				trackInfo = <font color="#004884">""</font>;
				trackInfo = regKey.GetValue(<font color="#004884">"Album"</font>).ToString();

				<font color="#0000ff">if</font>(trackInfo.Length != 0){
					hasMetadata = <font color="#0000ff">true</font>;

					displayString += <font color="#004884">" on the album "</font> + trackInfo;
				}
			}<font color="#0000ff">catch</font>{}


			<font color="#0000ff">if</font>(!hasMetadata){
				displayString += <font color="#004884">"Nothing."</font>;
			}

			displayString += <font color="#004884">" ]&lt;/div&gt;"</font>;

			<font color="#0000ff">return</font> displayString;
		}
	}</pre>

It could probably stand to be a bit more flexible - ie user-defined by a 
template like w.bloggar, but for the basics it works great! Oh yeah, and let's 
not forget the output:

<div class="media">[ Currently Listening to: Rage Against The Machine - Pocket 
Full of Shells (03:52) ]</div>