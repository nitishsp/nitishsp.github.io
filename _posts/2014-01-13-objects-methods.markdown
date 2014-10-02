---
title:  "Objects, Methods"
---

This week I learnt about some basics of objects and methods in Ruby, Here is the summary.

Depending on your Ruby version, the root of Ruby class hierarchy is **Object** or **BasicObject**. BasicObject was introduced in Ruby 1.9 and is parent of Object class. BasicObject is stripped down version of Object and contains very few methods. You can inherit from BasicObject to create class hierarchies independent of Ruby's built in hierarchy. For the rest of this blog post I will focus on Object and its descendants.

Each object has an unique object id. You can get an object's id using `object_id` or `__id__` methods. In standard Ruby (MRI), object id is same as VALUE which represents objects at C level. You may notice that object ids of true, false, nil and fixnums are constant across multiple runs. This is because of some clever performance optimization in MRI. You can read more about them [here](http://stackoverflow.com/questions/3430280/ruby-how-does-object-id-assignment-work), [here](http://www.oreillynet.com/ruby/blog/2006/01/the_ruby_value_1.html) and [here](http://www.oreillynet.com/ruby/blog/2006/02/ruby_values_and_object_ids.html)

Variables act as containers for object. Usually they store references to objects, so you have to be careful while manipulating objects. Consider the following example:
{% highlight ruby %}
>> a = "one"
>> b = a # copies content of variable, i.e. reference, not the actual object
>> puts a, b
one
one
>> a.replace("two") # method is called on the actual object
>> puts b
=> "two"
{% endhighlight %}
Some objects in Ruby (symbols, fixnums, false, true and nil) are stored directly in variables. When you assign one of these objects to a variable, variable stores the value itself rather than a reference. Regardless of this distinction, assignment statement always overwrites variables with whatever is there to the right of the `=` sign.

If you want to protect an object from being manipulated, invoke `freeze()` method on that object. Any attempts to modify a frozen object will result in runtime error. There is no way to unfreeze an object. If you wish to modify frozen object, you will have to create a copy of the object using `dup()` method and then manipulate it.

A method in Ruby may accept variables when called. Variables specified in method definition are called as formal parameters of the method and the values you supply while calling the method are called its arguments. When a method is called, the arguments passed to it are assigned to local variables which are visible inside method definition.

Methods in Ruby can take variable number of arguments using splat `(*)` operator and/or default values. When a method is called, Ruby tries to assign values to required parameters first and then to default valued parameters. If any arguments are left, they are packed into an array and assigned to the splat parameter otherwise the splat parameter is assigned an empty array `[]`. If number of arguments supplied is less than the number of required parameters, ArgumentError is raised. Splat operator can also be used while calling a method to unpack array.

{% highlight ruby %}
>> def mix_and_match(a, b=1, *c, d)
>>   p a, b, c, d
>> end

>> mix_and_match(1, 2)
1
1
[]
2

>> mix_and_match(1, 2, 3)
1
2
[]
3

>> mix_and_match(1, 2, 3, 4, 5)
1
2
[3, 4]
5

>> mix_and_match(1, *[2, 3], 4, 5)
1
2
[3, 4]
5
{% endhighlight %}

The optional parameters have to occur in the middle only. You can have required parameters on either side or both sides only. Also, you can have only one parameter with splat operator and you can't put it to the left of any default valued parameter.
{% highlight ruby %}
def example(a, b=1, c , *d, e) # invalid, required parameter in the middle
def example(a, *c , *d, e) # invalid, more than one splat parameter
def example(a,*b,c=1) # invalid, splat parameter to the left of default valued
{% endhighlight %}

Ruby 2.0 introduces keyword arguments and double splat operator.
{% highlight ruby %}
>>def foo(str: "foo", num: 42, **options)
>>  p str, num, options
>>end

>>foo
'foo'
42
{}

>>foo(check: true)
'foo'
42
{check: true}
{% endhighlight %}

That's it for this week.
