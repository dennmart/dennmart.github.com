---
layout: main
title: Sphinx Reindexing Gotcha
---
# {{ page.title }}

For the past year or so, I've always used [Sphinx](http://www.sphinxsearch.com/) for my full-text search needs. Along with [Thinking Sphinx](http://freelancing-god.github.com/ts/en/), it's one of the most simple, yet most powerful searching tools available in the Ruby world. Although there are other data search solutions (like [Solr](http://lucene.apache.org/solr/)) and other tools for using Sphinx under Ruby (like [UltraSphinx](http://blog.evanweaver.com/files/doc/fauna/ultrasphinx/files/README.html)), I prefer Sphinx and Thinking Sphinx for their ease of use.

As most full-text search tools out there, Sphinx needs your searchable data to be indexed, which will allow the search engine to work its magic. How often depends on your application's requirements. I use [delta indexing](http://www.sphinxsearch.com/docs/current.html#live-updates) for some of my data models, and I usually set a cron job to reindex every 30 - 60 minutes. I also have a [Capistrano](http://www.capify.org/index.php/Capistrano) task to reindex during deployment. This way, I can just deploy and any changes I've made in my models will be immediately indexed before the new version of the app comes up.

This week, however, I was having a problem during deployment to our Staging server. My indexing of Sphinx was failing, with the Thinking Sphinx error specifying a newly-created field in my database (the field was named 'visible' on a Rails model named 'Club') that I wanted to be included in the indexing:


    Cannot automatically map attribute visible in Club to an
    equivalent Sphinx type (integer, float, boolean, datetime, string as ordinal).
    You could try to explicitly convert the column's value in your define_index
    block:
      has "CAST(column AS INT)", :type => :integer, :as => :column

Everything was working smoothly on my development machine, so I was wondering what was up. After reviewing the deployment log for a while, I discovered that the problem was so simple. I had forgotten that I set up Capistrano to reindex Sphinx *before* running any pending database migrations, using Capistrano's `after "deploy:update_code"`method / task. So obviously, if the field isn't in the database, it can't be indexed!

The fix was simple - Reindex sphinx **after** any migrations are run. So I moved the reindexing task to be run before restarting the server (or touching the `tmp/restart.txt` file to restart all [Passenger](http://www.modrails.com/) processes), which is essentially the last step of Capistrano's `deploy` task, using `before deploy:restart`. It's really a simple thing, but I think it can be easily overlooked.