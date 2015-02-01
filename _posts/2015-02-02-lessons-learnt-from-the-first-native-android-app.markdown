---
title:  "Lessons learnt from the first native android app"
---

I first began learning Android through a  course offered on Udacity - "Developing Android Apps". The course helped me get started with Android development and it introduced me to some of the fundamental concepts involved. Before that, I had mostly done web development (largely  in Ruby on Rails). Towards the end of the course I started working on a production app for a client. It was a chat app, combined with jobs-board like functionality (details obscured because of NDAs). Here are a few lessons I’ve learnt while developing my first native android application.

It should feel like an app
-------------
In an app, users expect everything to happen almost instantaneously. Every time I saw someone using my app, they were always tapping here and there, often before realizing what was on the screen! Ideally you should have everything you need saved locally on the device and interact with a server only when necessary. Make heavy use of background syncing.

Sometimes connected
-------------
Not everyone using a smartphone has a 3G or even a 2G connection. Some even prefer to connect to the internet only when required. You need to keep this in mind while developing an app that needs to transfer data to a cloud server.  Before connecting, always check if the device is connected to the internet. If not, inform the user. If you can sync data asynchronously, make use of functionalities provided by the framework to sync data when device is connected to the internet.

Limited Resources
-------------
While developing for mobile devices it is important to keep in mind  that these devices run on battery power. You have to make sure that your app uses as little power as possible and takes advantage of services provided by the framework. It’s not a good practice to constantly ping the server for updates, make use of services like GCM. Combine updates into batches and let the OS figure out the optimal timing to execute them.

Design Patterns
-------------
Design patterns are everywhere in Android. Initially, they feel like an overhead but once you understand why they exist you will thank the core developers for putting them in place. Most of them focus on making efficient use of limited resources. They ensure that you follow certain best practices while developing Android apps. Without them, most developers would have likely created apps that drained resources pretty quickly, hampering the overall experience for end users.

Understanding The SDK
-------------
Android uses Java as its programming language. It’s a compiled language and doesn’t have Rails like console. So you can’t just fire up a debugger to try out your code. You need to be aware of language features as well as what works and what doesn’t work. You need to have working program in your head before you type it out. This means you have to spend some time learning the language and understanding the nitty-gritties of it. Debugger driven development just doesn’t work!

Scarcity of Quality resources
-------------
There are very few well documented libraries available for Android. Using some obscure, poorly documented feature of a library takes lot of effort. Most of the libraries haven’t matured yet and lack flexibility. Companies like Square are doing great work by contributing quality open source libraries. Given the popularity of the platform, more and more companies will release open source libraries, so I think this will  improve over the time.

Most of the blog articles and tutorials I found explained how to do something in Android. But very few bothered to explain why something works. Good for copy pasting, bad if you want to understand how stuff works.

Time factor
-------------
Lack of a console hurts you the most while debugging. You can’t just pause execution and try out arbitrary code. The most you can do is pause and inspect variables. Then you go backwards line by line till you find the actual cause of the error. Adding debug points and recompiling along the way as necessary. When compared to rails development, this is extremely slow and often frustrating.

While working on the UI, unlike browsers, you can’t just do inspect element and move things around till you are satisfied with the outcome. The Preview offered by IDE works only for the most basic elements. Often what you see on the screen is combination of multiple views. In such cases, the only way to preview changes is to compile and see them on a device/emulator. This slows you down and often you can only guess why the elements are not being displaying as expected.

Using IDEs
-------------
If you are a web developer, chances are that you have mostly used text editor for development. Switching to IDE takes some time to get used to it. IDEs take forever to load and slow down your system. But soon you get used to it and start taking advantage of their features. You really need features like code generation while working with verbose languages like Java. They also help eliminate errors caused due to misspelling names. Refactoring becomes much faster and error free.

No Substitute for core skills
-------------
Even with all the differences, the core skills required to successfully finish a project are not that different from web apps. You need to get good understanding of the requirements and craft the best possible solution in reasonable time frame, while keeping all the stakeholders informed. Always keep learning and do things the right way.

Android platform is still in its early stages. Android Studio - the official IDE for Android app development - came out of beta only last month. With Android 5.0, google has laid down the foundation for future improvement. As the ecosystem matures, the development process will improve. More tools will be introduced that will make life easier for developers. It will be interesting to see how the process evolves over time.


*Thanks to [Varun Vohra](https://twitter.com/binary2boot) for helping me improve this post.*