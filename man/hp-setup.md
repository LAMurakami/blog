---
layout: page
title: "hp-setup - Printer/Fax Setup Utility"
---
<H1>hp-setup</H1>
Section: User Manuals (1)<BR>Updated: 9.0<BR><A HREF="#index">Index</A>

<A NAME="lbAB">&nbsp;</A>
<H2>NAME</H2>

hp-setup - Printer/Fax Setup Utility
<A NAME="lbAC">&nbsp;</A>
<H2>DESCRIPTION</H2>

Installs HPLIP printers and faxes in the CUPS spooler. Tries to automatically determine the correct PPD file to use. Allows the printing of a testpage. Performs basic fax parameter setup.
<A NAME="lbAD">&nbsp;</A>
<H2>SYNOPSIS</H2>

<B>hp-setup [MODE] [OPTIONS] [SERIAL NO.|USB bus:device|IP|DEVNODE]</B>

<A NAME="lbAE">&nbsp;</A>
<H2>MODE</H2>

<DL COMPACT>
<DT>Run in graphical UI mode:<DD>
-u or --gui (Default)
<DT>Run in interactive mode:<DD>
-i or --interactive

<A NAME="lbAF">&nbsp;</A>
<H2>OPTIONS</H2>

<DL COMPACT>
<DT>Automatic mode:<DD>
-a or --auto (-i mode only)
<DT>To specify the port on a multi-port JetDirect:<DD>
--port=&lt;port&gt; (Valid values are 1*, 2, and 3. *default)
<DT>No testpage in automatic mode:<DD>
-x (-i mode only)
<DT>To specify a CUPS printer queue name:<DD>
-p&lt;printer&gt; or --printer=&lt;printer&gt; (-i mode only)
<DT>To specify a CUPS fax queue name:<DD>
-f&lt;fax&gt; or --fax=&lt;fax&gt; (-i mode only)
<DT>Type of queue(s) to install:<DD>
-t&lt;typelist&gt; or --type=&lt;typelist&gt;. &lt;typelist&gt;: print*, fax* (*default) (-i mode only)
<DT>To specify the device URI to install:<DD>
-d&lt;device&gt; or --device=&lt;device&gt; (--qt4 mode only)
<DT>Remove printers or faxes instead of setting-up:<DD>
-r or --rm or --remove
<DT>Set the language:<DD>
--loc=&lt;lang&gt; or --lang=&lt;lang&gt;. Use --loc=? or --lang=? to see a list of available language codes.
<DT>Set the logging level:<DD>
-l&lt;level&gt; or --logging=&lt;level&gt;
&lt;level&gt;: none, info*, error, warn, debug (*default)
<DT>Run in debug mode:<DD>
-g (same as option: -ldebug)
<DT>This help information:<DD>
-h or --help

<A NAME="lbAG">&nbsp;</A>
<H2>SERIAL NO.|USB ID|IP|DEVNODE</H2>

<DL COMPACT>
<DT>USB bus:device (usb only):<DD>
&quot;xxx:yyy&quot; where 'xxx' is the USB bus and 'yyy' is the USB device. (Note: The ':' and all leading zeros must be present.)
Use the 'lsusb' command to obtain this information.
<DT>IPs (network only):<DD>
IPv4 address &quot;a.b.c.d&quot; or &quot;hostname&quot;
<DT>DEVNODE (parallel only):<DD>
&quot;/dev/parportX&quot;, X=0,1,2,...
<DT>SERIAL NO. (usb and parallel only):<DD>
&quot;serial no.&quot;

<A NAME="lbAH">&nbsp;</A>
<H2>EXAMPLES</H2>

<DL COMPACT>
<DT>Setup using GUI mode:<DD>
$ hp-setup
<DT>Setup using GUI mode, specifying usb:<DD>
$ hp-setup -b usb
<DT>Setup using GUI mode, specifying an IP:<DD>
$ hp-setup 192.168.0.101
<DT>One USB printer attached, automatic:<DD>
$ hp-setup -i -a
<DT>USB, IDs specified:<DD>
$ hp-setup -i 001:002
<DT>Network:<DD>
$ hp-setup -i 66.35.250.209
<DT>Network, Jetdirect port 2:<DD>
$ hp-setup -i --port=2 66.35.250.209
<DT>Parallel:<DD>
$ hp-setup -i /dev/parport0
<DT>USB or parallel, using serial number:<DD>
$ hp-setup -i US12345678A
<DT>USB, automatic:<DD>
$ hp-setup -i --auto 001:002
<DT>Parallel, automatic, no testpage:<DD>
$ hp-setup -i -a -x /dev/parport0
<DT>Parallel, choose device:<DD>
$ hp-setup -i -b par

<A NAME="lbAI">&nbsp;</A>
<H2>NOTES</H2>

<DL COMPACT>
<DT>1. If no serial number, USB ID, IP, or device node is specified, the USB and parallel busses will be probed for devices.<DD>
<P>
<DT>2. Using 'lsusb' to obtain USB IDs: (example)<DD>
<P>
<DT>   $ lsusb<DD>
<P>
<DT>         Bus 003 Device 011: ID 03f0:c202 Hewlett-Packard<DD>
<P>
<DT>   $ hp-setup --auto 003:011<DD>
<P>
<DT>   (Note: You may have to run 'lsusb' from /sbin or another location. Use '$ locate lsusb' to determine this.)<DD>
<P>
<DT>3. Parameters -a, -f, -p, or -t are not valid in GUI (-u) mode.<DD>
<P>

<A NAME="lbAJ">&nbsp;</A>
<H2>SEE ALSO</H2>

hp-makeuri
hp-probe
<A NAME="lbAK">&nbsp;</A>
<H2>AUTHOR</H2>

HPLIP (HP Linux Imaging and Printing) is an
HP developed solution for printing, scanning, and faxing with
HP inkjet and laser based printers in Linux.
<A NAME="lbAL">&nbsp;</A>
<H2>REPORTING BUGS</H2>

The HPLIP Launchpad.net site
<B><A HREF="https://launchpad.net/hplip">https://launchpad.net/hplip</A></B>

is available to get help, report
bugs, make suggestions, discuss the HPLIP project or otherwise
contact the HPLIP Team.
<A NAME="lbAM">&nbsp;</A>
<H2>COPYRIGHT</H2>

Copyright (c) 2001-18 HP Development Company, L.P.
<P>

This software comes with ABSOLUTELY NO WARRANTY.
This is free software, and you are welcome to distribute it
under certain conditions. See COPYING file for more details.
<P>
<P>

<HR>
<A NAME="index">&nbsp;</A><H2>Index</H2>

<DT><A HREF="#lbAB">NAME</A><DD>
<DT><A HREF="#lbAC">DESCRIPTION</A><DD>
<DT><A HREF="#lbAD">SYNOPSIS</A><DD>
<DT><A HREF="#lbAE">MODE</A><DD>
<DT><A HREF="#lbAF">OPTIONS</A><DD>
<DT><A HREF="#lbAG">SERIAL NO.|USB ID|IP|DEVNODE</A><DD>
<DT><A HREF="#lbAH">EXAMPLES</A><DD>
<DT><A HREF="#lbAI">NOTES</A><DD>
<DT><A HREF="#lbAJ">SEE ALSO</A><DD>
<DT><A HREF="#lbAK">AUTHOR</A><DD>
<DT><A HREF="#lbAL">REPORTING BUGS</A><DD>
<DT><A HREF="#lbAM">COPYRIGHT</A><DD>

