---
layout: main
title: JSON Gem (1.1.9) Weirdness with Rails
---
# {{ page.title }}

Over the weekend, the server we use in our office for staging / testing purposes died due to a faulty battery. I replaced it in a hurry, but I didn't use the same software versions that we were using previously. Since we didn't tinker too much with the testing server, the gems weren't all up to date. However, this new server grabbed all the most recent gems while installing (which is done by default).

Everything was running fine, until one of our interns showed me some very weird Javascript rendering. We have a list displaying categories that does an AJAX call when a category is selected. In the back-end, we check if the selected category has any sub-categories. If it does, we render a new list with the sub-categories, and so on until the last sub-category is selected. Part of the menu uses the `update_page` helper. It's been working fine for a year now without any problems... Until it hit the new testing server. Instead of doing the proper rendering on the page after the AJAX call, it did this:

->![Messed-Up Menu](http://img86.imageshack.us/img86/2162/catjsprint.png "My Menu - Javascript and all")<-

It actually printed out the Javascript code instead of rendering it properly. After a few hours searching for possible solutions (everything from different Ruby versions to using different servers - Mongrel, Thin and Passenger) to nail down the problem, I finally narrowed it down to one thing: The latest version of the [JSON gem](http://flori.github.com/json/) for Ruby. The servers where the menu was working properly had version 1.1.7 installed; The new testing server had version 1.1.9 installed. After uninstalling the latest version and downgrading to version 1.1.7, my menu started working again.

I just discovered this a few minutes ago, so I haven't figured out why this gem was interfering with the generated code from the Rails helpers. The only clue I have is that when I had the latest JSON gem installed, the generated Javascript code from the `update_page` helper wasn't being escaped properly (in particular, any forward-slashes in the generated code wasn't being escaped properly using back-slashes). Once I installed the older version, all slashes were properly escaped. I'll do some more digging and report any findings here.