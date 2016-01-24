---
title:  "Logging Excon HTTP request/response"
---

I have been using [Excon](https://github.com/excon/excon) for a while. It's great for interacting with JSON APIs. One thing I find missing in it is out of the box support for logging HTTP requests and responses. Though Excon has a debug mode which spits detailed request/response information to terminal, it's handy to have some of that in the log file. While Excon README doesn't mention anything about logging, [this](https://github.com/excon/excon/issues/64) closed issue provided some cues.

Excon supports [Active Support Instrumentation](http://edgeguides.rubyonrails.org/active_support_instrumentation.html), which allows developers to provide hooks which other developers may hook into. Excon adds some events to which you can subscribe. [Instrumentation](https://github.com/excon/excon#instrumentation) section of Excon README has more details on how to subscribe to its events. For logging request/response, we are interested in `excon.request` and `excon.response` events. So let's get started.

First you need pass instrumentor while creating Excon connection:

{% highlight ruby %}
connection = Excon.new(@host, instrumentor: ActiveSupport::Notifications)
{% endhighlight %}

Then you can log requests/responses by subscribing to Excon events and accessing the payload data:

{% highlight ruby %}
# config/initializers/notifications.rb

ActiveSupport::Notifications.subscribe('excon.request') do |*_, payload|
  Rails.logger.info("API Request: #{payload[:method]} #{payload[:path]}")
  Rails.logger.info("headers: #{payload[:headers].except('Content-Type', 'Host')}")
  Rails.logger.info("query: #{payload[:query]}") if payload[:query].present?
  Rails.logger.info("body: #{payload[:body]}") if payload[:body].present?
end

ActiveSupport::Notifications.subscribe('excon.response') do |*_, payload|
  Rails.logger.info("API Response: #{payload[:body]}")
end
{% endhighlight %}

That's it. Restart the server and Excon requests and responses will get logged.
