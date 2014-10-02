---
title:  "Ruby Classes"
---
In Ruby, classes are instances of class **Class**. Since they are objects, they respond to messages sent using dot notation. Classes are special objects that have ability to spawn new objects. Classes are usually defined using `class` keyword with a constant as name. Classes can inherit the behavior (methods) of another class using inheritance. Ruby classes can have only one parent i.e. multiple inheritance is not allowed. You can reopen already defined classes and add methods to them.

{% highlight ruby %}
>> class A
>>   attr_reader :answer
?>   def initialize
>>     @answer = 42
>>   end
?>   def A.foo
>>     42
>>   end
>> end
>>
?> class B < A
?> end
>> A.foo == B.foo
=> true
>> A.new.answer == B.new.answer
=> true
{% endhighlight %}

Since classes are instances of class `Class`, defining class method means defining singleton method on `Class`'s objects. In the above example class `A` is an object of class `Class`. `A.foo` defines a singleton method on object `A` which is called as class method. Instead of `A.foo`, you could also use `self.foo`.

Ruby allows you to create **anonymous classes** using `Class.new`. `Class.new` accepts a block in which you can define class and instance methods.
{% highlight ruby %}
>> c = Class.new do
?>   def say_hello
>>     puts "Hello!"
>>   end
?>   def self.say_bye
>>     puts "Bye!"
>>   end
?> end
>> c.say_bye
Bye!
>> c.new.say_hello
Hello!
{% endhighlight %}

Classes have a special method `initialize` which is called every time a class is instantiated. It is typically used to set values of instance variables. Names of instance variables begin with `@` symbol. Each object contains its own copy of instance variables which store state of the object. They can be accessed from any instance method of the class. Instance variables are private and cannot be accessed from outside of the class without getter and setter methods. Ruby provides `attr_reader`, `attr_writter`, `attr_accessor` and `attr` methods (defined in the `Module` class) which automagically create basic getter/setter methods. Ruby provides syntactic sugar for calling setter methods. So instead of `object.attribute=(value)`, you can use `object.attribute = value`. Be careful with setter methods, they don't return result of the last expression. Instead, they return whatever’s on right-hand side of the `=`. This behavior is consistent with variable assignment.

In Ruby, name of a **constant** begins with uppercase letter. You can assign objects to constant in the same way as variable assignment. Reassigning already assigned constant is possible but results in a warning. If you try to modify object referred by a constant, ruby doesn't complain.
{% highlight ruby %}
>> Constant = [1, 2, 3]
=> [1, 2, 3]
>> Constant = [1, 2, 3, 4]
(irb):25: warning: already initialized constant Constant
=> [1, 2, 3, 4]
>> Constant << 5
=> [1, 2, 3, 4, 5] # no warning
{% endhighlight %}

Constants defined in a class are accessible from class as well as instance methods of that class. From outside of the class, constants can be accessed by using double colon (`::`).
Ex. `Math::PI`.
