---
layout: post
title: Dismiss Keyboard on Tap "Outside"
---

In almost every App I've developed so far, the client requested to be able to dismiss the keyboard by tapping "outside" of an input area like an *UITextField* or *UITextArea*. I guess it's kind of a natural thing, especially on the iPad, where you can see a lot more content and have this urge to "move on" after entering some data. Apple's built-in Apps support it to some extend. For example, if you search for a contact on your iPhone and tap the dark area, covering the *UITableView", the keyboard is being dismissed.

I always managed to get the job done somehow, but was never really satisfied with the solution. Last week, I had to implement this very requirement again and took a step back to think about a more general approach.

The first step to dimiss the keyboard by tapping outside an input area, is to actually be able to detect the tap. Take a look at Apple's approach in Safari.app, when you enter an URL: it adds a dark translucent layer to the content view in order to detect the tap outside the *UITextField*. It also prevents accidental taps on any element in the content area. 

You can do the same in your App: In your *UIViewController*, you can listen to *UIKeyboardDidShowNotification* and *UIKeyboardWillHideNotification*, in order to add/remove a *UIView* receiving the taps. It doesn't necessarily need to be a dark translucent layer like in Safari.app, it could be transparent. I've [blogged about those to notifications before](http://dlinsin.github.com/2011/05/11/KeyBoardHiddenTextFields.html) and posted some [sample code on github](https://github.com/dlinsin/district9/blob/master/KeyBoardHidden/KeyBoardHidden/KeyBoardHidden/KeyBoardHiddenViewController.m), in case you have no idea what I'm talking about. I've never really though about this before, but it is a general approach, you can take in order to detect taps outside a *UITextField* or any other element that takes an input.

The second step is to actually dismiss the keyboard. So far we only know, if a user taps outside an input area. I always thought there must be a way to tell the keyboard to dismiss, however the [docs](http://developer.apple.com/library/ios/#documentation/StringsTextFonts/Conceptual/TextAndWebiPhoneOS/KeyboardManagement/KeyboardManagement.html%23//apple_ref/doc/uid/TP40009542-CH5-SW7) clearly state you are on your own. That means you need to call *resignFirstResponder* on the input element currently active. Fortunately, it's not too hard to go from detecting a tap to finding and resigning the first responder. I found a [neat category on stackoverflow](http://stackoverflow.com/questions/1823317/how-do-i-legally-get-the-current-first-responder-on-the-screen-on-an-iphone/1823360#1823360), which does exactley that:

{% highlight objectivec %}
@implementation UIView (FindAndResignFirstResponder)
- (BOOL)findAndResignFirstResponder
{
    if (self.isFirstResponder) {
        [self resignFirstResponder];
        return YES;     
    }
    for (UIView *subView in self.subviews) {
        if ([subView findAndResignFirstResponder])
            return YES;
    }
    return NO;
}
@end
{% endhighlight %}
<a class="gist" href="https://gist.github.com/1008470">gist</a>

You simply add this category to your *UIViewController* and it's just one method call to go from detecting the tap to dismissing the keyboard.

The code to listen to the *UIKeyboardNotifications* in order to add the *UIView* to intercept the taps, as well as resigning the first responder, could go into your AppDelegate or a base *UIViewController*. It depends on your needs, I guess. However, I think this is a general approach to handle this requirement in your app.  
