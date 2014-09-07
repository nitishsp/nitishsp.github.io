---
layout: post
title: "Google App Engine Launcher in Fedora"
external_url: http://nitishsp.blogspot.in/2012/12/google-app-engine-launcher-and-fedora.html
---

Google App Engine launcher is a handy tool for GAE development. Although GAE sdk and command line are sufficient, one click execution\deployment is often more convenient. When I was installing GAE launcher I couldn't find a single guide for Fedora, hence this post. I am using Fedora 16 + LXDE.  This post assumes that you already have [GAE sdk](https://developers.google.com/appengine/downloads)

Get the prerequisites
-----
    sudo yum install wxGlade wxPython

Download source code
-----

The app engine launcher source is available on code.google.com.  If you have subversion installed, go to [this](https://developers.google.com/appengine/downloads) link and follow the instructions. If you don't have subversion, you can use wget as follows:
    wget -m -np http://google-appengine-wx-launcher.googlecode.com/svn/trunk/ google-appengine-wx-launcher-read-only
This command will fetch the code and put it in `./google-appengine-wx-launcher.googlecode.com/svn/trunk`. You can move the code to another directory. I copied the content of trunk directory to `/opt/appengine_launcher`

Create a desktop entry
-----
Save the following text to `/usr/share/applications/gae.desktop` (make sure you use correct path in Exec parameter)

    [Desktop Entry]
    Encoding=UTF-8
    Name=App Engine Launcher
    Categories=Development;
    Type=Application
    Exec=python /opt/appengine_launcher/GoogleAppEngineLauncher.py
    Icon=AppEngine

Icon for desktop entry
-----
Copy `AppEngine.png` inside images directory to `/usr/share/icons/` and Done!

GAE launcher should appear in the programming section. You'll probably need to configure path to gae sdk the first time you run it. Set it in GAE Launcher preferences.

Thats it! Happy Coding!