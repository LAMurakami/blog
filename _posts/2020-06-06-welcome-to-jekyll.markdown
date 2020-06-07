---
layout: post
title:  "My first static websites built with Jekyll"
date:   2020-06-07 11:46:40 -0800
categories: jekyll update
---
My first [LAMurakami GitHub Page][lamurakami-github-pages] publised to the GitHub Pages service was `raw html` from the master branch of my `lamurakami.github.io repo` based on [GitHub Pages documentation][github-pages-docs].  After that I published a page from the /docs folder of the master branch of a repo that had been created 5 years ago.

I then went on to a repo that had been forked from another 5 years ago.  For this GitHub Page I created a gh-pages branch, specified the cayman Jekyll theme and the datasharing.lamurakami.com custom URL, all from the GitHub web interface.  Since I had created a `new` branch I decided it was an opportunity for [my first git pull request][lamurakami-datasharing-pull].  To get this to be a branch with no conflicts I had to rebase both the master and gh-pages branches.

## Welcome to Jekyll!

This site was built on my laptop with `jekyll new` after installing `jekyll`, `bundler`, `gems`, `ruby-dev`, and `ruby-all-dev` from the default Linux Mint / Ubuntu repositories.

It is possible that not all these packages are needed but I had issues following the Jekyll quick start guide that tells me to run `bundle exec jekyll serve` after installing Jekyll with RubyGems.  It took me a long time to find that I could just use `jekyll serve` on my system.  I very much want to use packages installed from the default repositories rather than building from source or using some other package manager that would not be covered in my update process.  I found a lot of Ubuntu users had the same issue and a lot of Jekyll experts that were rude and condescending to users that did not use the RubyGems process to install becasue they saw Jekyll in the repository and installed it that way.

The original title to this post was "Welcome to Jekyll!" on 6/6/2020 which matches the `2020-06-06-welcome-to-jekyll.markdown` filename.  I have modified the title and date for the post and left the file name unchanged.

I modified the `_config.yml` file to change the `title`, `email`, `description`, `url`, `baseurl`, `github_username` values and delete the `twitter_username` variable definition.  These values are used in the header and footer of all the generated pages for the site.

I modified the index.html file and deleted the feed.xml file to remove the RSS feed link on the main page of the site.  I might want to add this back in later once my blog has more than one post.

I modified the `about.md` file adding links to the source code on GitHub for this page and my LAMurakami GitHub Pages page in the style used for the Jekyll links already on the page. 

I modified the `_sass/_base.scss` file to add color for H1 and H2 headers and a background color when links are hovered over matching the style on many of my pages.

I used `jekyll serve` to test the site at http://127.0.0.1:4000 on my local machine and `jekyll build` before the first commit to GitHub.

[lamurakami-github-pages]: https://github.lamurakami.com
[github-pages-docs]: https://help.github.com/categories/github-pages-basics
[lamurakami-datasharing-pull]: https://github.com/jtleek/datasharing/pull/688
