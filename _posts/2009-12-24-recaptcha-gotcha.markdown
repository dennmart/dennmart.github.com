---
layout: main
title: ReCAPTCHA - Quick Gotcha
---
# {{ page.title }}

On some sites I've worked on, I have used [ReCAPTCHA](http://recaptcha.net/) as a 'captcha' service to help minimize automated registrations on those sites. When using Ruby on Rails, I use the nice [ReCAPTCHA plugin](http://ambethia.com/recaptcha/) to set everything up for me.

This week, we did some updates to one of these sites, and after we checked around, we noticed that the places where ReCAPTCHA was used was all screwed up.

->![Messed-Up ReCAPTCHA](post_images/recaptcha_table_layout_fixed.png "ReCAPTCHA - All screwed up")<-

Now, we didn't catch this while testing, because we disable the captcha services in all environments except production. I did some digging around, and it turns out it that there was a recent CSS change by our designer on all tables:

{% highlight css %}
table {
  table-layout: fixed;
}
{% endhighlight %}

I started probing around this area because we didn't change any of the default styling for ReCAPTCHA, and it builds the whole section using HTML tables. So using the ever-so-awesome [Firebug](http://getfirebug.com/), I removed this CSS properly, and *voila*, ReCAPTCHA was looking all nice and beautiful, as it did before.

->![Fixed ReCAPTCHA](post_images/recaptcha_table_layout_auto.png "ReCAPTCHA - It's all beautiful again!")<-

Of course, the aforementioned `table-layout` property was there for a reason, and I didn't want to remove it from our CSS files without screwing everything up and causing more stress to our designer (she's had enough these past couple of weeks!). So after noticing that the ReCAPTCHA `<table>` tag had a class name itself, I just added the following CSS section of my own.

{% highlight css %}
.recaptchatable {
  table-layout: auto;
}
{% endhighlight %}

This fixed the problem at hand. So be careful when introducing CSS classes for an HTML element!