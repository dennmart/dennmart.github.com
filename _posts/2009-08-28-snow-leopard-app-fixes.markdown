---
layout: main
title: Snow Leopard App Fixes
---
# {{ page.title }}

Just like seemingly every Mac owner out there, I purchased [Snow Leopard](http://www.apple.com/macosx/) for my MacBook Pro. I actually woke up extra-early today and was at the [5th Avenue Apple Store](http://www.apple.com/retail/fifthavenue/) at 7:00 AM to buy it. As you guess, I was super-excited to get this running on my laptop.

I just installed it a few minutes ago, and it couldn't go smoother. The upgrade process from Leopard to Snow Leopard went without a hitch. However, as all operating system upgrades, regardless of how minor they are, some software just isn't going to want to cooperate with your shiny new toy. Apple has a list of [incompatible software](http://support.apple.com/kb/HT3258), but other software has some minor issues. Here are some that I encountered:

**MacPorts**

I had read so many messages on Twitter about developers mentioning that [MacPorts](http://www.macports.org/) didn't work with Snow Leopard. This worried me, as I use MacPorts quite a lot, especially since I want to learn lots of new things. Lucky for me (and others like me), I went to the MacPorts site this morning and saw that a new release of MacPorts, with Snow Leopard compatibility, was released recently. I simply downloaded the new version (version 1.8.0) and installed it over my previous installation, and all was good again.

***Edit:*** There are still some packages in MacPorts that refuse to compile. [Here's a list](http://trac.macports.org/wiki/snc/snowleopard) of the current status of the compatibility of some packages.

**MySQL**

MySQL works just fine with Snow Leopard. The problem is that in my case, the installation of Snow Leopard reset the paths I had set (the `/etc/paths` file), so none of the binaries was in my path. This was just a matter of adding the path where MySQL was (if you installed the Mac OS X package from [MySQL's official site](http://dev.mysql.com/), it should be installed in `/usr/local/mysql`).

**Textmate**

Since one of the early development releases of Snow Leopard in April, there has been a [ticket](http://ticket.macromates.com/show?ticket_id=0FDE7076) regarding using the Command and arrow keys to navigate text. I don't about everyone else, but whenever I'm coding, I hate to use the mouse or trackpad, and constantly use these types of shortcuts to navigate around. So this was a huge issue for me.

There's a temporary fix at the end in that ticket (*Snow Leopard Compatibility.zip*), which just install some macros to add this functionality again. It's just what's needed to get it working again. I think it's safe to assume that, like a million other things, this will be [fixed by Textmate 2](http://fixedbytm2.com/).

***Edit:*** On August 29, there was a new TextMate release (version 1.5.9 / revision 1509) which includes these fixes. This update can be automatically installed by going to *Textmate > Preferences* and going to the *Software Updates* section.

**Ruby / Ruby Gems**

I've mentioned before that I use [Jekyll](http://github.com/mojombo/jekyll/tree/master) to generate this blog. Just as I was about to send this post up to GitHub, I decided to check out if my Markdown formatting was correct. Instead, I got a nasty error message from Ruby Gems, stating that my [RDiscount](http://github.com/rtomayko/rdiscount/tree/master) gem wasn't working. When I tried to do a `gem update`, I got more errors.

Turns out there were some changes with the Ruby libraries that are installed with Leopard versus those installed with Snow Leopard. To fix this, just install the version of [Xcode](http://developer.apple.com/TOOLS/Xcode/) that's bundled with Snow Leopard (insert your Snow Leopard installation CD and look under the Optional Installs folder) to update all the libraries in the system.

***Edit:*** It seems like I forgot the small, tiny issue that Snow Leopard now uses 64-bit libraries. Since all previous Ruby-related libraries in your system were installed using 32-bit libraries in Leopard, none of the Ruby Gems will work. You can easily solve this using `gem pristine --all` to reinstall all your gems from the source cache.

Hopefully, that's the last of my incompatibilities. Should something else arise, I'll add more to this post as I find them.