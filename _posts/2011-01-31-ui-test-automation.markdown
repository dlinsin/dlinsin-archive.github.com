---
layout: post
title: UI Test Automation with Instruments
---

One of the most impressive talks for me at <a href="http://dlinsin.blogspot.com/2010/06/wwdc10.html">WWDC 2010</a> was session 306 - "Automating Use Interface Testing with Instruments". I've been wanting to check it out ever since iOS 4 was released. A couple of weeks ago, I finally had a chance to give it a test ride with <a href="http://mobile.synyx.de/2010/09/i-think-i-spider-1-0-released/">"I think I spider"</a>, one of the Apps I developed.

All you need to get started is an App, Instruments and some basic JavaScript skills. Apple provides a set of <a href="http://developer.apple.com/library/ios/#documentation/ToolsLanguages/Reference/UIATargetClassReference/UIATargetClass/UIATargetClass.html">JavaScript libraries</a>, that you can use to drive your tests and simulate user interaction. Your custom test scripts are run using the Automation Instrument in Apple's Instruments App, targeting your App either in the Simulator or on an actual device.

You can test almost every aspect of user interaction, using Apple's JavaScript library. No matter if you want to test shaking, device orientation or the basics like tapping and swiping, you can do all that using basic JavaScript function calls. Apple's <a href="https://developer.apple.com/library/mac/#documentation/DeveloperTools/Conceptual/InstrumentsUserGuide/Built-InInstruments/Built-InInstruments.html%23//apple_ref/doc/uid/TP40004652-CH6-SW75">documentation</a> is quite solid, as most of them are, and explains the process in detail.

For "I think I spider" I covered the basic use cases in terms of UI, to make sure it still works after adding new features. Here is a basic example of the JavaScript involved to test "opening" the book, after starting the App:

{% highlight javascript %}
// setup
var target = UIATarget.localTarget();
var appWindow = target.frontMostApp().mainWindow();
var element = target;

// first test
var testName = "Start Screen Test";
UIALogger.logStart(testName);
UIALogger.logMessage("Tapping start screen");
appWindow.elements()["start_screen"].tap(); 

// open the book
if (appWindow.elements()["main_screen"].isValid()) {
  UIALogger.logFail(testName);
} else {
  UIALogger.logPass(testName);
}
{% endhighlight %}
<a class="gist" href="https://gist.github.com/803902">gist</a>

You can see that the JavaScript API is quite easy to use and yet very powerful! After setting this up in the Automation Instrument and running it, you can see the Simulator firing up and tapping the *UIImageView* with the accessibility label "startscreen" after it became available. It then tests, if the main screen of the App was loaded and either passes or fails the test.

In order to make our App testable, I had to set the accessibility labels on the elements we wanted to reference from the script. That was the only change I had to make in our code. Since you should take accessibility into consideration anyways, it was a reasonable effort.

Apple did an awesome job giving us developers the ability to catch regressions and make our life easier. However, there is room for improvement, which has been nicely <a href="http://blog.airsource.co.uk/index.php/2010/08/13/ui-automation-on-the-iphone/">summarized</a> by <a href="http://www.airsource.co.uk">Air Source</a>. For us, a missing *UIALogger.warn* function in the JavaScript library was the biggest downside. Sometimes it's okay for a test to fail under certain conditions, but you still want to get a warning about it. I use *UIALogger.logMessage* for those cases as a workaround, but it's quite easy to miss those lines, since they don't stand out.

Overall, I think it's a huge improvement to have a UI testing tool for iOS Apps at hand. There is room for improvement, but the current state of UI Test Automation is already priceless!