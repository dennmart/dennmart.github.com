---
layout: main
title: jQuery and Rails
---
# {{ page.title }}

Ruby on Rails, by default, includes the [Prototype](http://prototypejs.org/) Javascript library. Along with [Scriptaculous](http://script.aculo.us/), it works pretty well with your website Javascript and effects needs. I've been using Prototype for a few years now, and I really haven't had any major issues. However, it seems like all the cool websites out there are using [jQuery](http://jquery.com/) instead. Now, why is this happening?

I haven't done any extensive research or anything like that, but I think it's because of one reason: [Plugins](http://plugins.jquery.com/). jQuery has a ton of plugins for just about anything. Need a cool slider effect for pictures, or maybe something to help ease the pain of form validation? There's something done for jQuery, ready to be placed in your app to get you up and running.

So, what's a Rails developer to do? Rails has a ton of helpers like `form_remote_for` and `visual_effect` that rely on Prototype and Scriptaculous, plus if your project already has a lot of custom Javascript code, most likely it will use these two libraries. You're not really required to use Prototype, as David Heinemeier Hansson [explained previously](http://www.loudthinking.com/posts/32-myth-3-rails-forces-you-to-use-prototype). But wouldn't it be cool to be able to use the Rails helpers we've all been used to all this time?

Thankfully, there's an excellent plugin called [jRails](http://ennerchi.com/projects/jrails), which makes these Rails helpers use jQuery instead of Prototype. The cool thing is that it works pretty well right out of the box. Also, if you already have a lot of custom Javascript around that can only work with Prototype, and you don't want to spend time fixing it, you can have both jQuery and Prototype living under the same roof harmoniously, thanks to jQuery's [noconflict](http://docs.jquery.com/Core/jQuery.noConflict) option.

I've been using this plugin for a few days, and so far nothing has been broken. Now I can start experimenting with these awesome plugins that I've seen in use around the Internet recently. Hopefully Rails 3 will be a bit more flexible as far as using alternative Javascript libraries is concerned.

**Update:** After writing this post, [Smashing Magazine](http://www.smashingmagazine.com/) wrote an [awesome post with 50 useful jQuery techniques](http://www.smashingmagazine.com/2009/08/23/50-useful-new-jquery-techniques/). Posts like these are another reason why jQuery seems to be above all other Javascript libraries.
