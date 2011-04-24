---
layout: post
title: DLWebView - a drop-in browser component
---


A couple of weeks ago, I had to implement a browser component in 4 different Apps at <a href="http://grandcentrix.com">work</a>. I went through the hassel of implementing it separately each time, although they basically had the same requirements. Last weekend I went the extra mile to bake a component, which you can use in your code, in case you need to display a website. 

Hello World - <a href="http://github.com/dlinsin/DLWebView">DLWebView</a>!

**DLWebView** is a *UIViewController* subclass, which you can use in conjunction with a *UINavigationController*. It features a refresh button, back/forward buttons as well as a title label. Those buttons are added to the *UINavigationBar*, when DLWebView is loaded. 

If you add a *UIBarButtonItem* to **DLWebView**, when setting up the *UINavigationController* and hook it up to 
{% highlight objectivec %}- (IBAction)showUrlField:(id)sender;{% endhighlight %}
and you'll get a flashy *UITextField* to handle editing URLs. However, if you only have one website to display, it's not mandatory to enable this feature.


<object width="480" height="385"><param name="movie" value="http://www.youtube.com/v/RrdGWb8qJ4Q?fs=1&amp;hl=en_US"></param><param name="allowFullScreen" value="true"></param><param name="allowscriptaccess" value="always"></param><embed src="http://www.youtube.com/v/RrdGWb8qJ4Q?fs=1&amp;hl=en_US" type="application/x-shockwave-flash" allowscriptaccess="always" allowfullscreen="true" width="480" height="385"></embed></object>


**DLWebView** works in portrait and in landscape mode (check out the video above). Once a page is loading, you can see the URL displayed in the title, which changes to the title of the website once loaded completly. It's iOS 3.x compatible, so no worries about breaking exisiting Apps.

There's still some stuff to work on:

* there's a basic URL validation implemented, however it's far from being perfect and I'm thinking of removing it entirely.
* the dependency on *UINavigationController* is certainly not be the best solution, so I'm looking into removing that
* the solution of using a *UIBarButtonItme* for bringing up the text field to edit URLs is not ideal

I'd love for folks out there to  <a href="http://github.com/dlinsin/DLWebView">help</a> me make this a first-class component to use, when you need to display websites in your App.  