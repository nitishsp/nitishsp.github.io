---
layout: post
title: "Beating Google Olympic Doodles"
---

Google has been creating interactive doodles for a while now. I am a big fan of these doodles. So when Google launched their [first interactive Olympic doodle](https://www.google.com/doodles/hurdles-2012) last night, I was hooked to it. Soon my friends started posting their high scores and my best score was far from theirs. I played for a while but soon lost interest. So I decided to try programming.

Few months ago I had come across [Robot](http://docs.oracle.com/javase/7/docs/api/java/awt/Robot.html) class in Java. I used it to simulate keystrokes from java program. Here is what Java Documentation says about Robot:

> This class is used to generate native system input events  for the purposes of test automation, self-running demos, and  other applications where control of the mouse and keyboard  is needed. The primary purpose of Robot is to facilitate  automated testing of Java platform implementations.

I created a java program that simulates left-right keystrokes for [the hurdles doodle](https://www.google.com/doodles/hurdles-2012). I didn't hardcode the jumping part because that would have required a lot of trial and error and would have taken the fun out of it. So you still have to jump the hurdles yourself. With the help of my program I clocked 9.6, better than any of my friends.

Next day Google launched [the basketball doodle](https://www.google.com/doodles/basketball-2012). I played it for a while and realized that unlike the hurdles doodle, this doodle could be completely automated without extensive trial and error. So I modified the previous code and scored 42 pts in it. It was amusing to see it in action.

Both the programs are simple and easy to understand. The source codes can be found on pastebin.
+ [Hurdles Doodle in Java](http://pastebin.com/xwzC6kbb)
+ [Basketball Doodle in Java](http://pastebin.com/8XahSUXK)

UPDATE
-----------

There are some hacks in JavaScript that make the runner go faster. It is perhaps much easier to do the above programs in JavaScript. But my intention wasn't to hack the doodles, I just wanted to see if it could be done using Java .

Google's view on this cheating stuff is interesting ([Mashable](http://mashable.com/2012/08/07/google-doodles-olympics/)):

>“Our hope is that people will want to play a fair game, but we also  understand that for some people cheating is in fact an engineering  challenge — its own kind of programming Olympics.”