---
layout: post
title: How to replace VS Code external terminal with new windows terminal?
# thumbnail: "https://miro.medium.com/max/1400/0*M-nbKpaJOiBFhGn8.jpg"
tags: [customization, windows]
---

Your workspace needs to be as cool as you :)

![Fig: The “new” windows terminal](https://cdn-images-1.medium.com/max/2560/0*M-nbKpaJOiBFhGn8.jpg)_Fig: The “new” windows terminal_

Personalizing workspace is always beneficial for productivity, at least for me. I hear a lot of people talking about how its better to just “work” without beautifying things but, I just can not work that way and I know most of you here can’t as well. In this article, I will guide you on how you can easily use the new and cool windows terminal as the external terminal in visual studio code. Not only that, we’d be discussing about cool themes, transparent terminal, cool fonts and a lot more.

This is the end result. (p.s. Don’t hate me but I actually like light mode terminal better than the dark mode terminal 😜)

![Fig: Execution of Java Program on the new terminal](https://cdn-images-1.medium.com/max/3300/1*8XySdGqQuBFZHR2L7JPJYg.png)_Fig: Execution of Java Program on the new terminal_

“Woah, That’s so cool, YOU ARE SO COOL, How did you do it?”, you might wonder. I wondered for a long time and finally u/GoodClover helped me figure it out.

Let’s get straight to the point. Follow the steps below.

1. Press F1 for the command box, and search for ‘Open Settings’ and click on the option which says: “Preferences: Open Settings (JSON)”. In the picture below, the option is at the top which might not be the case in your editor.

![](https://cdn-images-1.medium.com/max/2000/1*7t6A-c0bZv4OF0osl2aZRg.png)

2. On the settings.json file that opens up, scroll down until you see (or search)
   > “terminal.external.windowsExec”: “C:\\WINDOWS\\SYSTEM32\\cmd.exe”,

The value might be different in your system, but the key must be same.

3. Change the value to “wt -p cmd cmd” and now the total command will look like this

   > “terminal.external.windowsExec”: “wt -p cmd cmd”,

4. Yay, You are good to go. You have what you wanted to achieve.

**A common problem:**

If you set the key to:

    C:\\Users\\<username>\\AppData\\Local\\Microsoft\\WindowsApps\\wt.exe

you are likely to face an error like this:

![](https://cdn-images-1.medium.com/max/2000/1*X7E3OrPYtlc8_cdU-ZokOQ.png)

**So, How did it work?**

According to u/GoodClover,

This is because VScode assumes you are running cmd and has (afaik) no config for the command line arguments, and when they get passed to wt it has no clue what they mean, adding cmd (the last one) then makes wt run cmd and the argument get passed to it correctly.

If you want to use your profile for cmd you have to add -p cmd, so the full command becomes wt -p cmd cmd

## **BUT**

The terminal is not still as useful as the traditional command prompt. For example:

If you wanted to open a project folder in VSCode, its easy with the command prompt. As simple as this:

![](https://cdn-images-1.medium.com/max/2000/1*LAUuEJlHw4TtzTXWz8BWYA.png)

You typed cmd on _whatever-bar_ that’s called and a terminal window would pop at the same directory!

![](https://cdn-images-1.medium.com/max/2000/1*-lcSxQJ00kO3B_vrUAZhmQ.png)

This is what I wanted.

But, if type “wt” instead on “cmd” on the *whatever-bar, *Windows Terminal will pop up but look at the directory.

![](https://cdn-images-1.medium.com/max/2040/1*WSpeZdGnJWOuXIlf2XmIEw.png)

Its my home directory! I DID NOT WANT THAT!

So, what can we do? Solution is simple actually!

These are the steps:

1. Click on the down arrow and go to settings, It will open up a settings.json file but, this is the json settings for our terminal.

![](https://cdn-images-1.medium.com/max/2034/1*ODKvo16lkqhDX7qSMUbGHg.png)

We just need to add just one line to make this work.

2. Inside the defaults object which is inside the profiles object, just add this line:
   > “startingDirectory”: “%**CD**%”,

p.s. Don’t mind the fontFace, fontSize and other keys.

![](https://cdn-images-1.medium.com/max/2176/1*9TZdDH0yByPg-opE6DhafA.png)

3. You did it!!! That is it!

## ANOTHER BUT

Do you wish to have the windows terminal on the context menu as well? (p.s Yayyyy, I actually remembered what this menu was called.)

![](https://cdn-images-1.medium.com/max/2000/1*q3zaJOwKQPISUb0iBdx1iA.png)

Looks pretty dope, doesn’t it?

I don’t want to make this article too long so have a look at Vlad412’s answer [here](https://github.com/microsoft/terminal/issues/1060#issuecomment-640060704). Its simple, download an image, put it in the required directory and run a registry command. Yay, it’s done. But, if you had problems understanding that, leave comments so I may edit this post (if Medium let’s me, this is actually my first post :) ) or maybe reply to your comments.

## One last thing,

For people who want their terminal to look exactly like mine does, here’s how:

1. On the settings.json file of the windows terminal, search for schemes array and paste this object inside.

   {

   “name” : “Frost”,

   “background” : “#FFFFFF”,

   “black” : “#3C5712”,

   “blue” : “#17b2ff”,

   “brightBlack” : “#749B36”,

   “brightBlue” : “#27B2F6”,

   “brightCyan” : “#13A8C0”,

   “brightGreen” : “#89AF50”,

   “brightPurple” : “#F2A20A”,

   “brightRed” : “#F49B36”,

   “brightWhite” : “#741274”,

   “brightYellow” : “#991070”,

   “cyan” : “#3C96A6”,

   “foreground” : “#000000”,

   “green” : “#6AAE08”,

   “purple” : “#991070”,

   “red” : “#8D0C0C”,

   “white” : “#6E386E”,

   “yellow” : “#991070”

   }

It looks like this now:

![](https://cdn-images-1.medium.com/max/2000/1*jOrQj4KSGFyhVSpKRTi_TA.png)

2. Scroll up to the list array and inside cmd object, remove everything except guid and paste this:

   "name": "Command Prompt",

   "commandline": "cmd.exe",

   "hidden": false,

   "colorScheme": "Frost",

   "acrylicOpacity": 0.7,

   "cursorColor" : "#000000",

   "fontSize": 14,

   "fontFace":"Cascadia Code",

   "fontWeight": "light"

It looks like this now:

![](https://cdn-images-1.medium.com/max/2000/1*KwGQfWSEP7GvZX_mykXqIQ.png)

DONE! But, this just affects the cmd and if you wish to make your powershell and ubuntu terminals look the same, paste the above code not inside cmd array but inside the defaults object where we just set the starting directory.

Also, My VSCode theme is “Community Material Theme Ocean”.

And, if you want to check out the theme that I developed, that looks like this:

![](https://cdn-images-1.medium.com/max/2490/0*EFtlyLBvVwbwjKXs.jpg)

Here’s the [link](https://marketplace.visualstudio.com/items?itemName=rsnpj.cool-ass-theme).

Have a look at my [GitHub ](https://github.com/rsnpj/)and [Portfolio](https://www.roshanparajuli.com.np/)! :)

Want to customize more? Have a look at this.
[**Windows Terminal: The Complete Guide - SitePoint**
*In this article, we'll explore Windows Terminal, the ideal accompaniment to WSL2. It's fast, configurable, looks great…*www.sitepoint.com](https://www.sitepoint.com/windows-terminal/)

Thank you for reading. Have a great day, or maybe a night, how will I know when you’re reading this? 😜
