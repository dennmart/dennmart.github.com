---
layout: main
title: MongoDB and MongoMapper - The Future?
---
# {{ page.title }}

In the past couple of weeks, I've been playing around with different [Document-Oriented Databases](http://en.wikipedia.org/wiki/Document-oriented_database). Specifically, I've been focusing on [MongoDB](http://www.mongodb.org/). In reality, all the document-oriented databases out there today are great, and it's a refreshing change of pace from relational databases and stuff like not having to worry about database schemas. However, I found MongoDB to feel closer to 'home', being someone who has strictly worked on relational databases since college. Also, it's blazing fast - Most benchmarks I've seen around the Internet show that MongoDB is much faster than other alternatives, including both document-oriented databases and relational databases.

Besides databases, I've also been playing with [Sinatra](http://www.sinatrarb.com/), a micro-framework in Ruby. I have a ton of ideas for small sites, where using a framework like Rails or Merb would be overkill. So I thought, *"I like Sinatra and MongoDB... Why not create an app using these two awesome tools?"* So I've been doing some toy projects (some stuff will be released to my GitHub account soon), and I've really been enjoying it so far.

For connectivity to MongoDB, there are a few tools out there. MongoDB has excellent [drivers](http://www.mongodb.org/display/DOCS/Drivers) for many different languages, both officially supported and community supported. There's an official [Ruby driver](http://www.mongodb.org/display/DOCS/Ruby+Language+Center), which will install itself as a gem. This will provide Ruby with most of the functionality to connect and interact with MongoDB.

However, to make things even easier, there are other tools that hook into the power of the MongoDB Ruby Driver. The one I'm using the most is [MongoMapper](http://github.com/jnunemaker/mongomapper). MongoMapper works sort of like [DataMapper](http://datamapper.org/), where you map your database fields to a class, and you can use these as method attributes to write and fetch data.

I'll update this post later whenever I release any project where I use Sinatra and MongoDB together.