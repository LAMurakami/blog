---
layout: post
title: "Baloo is a daemon that forced me to remove konqueror after upgrading to Linux Mint 20"
date: 2020-07-15 21:25:58 -0800
---
<!-- start content -->
<div id="mw-content-text" lang="en" dir="ltr"><div><p>When I discovered baloo I was trying to find what was trying to kill my system.  I had upgraded from Linux Mint 19.3 yesterday and had a number of small issues and an unidentified issue causing my web server to have issues.  This was the fourth computer I had upgraded to Linux Mint 20 and had been able to resolve all the previous issues.  I went to bed not knowing what the issue was but sure I would be able to solve it.
</p><p>This morning I was surprised to find that the root partition was filling up and the lack of space was the problem.  My initial investigation showed that my home folder was using a huge amount of space and causing the system to have issues.  I initially missed that it was a pair hidden log files using up space but did see I had a copy of the 26G Music folder there and deleted it since I know I have other copies.
</p><p>After I provided over 25G of space I was surprised to find it quickly being used up by something I wasn't seeing.  I finally found the hidden .xsession-errors and .xsession-errors.old files using over 40G of space and growing at almost 1G / minute.  I then saw a huge number of the same messages over and over in the file.  I first noticed:
</p>
<pre>org.kde.baloo.engine: PositionDB::put MDB_BAD_TXN: Transaction must abort, has a child, or is invalid
</pre>
<p>When I searched the web I saw "<a rel="nofollow" href="https://forums.gentoo.org/viewtopic-t-1094392-start-25.html">HELP! My /home partition keeps filling up</a>" which mentioned the message I had searched for along with:
</p>
<pre>org.kde.baloo.engine: PostingDB::put MDB_BAD_TXN: Transaction must abort, has a child, or is invalid 
</pre>
<p>There was a bunch of discussion and "pkill baloo put an end to that nonsense" made sense to me.  I continued reading and saw people complaining about the difficulty in telling the daemon not to run.  I knew one way would be to remove the package with the daemon in it.  I saw I had a libkf5balooengine5 and decided to remove it.
</p><p>I removed konqueror because it was dependent upon baloo and I wanted baloo off my system so bad I was willing to give up konqueror.  I saw dolphin was also dependent on baloo but I use that even less than konqueror and could not actually remember the last time I had used either.
</p><p>I don't think I ever had KDE installed on ak17.  The ak17 machine was bought after the Burglary when many of my machines were stolen.  I did not get around to making it my main server until the beginning of 2018 partly becasue I still had ak7 which was working.  I know I have done a major upgrade on ak17 before including from 18 to 19 as well as the smaller point releases.
</p><p>I think I installed konqueror on ak19 just to have another browser.
</p><p>It looks like the but has been seen by people for at least 5 years and is still there.  I did some research and question the whole philosophy intentionally limiting settings for the daemon and especially not fixing the bugs.
</p><p>After correcting the problem by removing the horrible daemon and deleting the files I did not have room for I decided to do a little more investigating.  I looked at the backup from this morning and saw over 15G in the two files of the backup.  Those two files had over 164 million records in them and only 321 were not related to baloo.  The bulk were the following 4 messages repeated over and over.
</p>
<pre>org.kde.baloo.engine: PostingDB::put MDB_BAD_TXN: Transaction must abort, has a child, or is invalid
org.kde.baloo.engine: PositionDB::put MDB_BAD_TXN: Transaction must abort, has a child, or is invalid
org.kde.baloo.engine: Transaction::commit MDB_BAD_TXN: Transaction must abort, has a child, or is invalid
/home/lam/VirtualBox VMs/WXP-VM1/Logs/VBox.log.3" id seems to have changed. Perhaps baloo was not running, and this file was deleted + re-created
</pre>
<p>These messages might have some value but repeating the same messages over a million times an hour without any additional information such as a date or time stamp while using as much system resources as are available is not acceptable on my system.
</p><p>I was a fan of KDE for while but from my notes it looks like it has been over 5 years since I ran the KDE desktop.  I remember specifically installing some KDE over GNOME and I guess I did it over Cinnamon as well.  Other than konqueror I remember some KDE games that I installed but apparently not on ak17.
</p><p>I have more detail currently that I could provide to someone if it might help get the error fixed but I don't know that more info is necessary and it looks like the developers don't think it needs to be fixed.
</p><p>My only previous comments on Baloo are related to the Mowgli and Baloo characters of Jungle Book 2.
</p>
<!-- 
NewPP limit report
Cached time: 20200716052233
Cache expiry: 86400
Dynamic content: false
Complications: []
CPU time usage: 0.007 seconds
Real time usage: 0.008 seconds
Preprocessor visited node count: 1/1000000
Preprocessor generated node count: 0/1000000
Post‐expand include size: 0/2097152 bytes
Template argument size: 0/2097152 bytes
Highest expansion depth: 1/40
Expensive parser function count: 0/100
Unstrip recursion depth: 0/20
Unstrip post‐expand size: 0/5000000 bytes
-->
<!--
Transclusion expansion time report (%,ms,calls,template)
100.00%    0.000      1 -total
-->

<!-- Saved in parser cache with key wikidb:pcache:idhash:368-0!canonical and timestamp 20200716052233 and revision id 5180
 -->
</div></div><div>
Retrieved from "<a dir="ltr" href="https://ak17.lam1.us/A/index.php?title=Baloo_is_a_daemon_that_forced_me_to_remove_konqueror_after_upgrading_to_Linux_Mint_20&amp;oldid=5180">https://ak17.lam1.us/A/index.php?title=Baloo_is_a_daemon_that_forced_me_to_remove_konqueror_after_upgrading_to_Linux_Mint_20&amp;oldid=5180</a>"</div>
<!-- end content -->
