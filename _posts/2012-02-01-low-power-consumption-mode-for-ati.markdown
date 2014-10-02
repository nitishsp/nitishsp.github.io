---
layout: post
title: "Low Power Consumption Mode for ATI cards in Fedora"
external_url: http://nitishsp.blogspot.in/2012/02/low-power-consumption-mode-for-ati.html
---

I have ATI Radeon HD 4570 graphics card. Ever since I started using Fedora, I couldn't properly install drivers for my graphics card. It's hell lot of difficult to get ATI drivers working on Fedora. Last week, when I installed proprietary ATI drivers on F16, the OS just stopped working. It would stop loading just before the login-prompt. This time I decided not to pursue the problem & did a rollback.

Somewhere on the internet I found this:

    echo low & /sys/class/drm/card0/device/power_profile

It sets the graphic card to low power consumption mode. Upon using my laptop in this mode for a few days I noticed that this has solved the overheating problem to some extent. So I would definitely recommend it over installing crappy ATI drivers. Still its far from what I get on Windows Vista so I am considering switching to Ubuntu when its next LTS version is released.