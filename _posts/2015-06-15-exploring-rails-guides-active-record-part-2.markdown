---
title:  "Exploring Rails Guides - Active Record - Part 2"
---

In the previous post I covered Migrations, Validations and Callbacks. In this post I will be covering Associations and Query Interface guides.


inverse_of
-----------
It's normal for an association to work in two directions. For example, an article has_many comments and a comment belongs_to an article. By default, Active Record doesn't know about the connection between these associations. This can lead to two copies of an object getting out of sync. To prevent this use [inverse_of](http://guides.rubyonrails.org/association_basics.html#bi-directional-associations).

If you are using Rails 4.1+ you probably don't have to worry about this. Rails will automatically detect inverse associations using simple heuristics. For complex associations, you will have to define them yourself.


belongs_to counter_cache
-------------------------
Often, in has_many association, you need to cache number of belonging objects. For example, if you are building a blog application and displaying a list of articles on the home page, you would often need to display count of comments on each article. To avoid extra db calls, you would store the number of comments in article itself and update it every time a comment is added or removed from the article. Active Record provides [counter_cache](http://guides.rubyonrails.org/association_basics.html#counter-cache) option on belongs_to association, which will simplify this for you.


dependent - restrict_with_exception and restrict_with_error
---------------------------------------------------------------
The `dependent` option determines what happens to associated objects when the owner is destroyed. The two most popular options are `:destroy` and `:delete`. Almost every Rails tutorials mentions these options. But often you would want to prevent the owner from getting destroyed if there are any associated objects. `:restrict_with_exception` and `:restrict_with_error` serve this purpose. The former raises an exception, while the latter adds a validation error to the owner object.


When are Objects Saved?
------------------------
There are certain nuances regarding when objects are saved when assigned to an association. Rails guide does very well to explain this for [belongs_to](http://guides.rubyonrails.org/association_basics.html#belongs-to-association-reference-when-are-objects-saved-questionmark), [has_one](http://guides.rubyonrails.org/association_basics.html#has-one-association-reference-when-are-objects-saved-questionmark), [has_many](http://guides.rubyonrails.org/association_basics.html#has-many-association-reference-when-are-objects-saved-questionmark) and [has_and_belongs_to_many](http://guides.rubyonrails.org/association_basics.html#has-and-belongs-to-many-association-reference-when-are-objects-saved-questionmark) associations.


Association Callbacks
----------------------
In addition to normal [callbacks](http://guides.rubyonrails.org/active_record_callbacks.html#available-callbacks), Active Record also provides callbacks that are triggered by association events such as, adding/removing objects from an association. There are four [association callbacks](http://guides.rubyonrails.org/association_basics.html#association-callbacks) available.


find_each and find_in_batches
------------------------------
Many times you need to fetch large number of records from database and iterate over them. It's not efficient to fetch a large number of records in one go. You might not even have enough memory to hold all the objects in memory. Rails provides two methods `find_each` and `find_in_batches` that fetch records in batches. The detailed explanation could be found in [Rails Guides](http://guides.rubyonrails.org/active_record_querying.html#retrieving-multiple-objects-in-batches).


Nested hash conditions
-----------------------
Ever wanted to perform query on attributes of associated objects and ended up writing it like this:

{% highlight ruby %}
Author.joins(:articles).where("articles.author = ?", author)
{% endhighlight %}

I had been doing this simply because I didn't know I could use nested hash like this:

{% highlight ruby %}
Author.joins(:articles).where(articles: { author: author })
{% endhighlight %}

Much cleaner!


not conditions
---------------
I used to write NOT SQL queries by passing sql string to where:

{% highlight ruby %}
User.where('name != ?', 'Gabe')
{% endhighlight %}

With Rails 4.0, this can be done by using `where.not`

{% highlight ruby %}
User.where.not(name: 'Gabe')
{% endhighlight %}

It's not just cleaner; It provides some [additional features](https://robots.thoughtbot.com/activerecords-wherenot) too.


Overriding Conditions
----------------------
Sometimes you need to remove/override conditions from an already built query. One example of this would be using `unscoped` to remove the default scope. Active Record provides [5 more methods](http://guides.rubyonrails.org/active_record_querying.html#overriding-conditions) for this purpose: `unscope`, `only`, `reorder`, `reverse_order` and `rewhere`.


Null Relation
--------------
Active Record provides `none` method which returns an empty `ActiveRecord::Relation` object without firing any database queries. Use case for this is well illustrated in the [Rails Guides](http://guides.rubyonrails.org/active_record_querying.html#null-relation)


create_with
------------
When using `find_or_create_by` often you would want to set some attributes for the new record but you don't want to include them in the query. One way to achieve this is by passing a block to `find_or_create_by` and setting attributes inside the block. Active Record provides a method, [create_with](http://guides.rubyonrails.org/active_record_querying.html#find-or-create-by) to do the same.


With this, I have covered Rails Guides related to Active Record. In the next article I will explore views and controllers.
