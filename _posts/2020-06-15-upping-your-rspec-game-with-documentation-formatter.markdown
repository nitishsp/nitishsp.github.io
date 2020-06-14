---
title: "Upping your RSpec game with documentation formatter"
---

Ever since I came to know about it, I have always preferred using the **documentation formatter** when running a small set of specs. It lists the specs' output in an outline format.

So this:
{% highlight ruby %}
RSpec.describe 'A cup of coffee' do
  let(:coffee) { Coffee.new }

  it 'costs $1' do
    expect(coffee.price).to eq(1.00)
  end

  context 'with milk' do
    before { coffee.add :milk }

    it 'costs $1.25' do
      expect(coffee.price).to eq(1.25)
    end
  end
end
{% endhighlight %}


Outputs like this:

![RSpec documentation format output](/assets/images/posts/rspec-fd.png)

Pretty neat, isn't it?

Some advantages of the documentation formatter I have experienced:
* It gives an excellent **overview of functionality under test** if specs are properly structured using RSpec's `describe`, `context` and `it` blocks.
* It helps **spot mistakes in example and group descriptions**. Not just spelling and grammar mistakes - we often copy an existing spec, update the spec code, but forget to update the description. Using the documentation formatter and reading the output once before committing prevents such mistakes.
* The documentation formatter makes it easier to **spot redundant tests**.
* You can **combine it with --dry-run** to quickly get documentation-like output for your project - as long as you’ve taken care to phrase your example and group descriptions well.

We could set the documentation formatter as the default, but it is not very useful when running the entire suite. So you can configure RSpec to use  different formatters depending on the number of files to run:

{% highlight ruby %}
RSpec.configure do |config|
  config.default_formatter = config.files_to_run.one? ? 'doc' : 'progress'
end
{% endhighlight %}

This will use the documentation formatter if specs from at most one files will be run. Otherwise, it defaults to the progress formatter (which prints a green dot for each passing test). Of course, you can override this behavior by passing a formatter on the command line.

I am currently going through [Effective testing with RSpec 3](https://pragprog.com/titles/rspec3/) and found this nifty trick there. I am halfway through the book and I would definitely recommend it if you are looking to improve your understanding of RSpec. I am sure you will find something useful in it, no matter how many tests you've written using RSpec.