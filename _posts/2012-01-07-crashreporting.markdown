---
layout: post
title: Crash Reporting - Don't let your user do quality assurance
---


I'm not a big fan of crash reporting in App Store Apps. In a lot of discussions with 
developers I had the feeling they see it as some kind of quality assurance. As if it would 
replace thorough testing, because you can fix everything with an update. I think it's not 
a user's job to find bugs and report them to you. It's your job as a developer to go the extra mile 
and test your App to ensure a sufficient level of quality. 

That said, I do realize it's almost impossible to find every bug and to test every possible 
scenario. That's why I decided to add crash reporting to furryfishApps' latest App ["Bahn Köln"](http://ffapps.me/bahn), 
when being asked by [Crashlytics](http://crashlytics.com/) to join their private beta program.

When reading about Crashlytics I expected it to be one of those frameworks, which is almost 
impossible to integrate with an existing App. To my surprise it was quite the contrary. Everything 
was setup within a couple minutes, it couldn't have been more hassle-free. It's worth checking out 
if you consider adding crash reporting to your App.

It's been two weeks since the first version with crash reporting shipped. Almost 1600 users (about 60%) 
installed the update and with the Christmas holidays and new years eve, we've got some pretty 
good usage numbers to draw a conclusion. 

Overall we had about 4 crash related issues, with merely 15 users affected. That's 1% of 
the users who installed the update. Keep in mind: we decided to not send reports automatically. 
The user must agree to send them, hence there's a good chance we missed a couple of reports. 
However, due to the [thought](http://dlinsin.github.com/2011/07/31/Appdate.html) we put into 
each and every decision of our App, we can be quite happy with the numbers. 

From a developer's perspective the numbers are secondary. What's important is the source of 
the crashes. As it turned out, only 1 crash was actually a programming error. I forgot to 
check the length of an array - a stupid mistake, which surfaced in an edge-case. 
All other crashes were weird side-effects from our very unstable datasource - 
the [KVB-Widget generator](http://www.kvb-koeln.de/generator/index.html). We try our best 
to protect the user from those side-effects, unfortunately it doesn't always work. 

My reservations when it comes to crash reporting remain: It doesn't replace thorough testing - 
on various devices and in different scenarios. Don't let your user do quality assurance.
