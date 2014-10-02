---
title:  "Basic Ruby literacy"
---

I am trying to gain better understanding of Ruby (and Rails). [The Well-Grounded Rubyist](http://www.manning.com/black2/) is my primary source of learning. This is the gist of things I learnt this weekend.

Lets start with irb. **irb** or **Interactive Ruby Shell** is command line REPL tool that ships with ruby. I prefer starting irb with `--simple-prompt`, a command line options which results in a concise prompt. irb a great for toying with the language, for anything useful, you would save the ruby code in **.rb** file and run it using **ruby interpreter**. The ruby interpreter provides a lot of command line flags. The flag `-e` allows us to provide inline script to the interpreter, Ex. `ruby -e 'puts 2 ** 4'`. Another useful combination of flags is `-cw`. `-c` causes ruby to check the syntax of ruby program without executing it and `-w` enables verbose mode without printing the version information.

When running ruby program from files, **gets** is used to read a line from standard input stream. There are 3 functions to write to standard output: print, puts and p. **print** writes the given object to standard output stream. **puts** is similar to print but appends a newline character at the end if its not already present. **p** outputs inspect string of object. `p <object>` is same as `puts <object>.inspect`.

In ruby only `nil` and `false` are **falsy values**, all other objects (including 0 and empty string) are **truthy values**. `#` is used for **comments**. Although various constructs are available for [multiline comments](http://stackoverflow.com/a/2991254), `#` is the most preferred method.

Ruby has a modest list of **identifiers**: Variables, Constants, Keywords and method names. There are 4 types of variables: Local variables (start with a lowercase letter or _ and consist of letters, underscores and or digits), Instance variables (start with single @ sign), Class variables (start with @@) and Global variables (start with $). Constants begin with an uppercase letter. Keywords are reserved words in ruby.

In ruby almost **everything is an object**. Objects are represented by their literal form or by the variables that refer to them. Each object is capable of understanding a set of messages. Each message that an object understands corresponds directly to a method. If there is no corresponding method, objects can try to interpret the message on the fly and try to make sense of it. The **dot** operator (.) is the most common way of sending messages to an object. The message to the right of the dot is sent to the object on the left. Ex. In `"foobar".upcase`, the message upcase is sent to the string "foobar". Like other languages with classical inheritance, a Ruby object is an instance of exactly one class. But in ruby, objects can acquire new behaviours that were not defined in their class.

While working with ruby code in multiple files, you are often required to load/execute content of a program from within another ruby program. Ruby provides **load** and **require** methods for this purpose. A call to load always loads the file whereas require loads the file only once. require doesn't need file extension. This allows you to load extensions written in c and ruby in the same way (because file extension is not needed). Unless absolute path is given, require and load look for the specified file in load path (a list of directories). Ruby 1.9.2 added another method **require_relative** which allows you to load a file relative to the file containing require_relative.


You can get information about your ruby installation using a library package **rbconfig**. The information is available in hash data structure bound to a constant, `Config::CONFIG`. Here are a few important directories in ruby installation.
{% highlight ruby %}
Config::CONFIG["bindir"] # executables like irb, ruby
Config::CONFIG["libdir"] # standard library files
Config::CONFIG["archdir"] # C extensions
Config::CONFIG["sitedir"] # third party extensions and libraries
Config::CONFIG["vendordir"] # third party extensions and libraries
# There is also a 'gems' directory at the same level as sitedir which stores ruby gems.
{% endhighlight %}

Ruby also comes with a set of command line tools. **RDoc** (Ruby Documentation) turns comments put in code in specified format into documentation. **ri** (Ruby Index) gives you a way to access information extracted by RDoc. **rake** is a task management utility (like make) which allows you to write tasks using ruby syntax.

That's it for now. Excited about learning new things next week.
