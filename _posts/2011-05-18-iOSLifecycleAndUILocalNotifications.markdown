---
layout: post
title: iOS App Lifecycle and UILocalNotifications
---


In my [previous post](http://dlinsin.github.com/2011/04/30/UILocalNotification.html) on *UILocalNotifications*, I wrote about how to reset the badge number on your app icon. This time I'd like to point out how *UILocalNotifications* tie into the iOS lifecycle and a pitfall I ran into, developing furryfishApps lates app. When it comes to the iOS lifecycle in gerneral, I'd like to refere you to Oliver Drobnik's [great blog post](http://www.cocoanetics.com/2010/07/understanding-ios-4-backgrounding-and-delegate-messaging/) a while back. 

All the important methods that tie *UILocalNotifications* into your iOS app lifecycle reside in in *UIApplicationDelegate*:

{% highlight objectivec %}
// Tells the delegate when the application has launched and may have additional 
// launch options to handle.
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:
                                                 (NSDictionary *)launchOptions

// Sent to the delegate when a running application receives a local notification.
- (void)application:(UIApplication *)application didReceiveLocalNotification:
                                          (UILocalNotification *)notification
{% endhighlight %}

So it looks simple, right? In case you want to do something special, when your app is launching from a button tap on an *UILocalNotification* just implement the first method. If you want to handle receiving notifications, while your app is running, e.g. to update a view or display the content, you implement the second method.

As you can imagine, it turns out not to be that simple after all. I ran into a tricky problem: whenever our App received a *UILocalNotification* "running" in background and the user taps the button to open the App, *application:didReceiveLocalNotification:* on the app delegate was called. If you have implemented *application:didReceiveLocalNotification:* to play a sound and display a notification to the user when the App is actually running in the foreground, the same happens if the user taps on the button of the native notification. You probably don't want your user to get the same notification and sound twice, especially because he wants to check your App for further information.

As it turns out, this is intended as Apple's documentation of the method states:

> This method is invoked after application:didFinishLaunchingWithOptions: (if that method is implemented).

So in order to prevent the sound and notification to be played and displayed after launching from a *UILocalNotification*, you could simply add some kind of *BOOL* to your app delegate in *application:didFinishLaunchingWithOptions:* and check it afterwards in *application:didReceiveLocalNotification:*. However, *application:didFinishLaunchingWithOptions:* is only called when you "start" the app, not when your app is becomes active and all the other methods don't let you check if you've launched from a *UILocalNotification*.

StackOverflow to the rescue! I found a [question](http://stackoverflow.com/questions/4136333/test-if-app-did-become-active-from-a-uilocalnotification/5708486#5708486) with a neat solution, which works perfectly for me:

{% highlight objectivec %}
- (void)application:(UIApplication *)application didReceiveLocalNotification:
                                        (UILocalNotification *)notification {
    if(application.applicationState == UIApplicationStateActive ) { 
        DBLog(@"Received: %@", notification.alertBody);
        // alert, because app is running in foreground
    }
}
{% endhighlight %}
<a class="gist" href="https://gist.github.com/978155">gist</a>

It turns out, that *UIApplication.applicationState* is only active when the app is running in foreground. This is a neat way to check if your app has just launched from a *UILocalNotification* or is already active. 

 
