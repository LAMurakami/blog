---
layout: post
title: "I was able to install hplip 3.20.6 from source on Linux Mint 20"
date: 2020-07-21 19:11:37 -0800
---
<!-- start content -->
<div id="mw-content-text" lang="en" dir="ltr"><div><p><br />
The
<a rel="nofollow" href="{{ site.baseurl }}/man/hp-plugin.html">hp-plugin</a>
<a rel="nofollow" href="{{ site.baseurl }}/man/hp-setup.html">hp-setup</a> and
<a rel="nofollow" href="{{ site.baseurl }}/man/hp-check.html">hp-check</a> commands
are built along with the HP Device Manager gui from the hplip source
</p><p>When I look at hplip Release notes I see support for Linux Mint 19.3 wasn't officially added until version 3.20.3 which only came out January 27 earlier this year.  I do not see that Ubuntu 20.04 is supported but the hplip-gui hplip-data and hplip applications seem to work even though hp-check reports a lot of errors.
</p><p>The hplip-gui package of Ubuntu contains the GUI which appears as "HP Toolbox" on the menus.  By default it appears to be integrated with the simple-scan package which is an alternate front end to the sane package that xsane also uses.
</p><p>I just upgraded four machines to Linux Mint 20 and had an issue with hplip-toolbox and hp-plugin on ak19 and no issue on the other machines.  I had previously had an issue with scanning on that machine and had installed hplip from source which resolved the problem with the alternate xsane GUI and HP Device Manager.
</p>
<div id="toc"><input type="checkbox" role="button" id="toctogglecheckbox" style="display:none" /><div lang="en" dir="ltr"><h2>Contents</h2><label for="toctogglecheckbox"></label></div>
<ul>
<li><a href="#I_was_able_to_install_hplip_3.20.6_from_source_on_Linux_Mint_20">1 I was able to install hplip 3.20.6 from source on Linux Mint 20</a>
<ul>
<li><a href="#A_lot_of_.22..2Fconfigure.22_steps">1.1 A lot of "./configure" steps</a></li>
<li><a href="#python-dev-is-python3_resolves_the_.22cannot_find_python-devel_support.22_config_error">1.2 python-dev-is-python3 resolves the "cannot find python-devel support" config error</a></li>
<li><a href="#Continue_with_.22make.22_.22make_install.22_steps">1.3 Continue with "make" "make install" steps</a></li>
</ul>
</li>
<li><a href="#The_hplip_package_includes_the_hp-check_utility">2 The hplip package includes the hp-check utility</a></li>
<li><a href="#This_post_is_not_complete_install_instructions">3 This post is not complete install instructions</a></li>
</ul>
</div>

<h2><span id="I_was_able_to_install_hplip_3.20.6_from_source_on_Linux_Mint_20">I was able to install hplip 3.20.6 from source on Linux Mint 20</span></h2>
<p>This is the latest version as of July 2020 but the source is not yet ready for Linux Mint 20 or Ubuntu 20.04.
</p><p>The Manual Build and Install Instructions for both <a rel="nofollow" href="https://developers.hp.com/hp-linux-imaging-and-printing/install/manual/distros/linuxmint">Linux Mint</a> and <a rel="nofollow" href="https://developers.hp.com/hp-linux-imaging-and-printing/install/manual/distros/ubuntu">Ubuntu</a> at the HP's Developer Portal install with a /usr prefix which is wrong from what I know about installing software.  I used /usr/local as the prefix because I am installing from source.  This is based on the general guidance about bin:
</p>
<ul><li>/usr/local/bin is for normal user programs not managed by the distribution package manager, e.g. locally compiled packages. You should not install locally compiled packages into /usr/bin because future distribution upgrades may modify or delete them without warning.</li></ul>
<h3><span id="A_lot_of_&quot;./configure&quot;_steps"></span><span id="A_lot_of_.22..2Fconfigure.22_steps">A lot of "./configure" steps</span></h3>
<p>I ran a lot of the "./configure" steps to resolve dependencies.  The options I used ended up being:
</p>
<pre>./configure --prefix=/usr/local --with-hpppddir=/usr/share/ppd/HP \
--libdir=/usr/lib/x86_64-linux-gnu --enable-qt5 --enable-hpcups-install \
--enable-cups-drv-install --disable-cups-ppd-install --disable-hpijs-install \
--disable-foomatic-drv-install --disable-foomatic-ppd-install \
--disable-foomatic-rip-hplip-install --enable-fax-build --enable-dbus-build \
--enable-network-build --enable-scan-build --disable-policykit \
--disable-libusb01_build --disable-udev_sysfs_rules --enable-doc-build
</pre>
<p>Much is from the HP's Developer Portal install instructions except I use the -prefix=/usr/local and --enable-qt5 options.  I discussed the prefix above and I found the --enable-qt5 option when reviwing the "./configure --help" output.
I used only the default Linux Mint 20 repositories which includes the upstream Ubuntu 20.04 repositories.  Usually if it is a good configure like the one for the hplip software, missing required dependencies result in a message at the end of the compile process like:
</p>
<ul><li>configure: error: "cannot find &lt;package&gt; support"</li></ul>
<p>This particular process is more complicated because the hplip package is not ready for the Ubuntu 20.04 base and the package names do not match available packages.
</p>
<h3><span id="python-dev-is-python3_resolves_the_&quot;cannot_find_python-devel_support&quot;_config_error"></span><span id="python-dev-is-python3_resolves_the_.22cannot_find_python-devel_support.22_config_error">python-dev-is-python3 resolves the "cannot find python-devel support" config error</span></h3>
<p>The following produces a lot of output and when looking for python-devel which is not available.
</p>
<pre>apt-cache search python | grep dev
</pre>
<p>I don't remember the entire sequence of packages I installed in my attempt to resolve all the configure errors but I remember python-dev-is-python3 solved the last one.
</p><p>You must remove python-minimal before attempting to install python-is-python3 and python-dev-is-python3
</p>
<pre>sudo apt-get remove python-minimal
</pre>
<p>At one point python-is-python2 was installed along with another package and should be removed before python-dev-is-python3 is installed.
</p>
<pre>sudo apt-get remove python-is-python2
</pre>
<pre>sudo apt-get install python-dev-is-python3 python-is-python3
</pre>
<h3><span id="Continue_with_&quot;make&quot;_&quot;make_install&quot;_steps"></span><span id="Continue_with_.22make.22_.22make_install.22_steps">Continue with "make" "make install" steps</span></h3>
<p>Once the configure step completes normally the "make" and "make install" complete normally.
</p>
<pre>make
sudo make install
</pre>
<h2><span id="The_hplip_package_includes_the_hp-check_utility">The hplip package includes the hp-check utility</span></h2>
<p>The output of the hp-check utility includes a summary of Missing Required and Optional Dependencies.  I was able to remove all but the python3-pyqt4 Required and python3-dbus.mainloop.qt Optional Dependencies and with --enable-qt5 specified in the configure step this does not prevent the hp-plugin from working for me when the one provided in the default Ubuntu 20.04 repositories did not.
</p><p>Once additional dependencies are installed restart the build process from the configure step.
</p>
<h2><span id="This_post_is_not_complete_install_instructions">This post is not complete install instructions</span></h2>
<p>Sometimes I stop when the problem is resolved and sometimes I try to document how I solved the problem.  The hplip software has been around a while and has installation instructions for a lot of Linux distributions including Linux Mint and Ubuntu.  The developers that maintain hplip are not yet supporting the latest versions of Linux Mint and Ubuntu but the version in the Ubuntu repositories seem to work for most people.  I could not find documentation on a build for Ubuntu 20.04 but was able to succeed for my purposes.
</p><p>It's actually been a few days since I first resolved my problem and it was a problem with the upgrade of one of my machines that I commented on in the <a rel="nofollow" href="https://blog.linuxmint.com/?p=3946">"How to upgrade to Linux Mint 20" post</a>.
</p>
<!-- 
NewPP limit report
Cached time: 20200722020956
Cache expiry: 86400
Dynamic content: false
Complications: []
CPU time usage: 0.024 seconds
Real time usage: 0.025 seconds
Preprocessor visited node count: 27/1000000
Preprocessor generated node count: 0/1000000
Post‐expand include size: 60/2097152 bytes
Template argument size: 0/2097152 bytes
Highest expansion depth: 2/40
Expensive parser function count: 0/100
Unstrip recursion depth: 0/20
Unstrip post‐expand size: 0/5000000 bytes
-->
<!--
Transclusion expansion time report (%,ms,calls,template)
100.00%    0.000      1 -total
-->

<!-- Saved in parser cache with key wikidb:pcache:idhash:367-0!canonical and timestamp 20200722020956 and revision id 5201
 -->
</div></div><div>
Retrieved from "<a dir="ltr" href="https://ak17.lam1.us/A/index.php?title=Hplip_(software)&amp;oldid=5201">https://ak17.lam1.us/A/index.php?title=Hplip_(software)&amp;oldid=5201</a>"</div>
<!-- end content -->
