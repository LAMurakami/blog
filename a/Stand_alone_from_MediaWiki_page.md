---
layout: page
title: "Stand alone from MediaWiki page"
---

<span style="float: right;"><a href="#toc">Contents</a></span>
<!-- start content -->
<div id="mw-content-text" lang="en" dir="ltr"><div>

<h1><span id="Make_a_stand_alone_version_of_a_MediaWiki_page.">Make a stand alone version of a MediaWiki page.</span></h1>
<p>I am able to create a stand alone web page for a MediaWiki page using cut and paste from the source view of the LAMipeda page and minimal editing.
</p>
<h2><span id="Extract">Extract</span></h2>
<p>Cut From: &lt;!-- bodytext --&gt; To: &lt;!-- /bodytext --&gt; # Vector Skin
</p><p>Cut From: &lt;!-- start content --&gt; To: &lt;!-- end content --&gt; # MonoBook Skin
</p><p>I have found it easiest to put the complete source in the temp file then delete all before and all after the above tags.
</p><p>On ak19
</p>
<pre>cd /mnt/ak20-ext4/Temp
</pre>
<p>On the local machine
</p>
<pre>rm temp.html
leafpad temp.html &amp;
</pre>
<pre>WEB_PAGE=$(date +%Y-%m-%d)-WEB_page.html
</pre>
<pre>ll ${WEB_PAGE}
</pre>
<pre>rm ${WEB_PAGE}
</pre>
<pre>scp -p ${WEB_PAGE} q:/mnt/Bk0/Temp
</pre>
<h2><span id="Hints_for_using_vi_to_edit_the_temp.html_text_file.2C_stripping_before_and_after_bodytext."></span><span id="Hints_for_using_vi_to_edit_the_temp.html_text_file,_stripping_before_and_after_bodytext.">Hints for using vi to edit the temp.html text file, stripping before and after bodytext.</span></h2>
<p>To turn on line numbers:
</p>
<pre>&lt;escape&gt;:set nu
</pre>
<p>To go to the first line in the file:
</p>
<pre>:1
</pre>
<p>To go to the bodytext comment:
</p>
<pre>/bodytext
</pre>
<p>To go to the next in the same direction:
</p>
<pre>n
</pre>
<p>To delete from the beginning to a line number:
</p>
<pre>:1,&lt;n&gt;d
</pre>
<p>To delete from a line number to the end:
</p>
<pre>:&lt;n&gt;,$d
</pre>
<h2><span id="Strip_wiki_style">Strip wiki style</span></h2>
<p>Give a jekyll build stand alone page file the MarkDown extension of .md which can have the jekyll front matter and html source.
</p>
<pre>WEB_PAGE=Stand_alone_from_MediaWiki_page.md
</pre>
<p>The following stripped the edit links and all class information except the span tags which become green.
</p>
<pre>cat temp.html \
| perl -pe 's|&lt;span&gt;&lt;span&gt;\[.*?\]&lt;/span&gt;&lt;/span&gt;||' \
| perl -pe 's|||g' \
| perl -pe 's|&lt;span&gt;(.*?)&lt;/span&gt;|$1|g' &gt; ${WEB_PAGE}
</pre>
<pre>chmod a+r ${WEB_PAGE}
</pre>
<h2><span id="Edit">Edit</span></h2>
<p>Using:
</p>
<pre>leafpad ${WEB_PAGE} &amp;
</pre>
<p>Note that leafpad is a lightweight gui editor that is not installed by default on ARSC machines but I have put a copy in ~murakami/bin on jeeves and a few other machines.  You can of course use the editor of your choice;-)
</p>
<ul><li>Strip script from the end of the toc table.</li>
<li>Move toc to bottom</li>
<li>Move "Retrieved from" to below toctitle</li>
<li>Remove Categories</li>
<li>Insert header</li>
<li>Add &lt;/body&gt;&lt;/html&gt; to end</li></ul>
<h3><span id="jekyll_build_Head_section:">jekyll build Head section:</span></h3>
<pre>---
layout: page
title: "hp-setup - Printer/Fax Setup Utility"
---
</pre>
<p>If there was a table of contents add a link to it after the jekyll front matter with:
</p>
<pre>&lt;span style="float: right;"&gt;&lt;a href="#toc"&gt;Contents&lt;/a&gt;&lt;/span&gt;
</pre>
<h3><span id="lam1.us_Head_section:">lam1.us Head section:</span></h3>
<pre>&lt;html&gt;&lt;head&gt;

&lt;title&gt;Cabo Weeks 2015&lt;/title&gt;

&lt;link rel="Shortcut Icon" href="/Images/My/LAM.ico" /&gt;
&lt;link rel="stylesheet" type="text/css" href="/Public/Style.css" /&gt;

&lt;/head&gt;&lt;body&gt;

&lt;a href="."&gt;
&lt;img src=&quot;/Images/My/lam1-us.png"
alt="LAM1 US logo" border="0" width="135" height="98" style="float: left;"/&gt;&lt;/a&gt;

&lt;h1 &gt;&amp;nbsp;

Cabo Weeks 2015

&lt;/h1&gt;
&lt;br&gt;
</pre>
<h1><span id="Revision_Log">Revision Log</span></h1>
<ul><li>Saturday, July 16, 2022 - Added jekyll build Head section.
<ul><li>Extracted to: <a rel="nofollow" href="https://lamurakami.github.io/blog/a/Stand_alone_from_MediaWiki_page.html">https://lamurakami.github.io/blog/a/Stand_alone_from_MediaWiki_page.html</a></li></ul></li>
<li>1/2/2015 Copied this from <a href="/a/Talk:Christmas_/_New_Year" title="Talk:Christmas / New Year">Talk:Christmas / New Year</a> after finding the difference between the output from the MonoBook Skin and the Vector Skin.</li></ul>
<!-- 
NewPP limit report
Cached time: 20220717010350
Cache expiry: 86400
Reduced expiry: false
Complications: []
CPU time usage: 0.005 seconds
Real time usage: 0.005 seconds
Preprocessor visited node count: 25/1000000
Post‐expand include size: 0/2097152 bytes
Template argument size: 0/2097152 bytes
Highest expansion depth: 2/100
Expensive parser function count: 0/100
Unstrip recursion depth: 0/20
Unstrip post‐expand size: 0/5000000 bytes
-->
<!--
Transclusion expansion time report (%,ms,calls,template)
100.00%    0.000      1 -total
-->

<!-- Saved in parser cache with key wikidb:pcache:idhash:167-0!canonical and timestamp 20220717010350 and revision id 6267. Serialized with JSON.
 -->
</div>
<div>Retrieved from "<a dir="ltr" href="https://ak20.lam1.us/A/index.php?title=Stand_alone_from_MediaWiki_page&amp;oldid=6267">https://ak20.lam1.us/A/index.php?title=Stand_alone_from_MediaWiki_page&amp;oldid=6267</a>"</div></div>
<!-- end content -->
<div id="toc" role="navigation" aria-labelledby="mw-toc-heading"><input type="checkbox" role="button" id="toctogglecheckbox" style="display:none" /><div lang="en" dir="ltr"><h2 id="mw-toc-heading">Contents</h2><label for="toctogglecheckbox"></label></div>
<ul>
<li><a href="#Make_a_stand_alone_version_of_a_MediaWiki_page.">1 Make a stand alone version of a MediaWiki page.</a>
<ul>
<li><a href="#Extract">1.1 Extract</a></li>
<li><a href="#Hints_for_using_vi_to_edit_the_temp.html_text_file,_stripping_before_and_after_bodytext.">1.2 Hints for using vi to edit the temp.html text file, stripping before and after bodytext.</a></li>
<li><a href="#Strip_wiki_style">1.3 Strip wiki style</a></li>
<li><a href="#Edit">1.4 Edit</a>
<ul>
<li><a href="#jekyll_build_Head_section:">1.4.1 jekyll build Head section:</a></li>
<li><a href="#lam1.us_Head_section:">1.4.2 lam1.us Head section:</a></li>
</ul>
</li>
</ul>
</li>
<li><a href="#Revision_Log">2 Revision Log</a></li>
</ul>
</div>
