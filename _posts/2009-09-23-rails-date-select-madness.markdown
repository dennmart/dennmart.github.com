---
layout: main
title: Rails date_select Madness
---
# {{ page.title }}

I love using the Rails `date_select` helper. It's wonderful how one simple line of code can automatically generate all you need for your users to select a month, day and year. However, I have one small annoyance with it. A user can select an invalid date (like *February 30* or *September 31*), and Rails will automatically roll over the additional dates, instead of actually marking that field / attribute as invalid. For example, if the user selected *February 31* and submitted the form, Rails would happily set the date to *March 3*.

Now, that really isn't an issue for alarm on my part, and in most cases I would not handle these types of mistakes (or toying around, which is most likely what I suspect if this occurs). But one of the apps I'm working on required that the user should not be able to enter these bogus dates.

The easiest way I found to do this was to do a quick check using Ruby's [Date class](http://www.ruby-doc.org/core/classes/Date.html) with the selected values. The `Date` class raises an `ArgumentError` if you try to initialize it with a bogus date. I put this in my controller action where the information, including the selected date, was going to be saved:


{% highlight ruby %}
def create
  @user = User.new(params[:user])

  selected_day = params[:user]['birthdate(1i)'].to_i
  selected_month = params[:user]['birthdate(2i)'].to_i
  selected_year = params[:user]['birthdate(3i)'].to_i
  Date.new(selected_day, selected_month, selected_year)
  
  # Other logic here, including saving the record and redirecting on
  # success, or rendering the form on failure.
rescue ArgumentError
  @user.errors.add(:birthdate, 'is an invalid date')
  # Clear the birthdate, so it doesn't show the rolled-over date in the view.
  @user.birthdate = nil
  render :action => 'new'
end
{% endhighlight %}

In the code above, it does all the regular Rails stuff of creating a new object with the form data. However, I added an additional statement, which is to create a new `Date` object. I don't use this `Date` object for nothing I initialize it. I simply initialize the object so that if an incorrect date is selected in the `date_select` helper, it will raise the `ArgumentError`, where I then handle the error properly. It will render the form again, displaying the standard Rails error message indicating that the birthdate is invalid.

I avoided using plugins, since I didn't have many cases where it warranted using an external library. I'm also sure I could monkey-patch this, so that all my `date_select` helpers worked this way, but I only had it in two places. Is there some other way of doing this? There might be. But judging by the search results I encountered while looking into this, I don't think anyone cares if the user enters bogus dates.