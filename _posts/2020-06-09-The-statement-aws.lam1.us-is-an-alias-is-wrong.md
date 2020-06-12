---
layout: post
title:  "The statement *aws.lam1.us is an alias for lamurakami.duckdns.org* from host is wrong!"
date:   2020-06-09 11:47:12 -0800
---
This phrase is returned when I use the `host` command on a linux system.  The `host` command is a DNS lookup utility and actually iterprets this argument as a domain name or an IP address that is to be looked up.

As I analyze my initial response I understand that there was a time when I didn't consider it wrong.  That was before what is now known as the [World Wide Web][World-Wide-Web].  The `host` command was developed by the Internet Software Consortium who also developed the BIND daemon decades before the web, browsers and the http protocol existed.

Today I think of a host name as the name of a website.  I then have to add that different protocols can lead you to different websites.  Apache2 and most web servers can support the https protocol which adds encryption and authentication as well as the less secure http protocol and can serve it from a different DocumentRoot just as it can have a different DocumentRoot based on the host name.  For me an alias is a host name that leads you to the same website, served from the same DocumentRoot.

This GitHub Pages site which uses a content delivery network has four different IP addresses associated with it's CNAME target.  Like many of my sites a CNAME target is used rather than an IP address because I don't control the internet IP address of a particular resource I use.  There is [long documented confusion][CNAME-alias-confusion] about what's a CNAME and what's an alias in a little different context.

I will use the label "CNAME target" instead of just CNAME and also avoid alias in this context which according to the long discussion is inaccurate.  In the case of this site if you use the CNAME target in a web browser with either the http or https protocols you are redirected to [https://github.lamurakami.com][github-lamurakami-com] which is a completely different website.  The two websites are related in that both were created for GitHub Pages to be posted from a public repository in my GitHub account.  They are also related because both are published by GitHub Pages to the lamurakami.github.io namespace even though a custom domain is also supported.  Any GitHub Pages I publish from a repo I created not associated with a project will be published to this namespace even if I specify a custom domain name.

The Jekyll template I am using has url and baseurl variables that essentially restrict the site to correctly operating only at the specified name.  When I viewed a GitHub pages site published to the default location of a sub directory without setting the baseurl variable I could get to the site but it was not displaying properly and internal links did not work.  I have also experienced this with MediaWiki.  GitHub Pages handles this with permanent redirects.

* [http://lamurakami.github.io][lamurakami-github-io] +s=> [https://github.lamurakami.com][github-lamurakami-com]
* github.lamurakami.com CNAME target lamurakami.github.io

* [http://lamurakami.github.io/blog][lamurakami-github-blog] +s=> [https://blog.lamurakami.com][blog-lamurakami-com]
* http://github.lamurakami.com/blog +s=> [https://blog.lamurakami.com][blog-lamurakami-com]
* blog.lamurakami.com CNAME target lamurakami.github.io

I an using the "+s=>" notation above to indicate redirects for both the http and https protocols.  This is actually three different redirects with Enforce HTTPS on the GitHub repository setting panel specifying the http:// to https:// redirect.  The GitHub Pages CNAME file which can be created/modified on the GitHub repository setting panel creates the redirect from the default namespace to the custom domain name and sets up the GitHub Pages content delivery network to correctly serve up http and https content for this host name.

Within the above context there are no aliases for the [https://github.lamurakami.com][github-lamurakami-com] and [https://blog.lamurakami.com][blog-lamurakami-com] sites.  There are redirects but I do not consider the from of a redirect to be an alias.

If you use what the `host` command says is an alias for blog.lamurakami.com the address bar of a browser you end up at a completely different website.

I do have some sites that are true aliases.  The [aws.lam1.us][aws-lam1-us] and [www.lam1.us][www-lam1-us] are both served by my AWS cloud server from the default site configuration for http traffic.  In the case of this site if you use the CNAME target in a web browser you are redirected to [http://lamurakami.duckdns.org][lamurakami-duckdns-org] which once again is a completely different website.

* http://aws.lam1.us CNAME target lamurakami.duckdns.org
* http://www.lam1.us CNAME target lamurakami.duckdns.org

The [http://lamurakami.duckdns.org][lamurakami-duckdns-org] website is created during the initialization of a new AWS EC2 instance to take over lam1.duckdns.org websites.  This page includes the ip-.compute.internal and ec2-.compute.amazonaws.com external domain names a public AWS EC2 instance it gets when launched.

My LAM AWS VPC currently supports a number of websites using four different Dynamic Domain Name Service subdomains.  The websites are served from one to four different AWS EC2 server instances each with it's own public IP address.

All of this is related to me adding a page to the blog.lamurakami.com site about my sites.  It's my first website using Jekyll and Liquid and I already created a sitemap page and was thinking about a lam_sites collection to build a page.  It was in thinking about the structure I would use and the relationships that I would want in the structure that I decided [aws.lam1.us][aws-lam1-us] is NOT an alias for [lamurakami.duckdns.org][lamurakami-duckdns-org] and I would prefer "aws.lam1.us has a CNAME target of lamurakami.duckdns.org".  If I find the source for the `host` command and it's on GitHub, I could clone, branch, make the change, and create a pull request to see if I could get the change implemented.

While I was doing this I realized my website built with a template that primarily supports posts should have more than one post.

[World-Wide-Web]: https://en.wikipedia.org/wiki/World_Wide_Web
[CNAME-alias-confusion]: https://en.wikipedia.org/wiki/CNAME_record#Possible_confusion
[github-lamurakami-com]: https://github.lamurakami.com
[lamurakami-github-io]: http://lamurakami.github.io
[blog-lamurakami-com]: https://blog.lamurakami.com
[lamurakami-github-blog]: http://lamurakami.github.io/blog
[aws-lam1-us]: http://aws.lam1.us
[www-lam1-us]: http://www.lam1.us
[lamurakami-duckdns-org]: http://lamurakami.duckdns.org
