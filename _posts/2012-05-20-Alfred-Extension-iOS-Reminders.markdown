---
layout: post
title: Alfred Extension to create iOS Reminders
---


I have been using [Alfred](http://www.alfredapp.com/) - a productivity application for Mac 
OS X - for a [couple of months](http://twitter.com/#!/dlinsin/status/187817517073448960) 
now and I must admit: I'm a huge fan! The Mac by itself is already a huge productivity gain, but 
building your workflow around Alfred, boosts your productivity off the charts.

Don't worry this won't be an Alfred-praise post, but rather a quick introduction into a neat 
little extension I wrote, which allows you to create iOS Reminders directly from Alfred. It's free and 
open source. You can grab the [source on Github](http://github.com/dlinsin/alfred-reminders) 
or [directly download the extension](https://github.com/downloads/dlinsin/alfred-reminders/Reminders.alfredextension) 
and install it into Alfred. _Note: you'll need [Alfred's Powerpack](http://www.alfredapp.com/powerpack/) 
- a payed upgrade, enabling a lot of cool features._

Creating "iOS Reminders" is admittedly a little misleading. Essentially, reminders on the Mac are 
Todos in iCal, which are synced via iCould - nothing more and nothing less. It's fairly easy 
to create them via [AppleScript](http://en.wikipedia.org/wiki/AppleScript). There's already 
an [existing Alfred extension](http://mohey.be/post/20543412659/alfred-extension-for-ical-reminders) 
by Drew Mohebbi, solving exactly the same problem, but is limited in certain ways. I 
actually borrowed some code from yet another [rudimentary Reminders extension](http://www.dirtdon.com/?p=1261).

First I decided to use a fairly simple, but still flexible syntax to create reminders. Here 
are a couple of samples:

* `rem get milk -Mon -3am -work`
* `rem get milk -tom`
* `rem get milk -6:15am`

You can find all valid combination on the [project page](https://github.com/dlinsin/alfred-reminders#usage). 

![Sample Reminder with Alfred](https://github.com/downloads/dlinsin/alfred-reminders/reminder_screen_shot.png)

I guess you can see the value in using Alfred to create Reminders from the examples above. 
It is so much easier, faster and more convenient to create your Reminders!

There are a couple of defaults at play here, which I hope are sensible: 

* if you don't provide any day or time e.g. `rem get milk`  
-> it'll create a reminder _today 60 minutes from now_
* if you don't provide a day but no time e.g. `rem get milk -Monday`  
-> it'll create a reminder _next Monday at 8am_ 

Maybe I'll make those configurable at some point, however I think they are quite sensible.

Using [AppleScript](http://en.wikipedia.org/wiki/Applescript) was awesome! It's easy and 
there is lots of code and tutorials online. I have to admit: I've never been a big fan 
up until now, but I'll look into it more often from now on - especially for automating little 
things on my Mac.

There are definitely parts that need improvement: e.g. passing a date instead of only the 
next 7 days would be something quite handy (Drew's extension handles that). There are also 
some edge cases with passing the name of the calendar, which don't work. If you find 
anything else, [let me know](https://github.com/dlinsin/alfred-reminders/issues), I'll try 
to fix it. 
