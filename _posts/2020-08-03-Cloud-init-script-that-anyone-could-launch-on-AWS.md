---
layout: post
title: "A Cloud-init script that anyone could launch on AWS"
date: 2020-08-03 21:24:00 -0800
---
<!-- start content -->
<div id="mw-content-text" lang="en" dir="ltr"><div>
I created a new <a rel="nofollow" href="http://lam2.duckdns.org/aws-lam2-Ubuntu-CloudInit.txt">aws-lam2-Ubuntu-CloudInit</a> script that anyone could launch on Amazon Web Services (AWS).
<div id="toc"><input type="checkbox" role="button" id="toctogglecheckbox" style="display:none" /><div lang="en" dir="ltr"><h2>Contents</h2><label for="toctogglecheckbox"></label></div>
<ul>
<li><a href="#A_web.2C_shell_and_proxy_server_built_from_a_Generic_Ubuntu_Server_image">1 A web, shell and proxy server built from a Generic Ubuntu Server image</a></li>
<li><a href="#I_can_launch_from_the_command_line_with:">2 I can launch from the command line with:</a>
<ul>
<li><a href="#LAM_AWS_command_line_options">2.1 LAM AWS command line options</a></li>
</ul>
</li>
<li><a href="#Prerequisites">3 Prerequisites</a>
<ul>
<li><a href="#AWS_Account">3.1 AWS Account</a></li>
<li><a href="#Unknown_level_of_knowledge">3.2 Unknown level of knowledge</a></li>
<li><a href="#You_can_launch_the_instance_from_the_AWS_Console">3.3 You can launch the instance from the AWS Console</a></li>
<li><a href="#Install_awscli_and_set_credentials_to_use_the_command_line">3.4 Install awscli and set credentials to use the command line</a></li>
</ul>
</li>
<li><a href="#LAM_AWS_resources">4 LAM AWS resources</a>
<ul>
<li><a href="#Use_a_predefined_security_group">4.1 Use a predefined security group</a></li>
</ul>
</li>
<li><a href="#What_is_missing">5 What is missing</a>
<ul>
<li><a href="#The_instance_doesn.27t_check_in_to_a_Dynamic_Domain_Name_Service">5.1 The instance doesn't check in to a Dynamic Domain Name Service</a></li>
<li><a href="#The_HTTPS_port_is_an_alternate_SSH_port">5.2 The HTTPS port is an alternate SSH port</a></li>
<li><a href="#No_MediaWiki.2C_No_HTTPS_site_defined_or_modules_loaded">5.3 No MediaWiki, No HTTPS site defined or modules loaded</a></li>
<li><a href="#No_mount_of_a_persistent_parallel_file_system">5.4 No mount of a persistent parallel file system</a></li>
</ul>
</li>
<li><a href="#Why_the_lam2_instance">6 Why the lam2 instance</a></li>
<li><a href="#This_page_was_retrieved_from_my_private_MediaWiki_instance">7 This page was retrieved from my private MediaWiki instance</a></li>
</ul>
</div>

<h2><span id="A_web,_shell_and_proxy_server_built_from_a_Generic_Ubuntu_Server_image"></span><span id="A_web.2C_shell_and_proxy_server_built_from_a_Generic_Ubuntu_Server_image">A web, shell and proxy server built from a Generic Ubuntu Server image</span></h2>
<p>The script builds a web, shell and proxy server from the Generic Ubuntu 20.04 Server image available at no additional charge over the cost of running the EC2 instance.
</p><p>All the source is on GitHub and the creation and storage of a custom Amazon Machine Image is not required.
</p><p>The web server is configured for three websites.  The default website would be displayed if a domain name is pointed to the IP address or domain name of the running instance.  A second website is configured if the browser gets to the site by IP address or the public-hostname assigned to the instance when it launched.  The third website is configured for some domain names I have control of.
</p>
<h2><span id="I_can_launch_from_the_command_line_with:">I can launch from the command line with:</span></h2>
<pre>aws ec2 run-instances --count 1 --image-id ami-09dd2e08d601bff67 \
--instance-type t3.nano --security-group-ids sg-3bda0647 \
--associate-public-ip-address --key-name aws-nwo-lam1 --user-data \
file:///var/www/aws/<a rel="nofollow" href="http://lam2.duckdns.org/aws-lam2-Ubuntu-CloudInit.txt">aws-lam2-Ubuntu-CloudInit.txt</a>
</pre>
<h3><span id="LAM_AWS_command_line_options">LAM AWS command line options</span></h3>
<dl><dt>Launch a single ec2 instance of the t3.nano type which is cheapest or of the t2.micro type which is part of the AWS Free Tier offering.</dt>
<dd>aws ec2 run-instances --count 1 --instance-type t3.nano</dd>
<dt>Get a public IP address and launch using my key</dt>
<dd>--associate-public-ip-address --key-name aws-nwo-lam1</dd>
<dt>Use a predefined security group</dt>
<dd>--security-group-ids sg-3bda0647</dd>
<dt>Use the latest Ubuntu Server image</dt>
<dd>--image-id ami-09dd2e08d601bff67</dd>
<dt>Specify the file with the user data&#160;</dt>
<dd>--user-data file://&lt;file name&gt;</dd></dl>
<ul><li>ami-09dd2e08d601bff67 This is the Ubuntu Server 20.04 LTS image for the US west 2 AWS region
<ul><li>If you want to run this in another region, use the appropriate image which you can find at the bottom of the Launch instance wizard page.</li></ul></li>
<li>aws-nwo-lam1 This is my key from AWS Identity and Access Management for the IAM user I want to be able to access the instance.</li>
<li>sg-3bda0647 This is a pre defined security group.</li>
<li>t3.nano This is a very small instance and you would want to use the larger t2.mico to be eligible for the Free Tier.</li></ul>
<h2><span id="Prerequisites">Prerequisites</span></h2>
<p>I would love to have someone test this script but can't think of who to ask.  I have been retired for over five years so don't have co-workers I could ask.  My friends and family are not really interested in what I do related to computers for fun.
</p>
<h3><span id="AWS_Account">AWS Account</span></h3>
<p>I have a root user account that I almost never use and a separate AWS IAM user for that account that I use for everything.  My user level access has access to a everything for the account including billing.  
</p>
<h3><span id="Unknown_level_of_knowledge">Unknown level of knowledge</span></h3>
<p>I don't even remember all the steps in setting up the two sets of credentials and granting the proper level of access to the user account so I never have to use the root account but I remember there were lots of guidelines on the web.
</p><p>This page is not a tutorial and is instead an example.  It is also documentation for myself and has enough that I can launch the instance with copy and paste and even do the check in to a Dynamic Domain Name Service steps I documented below.
</p>
<h3><span id="You_can_launch_the_instance_from_the_AWS_Console">You can launch the instance from the AWS Console</span></h3>
<p>You can launch the instance from the AWS Console from Services - EC2 - Instances - Launch Instance
</p><p>As of August 2020 you have to scroll down a ways to find the Ubuntu 20.04 image with Ubuntu 18.04, Ubuntu 16.04, Amazon, RedHat, Suse and many other images listed before the relatively new Ubuntu 20.04 image.
</p><p>You can paste the data passed as a file on the command line into the User data box in the advanced section of the Configure Instance Details page.
</p><p>You can even configure a new security group from the launch web interface although this is step six with many previous options to launch before seeing that page.
</p><p>I am sure an advanced user could launch one of these instances from this post.
</p>
<h3><span id="Install_awscli_and_set_credentials_to_use_the_command_line">Install awscli and set credentials to use the command line</span></h3>
<p>This awscli package is in the standard Ubuntu repositories.  The .aws/credentials file has key information for aws-nwo-lam1 to launch an instance in my VPC and the .aws/config file holds us-west-2 as the region value where the instance is launched.
</p>
<h2><span id="LAM_AWS_resources">LAM AWS resources</span></h2>
<h3><span id="Use_a_predefined_security_group">Use a predefined security group</span></h3>
<p>The security group definition controls the traffic within the Virtual Private Cloud and with the outside world.  I use the same security group definition for multiple images with only a limited number of inbound ports open.  The definition details are:
</p>
<ul><li>GroupName - aws-web-anywhere-alt-ssh-port</li>
<li>Inbound Port 22 TCP Rule - SSH from VPC - 172.31.0.0/20</li>
<li>Inbound Port 80 Custom TCP Rule - HTTP - 0.0.0.0/0</li>
<li>Inbound Port 443 Custom TCP Rule - HTTPS or SSH on an Alternate port - 0.0.0.0/0</li>
<li>Inbound Port 55520 Custom TCP Rule - SSH on an Alternate port - 0.0.0.0/0</li>
<li>Inbound Port 55593 Custom TCP Rule - IMAPS on an Alternate port - 0.0.0.0/0</li>
<li>Outbound All/All 0.0.0.0/0</li></ul>
<p>This security group definition allows web traffic on the standard ports from the public interface (0.0.0.0/0), Secure Shell on an alternate high numbered port and IMAPS on an alternate high numbered port.  The security group definition allows Secure Shell on the standard port.  The SSH SOCKS5 Proxy instance uses the same security group definition but is accepting Secure Shell traffic on the port that is normally used for Secure Web (HTTPS) traffic.  The security group definition does allow outgoing traffic from the server over the public interface.
</p>
<h2><span id="What_is_missing">What is missing</span></h2>
<h3><span id="The_instance_doesn't_check_in_to_a_Dynamic_Domain_Name_Service"></span><span id="The_instance_doesn.27t_check_in_to_a_Dynamic_Domain_Name_Service">The instance doesn't check in to a Dynamic Domain Name Service</span></h3>
<p>My main lam2 script checks in as <a rel="nofollow" href="http://lam2.duckdns.org">http://lam2.duckdns.org</a> which is one of four names that along with the aws public-hostname can be used to access the customized website.  The instance-type is also shown on the page as well as a link to the Cloud-init log.  I can use this page to toggle between the four Dynamic Domain Names I use for the group of servers I use to support the websites.
</p><p>From another instance in the same VPC I can use Secure Copy to get the private ubuntu resource archive to the new instance over the local area network with:
</p>
<pre>scp -p /mnt/efs/aws-lam1-ubuntu/ubuntu.t* &lt;local-ipv4&gt;:/home/ubuntu
</pre>
<p>On the new instance I can install these resources with:
</p>
<pre>tar -xzf ubuntu.tgz --directory /home/ubuntu
</pre>
<p>Check in and get a verbose response:
</p>
<pre>DDNS_NAME=lam2
echo url="https&#58;//www.duckdns.org/update?domains=${DDNS_NAME}&amp;token=$(cat \
~/.duckdns)&amp;verbose=true&amp;ip=" | curl -k -K -&#160;; echo \
" for ${DDNS_NAME}.duckdns.org IP address update"&#160;; echo
</pre>
<p>Upon successful completion the output with the verbose option will look like the following:
</p>
<pre>OK
69.178.104.164

UPDATED for lam2.duckdns.org IP address update
</pre>
<p>If the ubuntu resources were not installed the following error is reported:
</p>
<pre>cat: ~/.duckdns: No such file or directory
</pre>
<p>Alternately the Duck DNS token file can be created with:
</p>
<pre>echo {DuckDNStokenValue} &gt; /home/ubuntu/.duckdns
</pre>
<h3><span id="The_HTTPS_port_is_an_alternate_SSH_port">The HTTPS port is an alternate SSH port</span></h3>
<p>The main function of this AWS EC2 instance is to be a SSH SOCKS5 Proxy server on port 443.
</p><p>Port 443 is normally used for HTTPS so is likely to be available even when other ports are blocked.
</p>
<h3><span id="No_MediaWiki,_No_HTTPS_site_defined_or_modules_loaded"></span><span id="No_MediaWiki.2C_No_HTTPS_site_defined_or_modules_loaded">No MediaWiki, No HTTPS site defined or modules loaded</span></h3>
<p>My main lam1 Cloud-init script has the HTTPS site definition in a private repository.
</p>
<h3><span id="No_mount_of_a_persistent_parallel_file_system">No mount of a persistent parallel file system</span></h3>
<p>My main lam1 Cloud-init script utilizes an AWS Elastic File System (EFS) that all the instances can access as a persistent parallel file system.  Private git repositories and other shared resources are on that filesystem.
</p>
<h2><span id="Why_the_lam2_instance">Why the lam2 instance</span></h2>
<p>The lam2 instance was a candidate to be modified so that anyone could launch it precisely because it did not have html/Private, MediaWiki or the databases that I only support on HTTPS.
</p><p>I have had an AWS VPC since 2017 but early on added the private EFS and private S3 buckets as a source for initializing.
</p><p>This year I finally switched to git as my main VCS and decided to publish repos that did not need to remain private to GidHub because of it's value for documentation.  Once I had published the <a rel="nofollow" href="https://github.com/LAMurakami/aws#readme">aws</a> Linux Apache MariaDB in the cloud,
<a rel="nofollow" href="https://github.com/LAMurakami/no-ssl#readme">no-ssl</a> Default unsecure site configuration,
<a rel="nofollow" href="https://github.com/LAMurakami/ubuntu-etc#readme">ubuntu-etc</a>
Ubuntu Server 20.04 configuration changes for LAM AWS VPC EC2 instances
and
<a rel="nofollow" href="https://github.com/LAMurakami/arsc#readme">arsc</a> Lawrence A. Murakami at ARSC
repos to GitHub I realized I could launch the lam2 instance using only publicly available sources for the initialization.
</p>
<h2><span id="This_page_was_retrieved_from_my_private_MediaWiki_instance">This page was retrieved from my private MediaWiki instance</span></h2>
<p>Most of the pages I end up publishing to the web are a Static Copy of a page in my private MediaWiki instance.  In this case I use view source and copy the parts from to From: &lt;!-- start content --&gt; To: &lt;!-- end content --&gt; to a file and add Front Matter for Jekyll that will build the page to be published on GitHub Pages.
</p>
<!-- 
NewPP limit report
Cached time: 20200804052444
Cache expiry: 86400
Dynamic content: false
Complications: []
CPU time usage: 0.030 seconds
Real time usage: 0.031 seconds
Preprocessor visited node count: 56/1000000
Preprocessor generated node count: 0/1000000
Post‐expand include size: 0/2097152 bytes
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

<!-- Saved in parser cache with key wikidb:pcache:idhash:371-0!canonical and timestamp 20200804052444 and revision id 5254
 -->
</div></div><div>
Retrieved from "<a dir="ltr" href="https://ak17.lam1.us/A/index.php?title=A_Cloud-init_script_that_anyone_could_launch_on_Amazon_Web_Services_(AWS)&amp;oldid=5254">https://ak17.lam1.us/A/index.php?title=A_Cloud-init_script_that_anyone_could_launch_on_Amazon_Web_Services_(AWS)&amp;oldid=5254</a>"</div>
<!-- end content -->
