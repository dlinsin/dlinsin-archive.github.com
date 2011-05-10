---
layout: post
title: UITextFields hidden by keyboard
---


In almost every iOS app I developed so far I came across the situation where multiple UITextFields on the screen are hidden behind the keyboard. I almost always developed a custom solution, since I didn't know any better. A couple of weeks ago, again facing the same problem, I came across a [blog post](http://atastypixel.com/blog/a-drop-in-universal-solution-for-moving-text-fields-out-of-the-way-of-the-keyboard/) by Michael Tyson, which features a drop-in UIScrollView component to handle the problem. Unfortunately, he didn't reveal in his post, that this is also [Apple's proposed solution](http://developer.apple.com/library/ios/#documentation/StringsTextFonts/Conceptual/TextAndWebiPhoneOS/KeyboardManagement/KeyboardManagement.html%23//apple_ref/doc/uid/TP40009542-CH5-SW7) to the problem:

> When asked to display the keyboard, the system slides it in from the bottom of the screen and positions it over your application’s content. Because it is placed on top of your content, it is possible for the keyboard to be placed on top of the text object that the user wanted to edit. When this happens, you must adjust your content so that the target object remains visible.
>
>Adjusting your content typically involves temporarily resizing one or more views and positioning them so that the text object remains visible. The simplest way to manage text objects with the keyboard is to embed them inside a UIScrollView object (or one of its subclasses like UITableView). When the keyboard is displayed, all you have to do is reset the content area of the scroll view and scroll the desired text object into position. Thus, in response to a UIKeyboardDidShowNotification, your handler method would do the following:
>
>* Get the size of the keyboard.
>* Adjust the bottom content inset of your scroll view by the keyboard height.
>* Scroll the target text field into view.

When you look at Michael's [code on github](https://github.com/michaeltyson/TPKeyboardAvoiding) you can see, that he went along to creat a set of custom base classes handling those three steps, that Apple suggest to do. I suggest to go, check it out and use it if you can!

In case you cannot use it or don't want to, I created a small sample project for myself to understand what Apple is suggesting. You can find it [on github](http://github.com/dlinsin/district9/KeyBoardHidden/). Almost all the code is from the Apple's documentation. It's the bare minimum without any animation or fancy schmancy design, but I believe it gives you an idea of how to apply it to your code. 
