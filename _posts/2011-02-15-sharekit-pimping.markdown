---
layout: post
title: ShareKit Pimping
---

A couple of months ago, I <a href="http://dlinsin.blogspot.com/2010/11/word-buzz-getting-better-twitter.html">improved Word Buzz' Twitter sharing feature</a> significantly, by leveraging a <a href="https://github.com/dlinsin/iphone-twitter">tweaked version</a> of an existing framework. Unfortunately, I had only heard of <a href="http://getsharekit.com">ShareKit</a> at that time, that's the reason why I decided to implement my own solution!

In case you don't know about ShareKit or like me only heard about it:

>SharKit adds full sharing capabilities to your App. It's a drop-in library, which supports services like Twitter, Facebook, Instapaper and many more. You can share links, text and pictures with a customizable user interface. It evens queues shared items until an internet connection is available.

SharKit is awesome and I really regret not using it to add Twitter sharing to <a href="http://itunes.apple.com/app/word-buzz/id388372038?mt=8">Word Buzz</a>. It has a well documented API and is really easy to extend, there's even a step-by-step guide on ShakreKit's website, which describes the process. I followed that guide to add <a href="https://github.com/dlinsin/ShareKit">TwitPic and yfrog capability</a> to ShareKit for one of our next <a href="http://twitter.com/furryfishApps">furryfishApps</a> projects and that's what I'd like to write about in this post.

ShareKit comes with built-in Twitter support, which you can find in *SHKTwitter* and its authentication form *SHKTwitterForm*. It uses <a href="http://bit.ly">bit.ly</a> to share images, which has a similar API as TwitPic and yfrog. I piggybacked on that implementation, however dropped oAuth support in favor of xAuth.

I know there are <a href="http://hueniverse.com/2010/06/xauth-a-terrible-horrible-no-good-very-bad-idea/">a lot of discussions</a> on xAuth, however I found it the <a href="http://www.reynoldsftw.com/2010/03/using-xauth-an-alternate-oauth-from-twitter/">easiest way</a> to provide the most benefit for iPhone App users, without compromising security in a hurtful way. In order to get your iPhone App ready to use xAuth with Twitter, you need to sign up at <a href="http://developer.twitter.com/">http://developer.twitter.com/</a>. I described the process in a <a href="http://dlinsin.blogspot.com/2010/11/word-buzz-getting-better-twitter.html">previous post</a>.

The previously mentioned class *SHKTwitter* inherits from *SHKOAuthSharer*, which does all the heavy lifting in terms of authentication for you! All you need to do is hook into the API calls and customize your authentication screen:

{% highlight objectivec %}
return [NSArray arrayWithObjects:
  [SHKFormFieldSettings label:SHKLocalizedString(@"Username") key:@"username" 
    type:SHKFormFieldTypeText start:nil],
  [SHKFormFieldSettings label:SHKLocalizedString(@"Password") key:@"password" 
    type:SHKFormFieldTypePassword start:nil],
  [SHKFormFieldSettings label:SHKLocalizedString(@"Send to Twitter") 
    key:@"sendToTwitter" type:SHKFormFieldTypeSwitch start:SHKFormFieldSwitchOn],nil];
{% endhighlight %}
<a class="gist" href="https://gist.github.com/827260">gist</a>

So let's say the user wants to share a picture, taps on the share icon and select TwitPic. He authenticates after being prompt for his Twitter credentials. When the authentication was successful, you want to show some sort of form to your users, where they can enter a comment or in case of Twitter, their status. You can totally customize the UI, without any dependency to ShareKit. In fact *SHKTwitterForm*, ShareKits built-in Twitter form, is a simple *UIViewController* with its delegate set to *SHKTwitter*.

The actual sharing part of the code is as straight forward as the rest of ShareKit. It's a little verbose, but once your understood the concept, it's easy to extend:

{% highlight objectivec %}
- (void)sendImage {

NSString * oauthHeader = [self oauthHeader];

NSURL *serviceURL = [NSURL URLWithString:@"http://yfrog.com/api/xauth_upload"];
OAMutableURLRequest *oRequest = [[OAMutableURLRequest alloc] initWithURL:serviceURL
consumer:super.consumer
token:super.accessToken
realm:@"http://api.twitter.com/"
signatureProvider:super.signatureProvider];

[oRequest prepare];
[oRequest setValue:nil forHTTPHeaderField:@"Authorization"];

[oRequest setHTTPMethod:@"POST"];
[oRequest setValue:@"https://api.twitter.com/1/account/verify_credentials.json" 
  forHTTPHeaderField:@"X-Auth-Service-Provider"];
[oRequest setValue:oauthHeader 
  forHTTPHeaderField:@"X-Verify-Credentials-Authorization"];

NSString *boundary = @"a21ff70823f9";
NSString *contentType = [NSString stringWithFormat:@"multipart/form-data; 
                                                  boundary=%@",boundary];
[oRequest setValue:contentType forHTTPHeaderField:@"Content-Type"];

NSMutableData *body = [NSMutableData data];

[body appendData:[[NSString stringWithFormat:@"--%@\r\n",boundary] 
  dataUsingEncoding:NSUTF8StringEncoding]];
[body appendData:[@"Content-Disposition: form-data; name=\"key\"\r\n\r\n" 
  dataUsingEncoding:NSUTF8StringEncoding]];
[body appendData:[self.yfrogAPIKey dataUsingEncoding:NSUTF8StringEncoding]];
[body appendData:[@"\r\n" dataUsingEncoding:NSUTF8StringEncoding]];

[body appendData:[[NSString stringWithFormat:@"--%@\r\n",boundary] 
  dataUsingEncoding:NSUTF8StringEncoding]];
[body appendData:[@"Content-Disposition: form-data; name=\"media\"; 
  filename=\"upload.jpg\"\r\n" 
  dataUsingEncoding:NSUTF8StringEncoding]];
[body appendData:[@"Content-Type: image/jpg\r\n\r\n" 
  dataUsingEncoding:NSUTF8StringEncoding]];
[body appendData:[self imageData]];
[body appendData:[@"\r\n" dataUsingEncoding:NSUTF8StringEncoding]];

[body appendData:[[NSString stringWithFormat:@"--%@--\r\n",boundary] 
  dataUsingEncoding:NSUTF8StringEncoding]];

[oRequest setHTTPBody:body];

[self sendDidStart];

// Start the request
OAAsynchronousDataFetcher *fetcher = [OAAsynchronousDataFetcher 
asynchronousFetcherWithRequest:oRequest
delegate:self
didFinishSelector:@selector(sendImage:didFinishWithData:)
didFailSelector:@selector(sendImage:didFailWithError:)];

[fetcher start];

[oRequest release];
}
{% endhighlight %}
<a class="gist" href="https://gist.github.com/827294">gist</a>

As you can see most of the work goes into setting up the authentication headers for the request, as well as filling in the elements of the request body. There are APIs like <a href="http://allseeing-i.com/ASIHTTPRequest">ASIHTTPRequest</a>, which handle this for you, however ShareKit doesn't use them and I didn't want to introduce a 3rd party library. If you take a look at <a href="https://github.com/Gurpartap/GSTwitPicEngine">Gurpartap's TwitPic engine</a>, you can see how easy and simple the code would be.

Overall it's a breeze to develop with <a href="http://getsharekit.com">SharKit</a> and I'm glad I digged in deeper. For our next project we'll definitely use it and you should at least take a look at it before rolling your own implementation.