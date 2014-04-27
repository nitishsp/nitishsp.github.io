---
layout: post
title:  "Setting up Dev machine for Rails"
---

After grappling with UEFI, GPT, Driver issues and what not, finally I have reasonably stable dual boot system. I used to follow [this](http://geniitech.tumblr.com/post/25984445368/r) guide for setting up development environment, but it's a bit outdated. So I decided to log the process. Here is how I set up my machine for Rails development.


Ubuntu
-------------
Before installing the tools, I ensure that all the installed packages and the package index itself is updated.
{% highlight bash %}
# Fetch latest packages info from sources
sudo apt-get update

# Update all installed packages
sudo apt-get dist-upgrade

# If you want to play safe, use replace 'dist-upgrade' with 'upgrade'
{% endhighlight %}
man page of apt-get has detailed explanation for `update`, `dist-upgrade` and `upgrade`.

Sublime Text
--------------------------
[Sublime Text](http://www.sublimetext.com/) has been my favorite text editor ever since I got outside the Java world and started exploring Python and Ruby. It's lightweight, has great plugins and gives a lot of customization options. Here are my overrides for its default settings,

{% highlight javascript %}
// Settings:
{
  // The number of spaces a tab is considered equal to
  "tab_size": 2,

  // Set to true to insert spaces when tab is pressed
  "translate_tabs_to_spaces": true,

  // Set to true to removing trailing white space on save
  "trim_trailing_white_space_on_save": true,
}

// Keybindings:
[
  { "keys": ["ctrl+shift+o"], "command": "prompt_open_folder" }
]
{% endhighlight %}

The easiest way of installing sublime packages is using [Sublime Package Control](https://sublime.wbond.net/). Just go to its site and follow the installation instructions. Once you have installed Sublime Package Control, all you have to do is press `Ctrl + Shift + P`, go to `Package Control: Install Packages` and select the package you want to install. One package I find very useful is [GitGutter](https://github.com/jisaacks/GitGutter). It shows an icon in the gutter indicating if line has been inserted, modified or deleted.


Terminal
--------------------------
The default terminal included in Ubuntu is fine for initial setup but for regular use I prefer dropdown terminals. They stay out of your way and you can conjure them when required. I started with yakuake but it has a lot of KDE dependencies, so I switched to tilda, which is really lightweight.
{% highlight bash %}
sudo apt-get install tilda
{% endhighlight %}


Git
--------------------------
[Git](http://git-scm.com/) is probably the most popular version control system in the Open Source community. Most of my recent code is on GitHub. In fact, this blog itself is hosted on GitHub.

{% highlight bash %}
sudo apt-get install git
{% endhighlight %}

Here is my `~/.gitconfig` file:

    [user]
      name = Nitish Parkar
      email = <my_github_email>
    [color]
      ui = auto
    [alias]
      co = checkout
      s = status
      b = branch
      hist = log --pretty=format:'%h %ad | %s%d [%an]' --branches --graph --date=short --max-count=10

Git aliases are shorthands for long git commands. Before I discovered them I almost always used to misspell status. Now it's just `git s`!

Finally, I generate ssh key and add it to GitHub as explained in [this](https://help.github.com/articles/generating-ssh-keys) article.


Ruby
--------------------------
I use [RVM](https://rvm.io/) to install Ruby. Its installation is pretty straightforward. Once you have RVM, you can install multiple ruby environments and switch among them as and when required.

{% highlight bash %}
# List all available rubies
rvm list known

# Install a ruby
rvm install 2.1.1

# Show currently installed rubies
rvm list

# Switch ruby
rvm use 2.1.1

# Set default ruby
rvm use --default 2.1.1
{% endhighlight %}

For RVM to work properly, you have to pass `--login` flag to the shell. The way of doing this differs from terminal to terminal. [This](http://stackoverflow.com/a/9337014) answer provides little explanation and links to appropriate resources. For tilda, set *Preferences > Custom Command* to `/bin/bash --login`.

I don't use rdoc, so by default I don't want to download rdoc and ri info for any gems. This can be achieved by adding the following line to `~/.gemrc`.

    gem: --no-rdoc --no-ri

I used to use RVM gemsets. But with bundler, Gemsets are not required. So I have stopped using them.


MySQL
--------------------------
{% highlight bash %}
sudo apt-get install mysql-server mysql-client libmysqlclient-dev
gem install mysql2
{% endhighlight %}


Apache and Passenger
--------------------------
Though Webrick or Thin are great for development, it's nice to have [Apache](http://www.apache.org/) and [Passenger](https://www.phusionpassenger.com/) around.

{% highlight bash %}
sudo apt-get install apache2

# for asset pipeline
sudo a2enmod headers
sudo a2enmod expires

gem install passenger

passenger-install-apache2-module

# Dependencies:
# sudo apt-get install apache2-threaded-dev libapr1-dev libaprutil1-dev libcurl4-gnutls-dev
{% endhighlight %}

At the end, passenger will tell you to copy paste a few lines to apache configuration file.

    LoadModule passenger_module /home/nitish/.rvm/gems/ruby-2.1.1/gems/passenger-4.0.41/buildout/apache2/mod_passenger.so
    <IfModule mod_passenger.c>
     PassengerRoot /home/nitish/.rvm/gems/ruby-2.1.1/gems/passenger-4.0.41
     PassengerDefaultRuby /home/nitish/.rvm/gems/ruby-2.1.1/wrappers/ruby
    </IfModule>


Javascript Runtime environment
--------------------------
Rails asset pipeline requires Javascript Runtime environment to compile CoffeeScript, uglify JS, etc. You can use therubyracer gem but I prefer [NodeJS](http://nodejs.org/), since it's a dependency for a lot of dev tools.
{% highlight bash %}
sudo add-apt-repository ppa:chris-lea/node.js
sudo apt-get update
sudo apt-get install python-software-properties python g++ make nodejs
# source
# https://github.com/joyent/node/wiki/Installing-Node.js-via-package-manager#ubuntu-mint-elementary-os
{% endhighlight %}


Miscellaneous
--------------------------
{% highlight bash %}
# required by paperclip
sudo apt-get install imagemagick

# nokogiri dependencies
sudo apt-get install libxslt-dev libxml2-dev
{% endhighlight %}


That's it. Happy Coding! :)