---
layout: post
title: Reset App Icon Badge with UILocalNotification
---


For our new super secret project at [furryfishApps](http://furryfishapps.com "furryfishApps"), we are heavily using *[UILocalNotification](http://developer.apple.com/library/ios/#documentation/iphone/Reference/UILocalNotification_Class/Reference/Reference.html "Apple's docs on UILocalNotification")* and the badge on our App's icon. 

Just to quickly revisit: when a *UILocalNotification* is fired, it'll set the badge to the number, that you previously defined like this:

{% highlight objectivec %}
UILocalNotification *notification = [[UILocalNotification alloc] init];
notification.applicationIconBadgeNumber = 3;
// TODO schedule notification
{% endhighlight %}
<a class="gist" href="https://gist.github.com/949534">gist</a>

While trying to remove the badge, I found that there is no documentation on this whatsoever. You might think it should be easy, just set the property *applicationIconBadgeNumber* to 0, however here's what *UILocalNotification*'s documentation says:

> The default value is 0, which means "no change.” The application should use this property’s value to increment the current icon badge number, if any.

Well, that means the badge is not removed when setting the property *applicationIconBadgeNumber* to 0, **instead you need to set it -1**. As soon as the *UILocalNotification* is fired, the badge is removed from the App's icon.

Would be nice to have that in the documentation, so I filed radar://9357622.