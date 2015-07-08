---
title:  "Exploring Rails Guides - Views, Controllers and Routing"
---

In the last two posts I covered Active Record. In this post I will be covering views, controllers and routing.


Passing Local Variables to partials
------------------------------------
Avoid using instance variables directly in partials. Instead, pass them as locals. It's not unusual for a partial to be rendred from multiple views. If you use instance variables directly in partials, it is much harder to figure out the dependencies. Also, if instance variables are left unset, they return nil; whereas trying to use a local variable which you forgot to pass throws an exception.

{% highlight ruby %}
<%= render partial: "transactions", locals: items: @items %>
{% endhighlight %}

Every partial has a local variable with the same name as the partial. You can pass an object in to this local variable using the `:object` option. In the example below, within the customer partial, the `customer` variable will refer to `@new_customer`.

{% highlight ruby %}
<%= render partial: "customer", object: @new_customer %>
{% endhighlight %}

In addition to this, partials provide very useful features such as [rendering collections](http://guides.rubyonrails.org/layouts_and_rendering.html#rendering-collections), [spacer templates](http://guides.rubyonrails.org/layouts_and_rendering.html#spacer-templates). While rendering collections, if the collection is empty, render will return `nil`. So it's easy to provide alternative content.

{% highlight ruby %}
<%= render(@products) || "There are no products available." %>
{% endhighlight %}



Understanding Parameter Naming Conventions
-------------------------------------------
HTML forms do not know about any sort of structured data. All they know is name, value pairs. Rails uses some parameter naming conventions to convert HTML form data into mix of Arrays and Hashes. [Userstanding Parameter Naming Conventions](http://guides.rubyonrails.org/form_helpers.html#understanding-parameter-naming-conventions) will help you fully utilize this feature.


default_url_options
--------------------
You can define a method [default_url_options](http://guides.rubyonrails.org/action_controller_overview.html#default-url-options) in application controller to set some default options across the application. This method must return hash with keys as symbols. This is typically useful when setting applicationwide options such as locale.


Cookies
--------
Rails applications can store small amount of data on client machines using cookies that will be persisted across sessions. You can access cookie data using [cookies](http://guides.rubyonrails.org/action_controller_overview.html#cookies) method which behaves like a hash. Rails also provides methods to set signed or encrypted cookies. A signed cookies prevents users from tempering it's value. It is signed using your app's `secret_key_base`. Encryoted cookies are encrypted (in addition to signing) so that end users cannot read their value.


Log Filtering
--------------
Most of us are familier with [parameter filtering](http://guides.rubyonrails.org/action_controller_overview.html#parameters-filtering). There is another form of log filtering - [redirects filtering](http://guides.rubyonrails.org/action_controller_overview.html#redirects-filtering). It is used to filter out sensitive locations your app is redirecting to.



Shallow Nesting
----------------
When using RESTful routes, it's common to end up having deeply nested routes. You could use [shallow nesting](http://guides.rubyonrails.org/routing.html#shallow-nesting) to solve this issue to some extent. In shallow nesting, all the collection routes are still nested under the parent scope but all the member routes are not. [This](http://thepugautomatic.com/2013/05/unnesting-routes-in-rails/) article does a very good job of explaining shallow neesting.


Routing concerns
-----------------
Like their model and controller counterparts, routing concerns provide a way to share common code. With routing concerns you can define common routes that could be used inside other routes.

{% highlight ruby %}

concern :commentable do
  resources :comments
end

resources :articles, concerns: :commentable
resources :photos, concerns: :commentable
resources :videos, concerns: :commentable

{% endhighlight %}


Request-Based and Advanced Constraints
---------------------------------------
You can use methods of [request object](http://guides.rubyonrails.org/action_controller_overview.html#the-request-object), that return string, to constrain routes.

{% highlight ruby %}
get 'photos', to: 'photos#index', constraints: { subdomain: 'admin' }
{% endhighlight %}

For more [advanced constraints](http://guides.rubyonrails.org/routing.html#advanced-constraints), you can pass an object that responds to `matches?`.


Redirection
------------
Inside the router, you can use `redirect` helper to redirect to a path or URL. But be warned! this redirection is [a permanent redirect](http://getluky.net/2010/12/14/301-redirects-cannot-be-undon/).


Listing Existing Routes
------------------------
When you want to see routes and related info generated by the router, you do `rake routes`. If you don't want to run rake routes every time you want to see this info, you use some annotation gem. But there is another way. Visiting [http://localhost:3000/rails/info/routes](http://localhost:3000/rails/info/routes) will give you the same output as rake routes. Much better than rake routes or annotations.


Going through the Rails Guides again was fun. Even after using Rails for long, there was so much to learn from the guides. I haven't covered the advanced guides in this series, but reading the basic guides alone was a rewarding experience. Looking forward to diging deeper in Rails and gaining better understanding of how stuff works.
