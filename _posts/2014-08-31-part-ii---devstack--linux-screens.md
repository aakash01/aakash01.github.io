---
layout: post
title: "Part II - DevStack : Linux Screens"
description: ""
category: OpenStack
tags: [OpenStack, DevStack]
author: aakash01
---
{% include JB/setup %}

There is a great post written on linux screens in devstack over [here](http://www.rushiagr.com/blog/2013/06/05/linux-screens-in-devstack/). I'm going to use most of the stuff from that post. 

In a DevStack environment, all the processes run under something special in Linux, called as a `screen`. Each screen runs a ‘service’ of OpenStack.  We can get the screens by : 

**` screen -x `**

-------------------------------

####Working with Screens
Names of all screens are shown at the bottom of the terminal . The screen on which you currently are bears an asterisk (*) near its name. 

####Commands : 

`Ctrl+A` `D`	To detach from a screen

`Ctrl+A` `K`	To kill a service. 

`Ctrl+A` `N`	Move to right("next") screen

`Ctrl+A` `P`	Move to left("previous") screen

`Ctrl+A` `'<Apostrophe)` `<screen_number>`	Move to particular number of screen. Eg: `Ctrl+A` `'` `4`

`Ctrl+A` `[` 	Copy Mode, You can use this to scroll up/down to check logs.  use `]` to come out of it. 

####other commands 

`screen` 		Create new Screen

`screen -rd`	Reattach to an existing screen

`screen -list`	List all the screens

