---
layout: main
title: MongoShort - URL Shortener using Sinatra and MongoDB
---
# {{ page.title }}

One of the things I've been working on recently at [BarterQuest](http://www.barterquest.com/) is adding some basic Twitter integration. After seeing Facebook implement [their own URL shortener recently](http://www.insidefacebook.com/2009/12/14/facebook-testing-new-url-shortener-fb-me/), I got the idea to make our own URL shortener, for use when sending Twitter messages. The main purpose is that I hope doing this will make users trust the URL more, since we'll only be generating these short URLs internally, meaning that the shortened URL really comes from us. It also makes for a fun little project. Seeing that I've been toying with [Sinatra](http://www.sinatrarb.com/) and [MongoDB](http://www.mongodb.org/) for quite a while now, earlier this week I whipped up a URL shortening server in a day or so.

Today, I christened this code as **MongoShort**, and released it to [GitHub](http://github.com/dennmart/mongoshort). MongoShort is an extremely simple shortening service (I only have two actions - One to create a shortened URL, the other to redirect a shortened URL to the full URL). Since this app is really simple and there are so many more fully-featured URL shorteners out there, I don't expect anyone to use this nearly as much as I do. I released MongoShort because I hope others can use it as a starting point to Sinatra, MongoDB and the awesome [MongoMapper](http://github.com/jnunemaker/mongomapper) gem, and perhaps serve as inspiration to use these tools.

I hope you can take a look at MongoShort and send some comments about it in my direction! I'm always up to learning more about what I used.