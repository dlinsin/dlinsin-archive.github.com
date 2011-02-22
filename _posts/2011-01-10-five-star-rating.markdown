---
layout: post
title: 5 Star Rating
---

A <a href="http://dlinsin.blogspot.com/2010/09/i-think-i-spider.html">couple of months ago</a> we release our first own App "<a href="http://mobile.synyx.de/2010/09/i-think-i-spider-1-0-released/">I think I spider</a>" at Synyx. It features German quotes and sayings directly translated to English. It doesn't make much sense to a none-native German speaker, but believe me it's hilarious for us.

The App let's you rate those quotes with a 5 star rating, which is directly incorporated into a ranking. Up until today the component in charge of the ranking is a simple bunch of *UIImageViews* wired up with Interface Builder and set appropriately when tapped. That means if you want to give a 3 star rating, tapping on the 3rd *UIImageView* would fill up the 2 previous one as well. Same goes for changing your mind and going from a 5 to 3 star rating. The logic would unhighlight the 4th and 5th star.

Now, this works great and it certainly looks beautiful, but have you ever rated an App in the App Store on your iOS device? This is how it looks like:

<object width="480" height="385"><param name="movie" value="http://www.youtube.com/v/cbOll4SWwmU?fs=1&amp;hl=en_US"></param><param name="allowFullScreen" value="true"></param><param name="allowscriptaccess" value="always"></param><embed src="http://www.youtube.com/v/cbOll4SWwmU?fs=1&amp;hl=en_US" type="application/x-shockwave-flash" allowscriptaccess="always" allowfullscreen="true" width="480" height="385"></embed></object>

Apple did a great job of just getting everything right with this small little control. The way you can slide your finger over it and the stars light up is just great. Also notice that if you want to reset the rating and go down to 0 stars, you need to swipe your finger all the way to the left. Note, that you can also touch slightly below the star, in order to see the stars above your fingers.

All those little details were the requirements for the next version of the rating feature of <a href="http://itunes.apple.com/de/app/i-think-i-spider/id390639989?mt=8">I think I spider</a>. However, having some spare time over the holidays, I though I'd write a little component, which does all of that and more: <strong>DLStarRating</strong>. You can find the code on <a href="https://github.com/dlinsin/DLStarRating">github</a>, along with a sample project of how to use the stuff in your next App.

<object width="480" height="385"><param name="movie" value="http://www.youtube.com/v/0fpeBo2H7Tc?fs=1&amp;hl=en_US"></param><param name="allowFullScreen" value="true"></param><param name="allowscriptaccess" value="always"></param><embed src="http://www.youtube.com/v/0fpeBo2H7Tc?fs=1&amp;hl=en_US" type="application/x-shockwave-flash" allowscriptaccess="always" allowfullscreen="true" width="480" height="385"></embed></object>

*DLStarRating* consists of a configurable number of custom *UIButtons* called *DLStarView*. They have a different background image for their normal and highlighted state. Those buttons are wrapped in a *UIControl* called *DLStarRatingControl*, which does all the touch handling. The buttons are centered in the *DLStarRatingControl* so keep that in mind when configuring its size.

It's quite easy to use *DLStarRating* in your code. You can wire it up in Interface Builder (although you won't be able to configure it from there) or in your *UIViewController* subclass:

{% highlight javascript %}
DLStarRatingControl *customNumberOfStars = 
  [[DLStarRatingControl alloc] initWithFrame:CGRectMake(0, 230, 320, 230) andStars:3];
customNumberOfStars.backgroundColor = [UIColor groupTableViewBackgroundColor];
customNumberOfStars.autoresizingMask =  UIViewAutoresizingFlexibleLeftMargin | 
                                        UIViewAutoresizingFlexibleWidth | 
                                        UIViewAutoresizingFlexibleHeight | 
                                        UIViewAutoresizingFlexibleRightMargin | 
                                        UIViewAutoresizingFlexibleTopMargin | 
                                        UIViewAutoresizingFlexibleBottomMargin;
customNumberOfStars.rating = 2;
[self.view addSubview:customNumberOfStars];{% endhighlight %}
<a class="gist" href="https://gist.github.com/772510">gist</a>

To customize the stars, you can replace *star.png* and *star_highlighted.png* in the images folder under *DLStarRating* with your own. The only requirement is that the two images must have the same size.

If you discover any bugs or have a great idea you want implemented, open an issue on <a href="https://github.com/dlinsin/DLStarRating/issues">github</a> or fork the project and help me out!