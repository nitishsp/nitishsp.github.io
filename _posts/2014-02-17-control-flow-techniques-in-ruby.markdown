---
layout: post
title: "Control Flow Techniques in Ruby"
---

Ruby has a variety of control flow techniques that let you control the execution of the program. Many of them (e.g. if, while, etc..) are similar to their counterparts in other programming languages. This article focuses on syntax and idiosyncrasies of Ruby control flow techniques.

Ruby provides **if..else**, **unless..else** and **case** constructs for conditional execution. `if..else` is same as other programming languages such as Python, Java, C. `unless` is opposite of `if`, its body gets executed if condition is false. If you are new to Ruby, you might find `unless` awkward to use, but as you code more and more in Ruby, you will intuitively start using unless. You can use `if !(condition)` or `if not condition` to achieve the same result as unless.

{% highlight ruby %}
>>   a = true
>>   b = false
>>
?>   if a
>>     puts "Inside IF a"
>>   elsif b
>>     puts "Inside ELSE IF b"
>>   else
?>     puts "Inside ELSE"
>>   end
Inside IF a
>>
?>   unless b
>>     puts "Inside UNLESS"
>>   else
?>     puts "Inside ELSE"
>>   end
Inside UNLESS
>> # This works too
>> puts "IF a is true" if a
IF a is true
>> puts "IF b is false" unless b
IF b is false

{% endhighlight %}

It is possible to assign value to a variable inside conditional test. In such cases, the return value of the assignment is considered while evaluating condition. Also, if a local variable is initialized in the body of a conditional it comes into existence even if conditional body containing the variable is not executed.

{% highlight ruby %}

>> a = 1
>> if (b = a)  # b gets a's value, which is interpreted as true.
>>   puts "True that!"
>> else
?>   t1 = 2
>> end
True that!
>>
?> p b
1
>> p t1 # t1 is nil, NOT undefined
nil
>> p t2
NameError: undefined local variable or method `t2' for main:Object

{% endhighlight %}

In the above example, variable `t1` does not throw `NameError`. This is because when Ruby parses the code, it sees `t1 = 2` and allocates memory for `t1`. So t1 exists as result of parsing process but it is not assigned any value.


`case..when` is similar to C or Java's switch case which one caveat. `when` does not use `==` to test equality, rather it uses `===` operator, which is syntactic sugar for method call `.===`. For most of the common Ruby classes such as `String`, `===` is same as `==`.

{% highlight ruby %}
case test_var
when 1
  puts "test_var is 1"
when 2
  puts "test_var is 2"
else
  puts "test_var is something else"
end
{% endhighlight %}

Ruby provides **loop**(for unconditional looping), **while** and **untill** (for conditional looping) and **for** (for looping through a list of value). Ruby has **break** and **next** keywords which allow the program to exit looping block or skip remaining part of the iteration respectively.

{% highlight ruby %}
## Ruby Looping constructs for printing 1 to 10
a = 1
loop do
  puts a
  a += 1
  break if a > 10
end

a = 1
while a <= 10
  puts a
  a += 1
end

# until is same as while but with reverse logic
a = 1
until a > 10
  puts a
  a += 1
end

# Similar to do..while in C, Java.
a = 1
begin
  puts a
  a += 1
end while a <= 10

# for is similar to its counterpart in Python
lst = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
for a in lst
  puts a
end

{% endhighlight %}

An **exception** in Ruby is a special kind of object of class **Exception** or its descendants. Ruby provides **rescue** clause to handle exceptions and **ensure** clause to make sure that certain code gets executed whether an exception is thrown or not. Ruby's `begin..rescue..ensure` is similar to Java's `try..catch..finally` block. You can raise exception programatically using **raise** keyword. While rescuing from an exception, you can catch the thrown exception object using special operator `=>`. Here is a contrived example that tries to explain the constructs.

{% highlight ruby %}

>> begin
?>   raise RuntimeError, "Problem occurred!"
>> rescue RuntimeError => e
>>   puts "Handled:"
>>   p e
>>   puts '-----------'
>>   # re-raising Exception to pass it up the call stack
?>   raise
>> ensure
?>   puts "I will get executed for sure"
>> end
Handled:
#<RuntimeError: Problem occurred!>
-----------
I will get executed for sure
RuntimeError: Problem occurred!
        from (irb):2
        ...

{% endhighlight %}

In the above example, `raise RuntimeError` is syntactic sugar for `raise RuntimeError.new`. You raise exception object, not class.

If Ruby's built-in exceptions do not suit your needs, you can define you own exception class by subclassing `Exception` or one of its descendants.

That's it for now. In the next article we will take a look at more powerful control flow constructs, code block.