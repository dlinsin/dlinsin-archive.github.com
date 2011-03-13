---
layout: post
title: Don't use MainWindow.xib with Autorotation
---

Working on [furryfishApps'](http://furryfishapps.com "furryfishApps") new super secret project, I came across a strange problem, which not even [stackoverflow](http://stackoverflow.com "stackoverflow") had a solution for. At least I couldn't find it.

When using the standard Apple template to create an iOS framework, Xcode creates, along with other stuff, a *MainWindow.xib*, which contains your *UIWindow* and is used to create your AppDelegate. Since its' already hooked up to your *Info.plist* and works out of the box, I never bothered to question this construct - until today. 

I noticed that our new App, when rotated has some weird effects at the bottom of the screen. It didn't appear smooth, almost a little lagging. Since a picture tells more than my attempt to explain:

![Weird effects when autorotating](/images/2011-03-20-autorotation-1.png "Weird effects when autorotating")

Since I'm using a pimped version of [BCTabBarController](http://github.com/dlinsin/BCTabBarController "BCTabBarController fork on github"), my first thought was that it must be the root of all evil. Fortunately, I was wrong! The sample coming with BCTabBarController doesn't show those effects. I decided to set up a brand new projects with Apple view-based template. After integrating and setting up BCTabBarController, the same effects as in our App appeared. The projects were almost identical, so how could this be? 

The only difference between the two projects was the setup of AppDelegate and its *UIWindow*. Apple's template added a *NSMainNibFile* key and MainWindow.xib value to the *Info.plist*. Furthermore there's an *IBOutlet* in the AppDelegate, which is hooked up to the *UIWindow* instance, configured in *MainWindow.xib*. 

The BCTabBarController sample project on the other hand was configured "manually". The *UIWindow* instance was created in the AppDelegate like this:

{% highlight objectivec %}
self.window = [[[UIWindow alloc] initWithFrame:
              [[UIScreen mainScreen] bounds]] autorelease];
{% endhighlight %}
<a class="gist" href="https://gist.github.com/868321">gist</a>

There was no MainWindow.xib, so no need for a corresponding key/value pair in the *Info.plist*. The AppDelegate is configured in the file *main.m* like this:

{% highlight objectivec %}
int retVal = UIApplicationMain(argc, argv, nil, @"EXAppDelegate");
{% endhighlight %}<a class="gist" href="https://gist.github.com/3512b737fd34a3e75a6a">gist</a>

After applying those changes to our new project, I was able to remove the weird effects and there's a smooth autorotation experience now:

![Smooth autorotation](/images/2011-03-20-autorotation-2.png "Smooth autorotation")

Honestly, I have no idea what the cause of this might be. Looking at the configuration of *UIWindow* instantiated by *MainWindow.xib*, there's no difference to the one set up manually. I'm grateful for any clues, however, at the moment I'm just happy that I solved this issue.