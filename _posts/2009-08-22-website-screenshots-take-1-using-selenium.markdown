---
layout: main
title: Website Screenshots - Take 1 (Using Selenium)
---
# {{ page.title }}

As part of a small project I want to do, I want users to be able to enter a URL and have a screenshot of the site be saved with the entry, just like many sites out there. However, when I started looking for information on how to do this, I rapidly found that if you want to do it yourself, there's really no easy solution. It's especially difficult if you're planning on running the application on a remote headless server (which is what I'll do). It seems that the easiest route to take is to use one of the many websites that provide this service for you (like [Thumbalizr](http://www.thumbalizr.com/) and [WebShotsPro](http://webshotspro.com/), among many others). There's just a slight problem:

*  I don't want to rely on third-party services.
*  I don't want to spend any cash on this.
*  I don't want to use a free service which appends a watermark on the generated image.

That means I'm stuck with rolling my own. I don't mind this, since I love doing these types of experiments (as time permits, of course).

I was surprised when I read that the testing framework [Selenium](http://seleniumhq.org/) could actually help me do this. It turns out that Selenium has a [capture_screenshot](http://release.seleniumhq.org/selenium-remote-control/1.0-beta-2/doc/ruby/classes/Selenium/Client/GeneratedDriver.html#M000220) method that does exactly what it says - capture a screenshot of the currently-opened site you opened to test. It seemed like a good alternative to try out.

The issue is that Selenium can't run by itself in a headless environment. You either have to run the Selenium server in some sort of desktop environment, or use a tool such as [Xvfb](http://en.wikipedia.org/wiki/Xvfb) that uses a virtual framebuffer to handle all the graphical needs of the application. I didn't take the Xvfb route, although I plan to experiment with it later on. I have a Mac Mini running Ubuntu (Desktop Edition) at home, so I downloaded Selenium ([Selenium-RC](http://seleniumhq.org/projects/remote-control/), to be more specific) there to do the test.

The Selenium server uses the [Jetty HTTP server](http://www.mortbay.org/jetty/), so to begin, I needed to install the [Java Runtime Environment](http://www.java.com/en/download/manual.jsp) for Linux to actually run the server. **Note:** I first used the [GNU Java compiler](http://gcc.gnu.org/java/), and while it could start the Selenium server, it would crash for any other operation, so don't use it.

Also, make sure you have the browser you want to use installed. Ubuntu Desktop Edition comes with Firefox by default, so I didn't have any issues. But remember that headless server environments don't install any browsers (perhaps maybe [lynx](http://lynx.isc.org/), but you don't want to take screenshots with that browser, do you?). You'll need some browser installed for Selenium to run.

Once all this is done and you uncompressed the Selenium-RC archive, go to the *selenium-server* directory you can start the Selenium server with a simple `java -jar selenium-server.jar`. Some info from the Jetty server will show up, and as long as it doesn't crash back to the prompt, you should be running.

Now came the experiment - I'm going to use [Sinatra](http://www.sinatrarb.com/) for my project, so I installed the [Selenium Gem](http://selenium.rubyforge.org/) to use with Selenium with Ruby. I wrote a short Ruby script that starts an instance to connect to the Selenium server, open a URL in the firefox browser and use the `capture_screenshot` method I mentioned above to grab the screenshot. Here's the code, which should be a bit self-explanatory:

{% highlight ruby %}
require 'rubygems'
require 'selenium'

selenium = Selenium::SeleniumDriver.new("localhost", 4444, "*firefox",
                                        "http://www.google.com/", 10000)

selenium.start
selenium.open("http://www.google.com")
selenium.capture_screenshot("google_screenshot.png")
{% endhighlight %}

This produced the following screenshot:

->![Selenium Screenshot](http://img195.imageshack.us/img195/5299/googlescreen.jpg "Selenium Screenshot")<-

Yep, it took the screenshot of my *entire desktop*. I didn't dedicate too much time to experiment with it any further, because I decided against using this approach. I don't want to have a somewhat heavyweight Java process like the Selenium and Jetty HTTP servers running solely for capturing screenshots. It seems like a bit too much for a minor feature of what I plan to do in my project. Oh well.

Next up, testing with [khtml2png](http://khtml2png.sourceforge.net/) is coming up next.