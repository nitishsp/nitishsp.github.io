---
title:  "Ruby Modules"
---

Modules are great for code organization. They are typically used for organizing related code together and mixing them in other classes and modules when required. All modules are instances of **Module** class. Modules are similar to classes. In fact, class `Module` is superclass of class `Class`. Unlike classes, modules cannot be instantiated. They don't support inheritance either. A module is defined using **module** keyword.

{% highlight ruby %}
module A
  # module body
end
{% endhighlight %}

Modules consist of methods, constants, classes and other modules. Methods in a module can be of two types: **module methods** or **instance methods**. Module methods are defined by using self keyword. They are basically singleton methods on module object and can be accessed directly using module name. Module's instance methods can be used by other modules and classes by including or extending module. The **include** method makes all instance methods of the included module available as instance methods whereas the **extend** method makes all instance methods available as singleton methods of the class or module from which it is called.

{%  highlight ruby %}
>> module A
>>   # instance method
>>   def method1
>>     puts "In method 1"
>>   end
>>
>>   # Module method
>>   def self.method2
>>     puts "In method 2"
>>   end
>> end
>>
?> module B
>>   include A
>> end
>>
?> class C
>>   include B
>> end
>>
?> class D
>>   extend B
>> end

# Calling module method
>> A.method2
In method 2

# Calling included method
>> C.new.method1
In method 1

# Calling extended method
>> D.method1
In method 1
{% endhighlight %}

From the example above, you can see that a method need not be defined in the class of the object on which it is called. It could be defined in any of the ancestor classes or in modules included by those classes. When you call a method on an object, it looks for that method at the following places:
1. Its class
2. Included modules
3. Parent class
4. Modules included by parent class

and so on... all the way to the `BasicObject` class.

When two or more methods have the same name, the one defined later gets called. If the same method is defined in two or more included modules, the one in the most recently included module gets called. Including a module more than once has no effect.

If method is not found, the interpreter sends a special message **method_missing** to the receiver along with the symbol of non-existent method and array of parameters passed to the method.

It is possible to call an overridden method using **super**. You can use super keyword inside the body of a method definition to pass the method call up the lookup chain. When called without arguments e.g. `super`, it passes all the parameter received by the method from which it's called. You can also explicitly pass 0 or more parameters e.g. `super()` or `super(a, b)`.

Ruby allows you to nest classes inside modules or modules inside classes. Further, you can encapsulate code in both modules and classes in a similar way. There is no particular rule to consider while picking classes or modules for your program's architecture. You have to consider the limits of both the constructs and use them in a sensible way.