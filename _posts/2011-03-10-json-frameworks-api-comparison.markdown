---
layout: post
title: JSON frameworks API comparison
---

There are dozens of iOS compatible JSON frameworks aka parsers. It's awesome to have the ability to choose between so many different frameworks, however there are differences in terms of performance, API and licensing. I'll take a highlevel peek at couple of them in terms of their API and how to use them in your project. I'll only highlight and compare the JSON consuming part of the API, although serialization works similarly.

All of the frameworks presented here, are released under a license which allows you to use them in closed-source projects, so no problem here. Please keep in mind, that I don't factor in performance. If you are interested there are [lots](http://www.mail-archive.com/cocoa-dev@lists.apple.com/msg61077.html "JSON framework performance") of [comparisons](http://www.cocoanetics.com/2011/03/json-versus-plist-the-ultimate-showdown/ "JSON framework performance") out there.

The first framework I'd like to highlight is [YAJL](https://github.com/gabriel/yajl-objc "YAJL on gihub") (Yet Another JSON Library). I used YAJL in a [couple of projects](http://itunes.apple.com/us/artist/david-linsin/id362714030 "David Linsin on iTunes") and I really like its approach. It's available for Mac and iOS. In order to use it in your project, you can either include it as a static library or add the source code to your Xcode project. In the latter case, you'll need to add other linker flags in your target in order to use YAIL. 

From an [API](http://gabriel.github.com/yajl-objc/ "API docs") point of view, YAIL comes with a bunch of categories on *NSString* or *NSData*, helping you to transform the JSON string into various Objective-C data types. It looks something like this:

{% highlight objectivec %}
#import <YAJLiOS/YAJL.h>
NSString *JSONString = @"[1, 2, 3]";
NSArray *arrayFromString = [JSONString yajl_JSON];
{% endhighlight %}
<a class="gist" href="https://gist.github.com/857288">gist</a>

I really like YAJL's transparent approach using categories, although using it as a static library and configuring linker flags can be a [source of error](http://dlinsin.blogspot.com/2010/05/don-forget-your-linker-flags.html "blog post on linker flags").

The next framework I'd like to talk about is [JSONKit](https://github.com/johnezang/JSONKit "JSONKit on gihub"). I'm using it on my current project at work and so far I'm quite happy. Just like YAJL, JSONKit comes with categories on *NSString* and *NSData*. In addition to that, it has an explicit parsing interface to create objects from those two data types.

{% highlight objectivec %}
#import "JSONKit.h"
NSString *JSONString = @"[1, 2, 3]";
NSArray *arrayFromString = [JSONString objectFromJSONString];
{% endhighlight %}
<a class="gist" href="https://gist.github.com/857294">gist</a>

I like JSONKit, especially because it manages to provide an easy to use API. It also doesn't hurt, that it [seems](http://www.mail-archive.com/cocoa-dev@lists.apple.com/msg61077.html "JSON framework performance") to be quite fast.

At work we use [json-framework](https://github.com/stig/json-framework "json-framework on github") a lot. It doesn't stand out much from the frameworks discussed before. The only real difference is, it has been around for [quite a while](https://github.com/stig/json-framework/commit/108b9ca38dc2fd8ad31db078cfc71b3b4ab10d13 "commit on github"). Just like JSONKit it provides an explicit interface or categories to parse JSON from *NSString* and *NSData*. Let's look at the same example of the previously discussed frameworks:

{% highlight objectivec %}
#import "JSON.h"
NSString *JSONString = @"[1, 2, 3]";
NSArray *arrayFromString = [JSONString JSONValue];
{% endhighlight %}
<a class="gist" href="https://gist.github.com/860623">gist</a>

A nice feature of json-framework's explicit parser interface is the [configuration of parsing depth](http://stig.github.com/json-framework/api/interfaceSBJsonParser.html#a0378b4ce99a1caeddc4a05da37ca4ffa "api docs on github"). It could be useful, if you have to parse large JSON structures and only need the top level objects. 

The last framework I want to peek at is [TouchJSON](https://github.com/TouchCode/TouchJSON "TouchJSON on github"). As with json-framework, I've never used this one in production myself. The only way to get an overview is by looking at a couple of samples and running them in an Xcode project. In order to use TouchJSON, you simply have to include the source in your project. The sample code used to previously illustrate how to use the framework looks a little different:

{% highlight objectivec %}
#import "CJSONDeserializer.h"
NSString *JSONString = @"[1, 2, 3]";
NSData *jsonData = [JSONString dataUsingEncoding:NSUTF8StringEncoding];
NSError *error = nil;
NSArray *array = [[CJSONDeserializer deserializer] deserializeAsArray:jsonData 
                error:&error];
{% endhighlight %}
<a class="gist" href="https://gist.github.com/860676">gist</a>

In contrast to all other frameworks, TouchJSON only supports a category to create a *NSDictionary*. Everything else needs to be done using the explicit interface *CJSONDeserializer*. 

As you can see, almost all API's are used the same way. They all provide categories, except for TouchJSON. You can simply use iOS' datatypes to retrieve native datastructures from JSON. I like categories, especially when used in such a way as the JSON frameworks presented here. It just feels natural to call *objectFromJSONString* on a *NSString* containing JSON. 

There is no clear winner, but I think JSONKit would be my framework of choice, if I had to pick. I love the transparent, intuitive approach of its API and for me that's more important than other aspects of a framework. 