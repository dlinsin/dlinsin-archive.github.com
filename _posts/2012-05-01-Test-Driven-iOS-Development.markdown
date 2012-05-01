---
layout: post
title: Test-Driven iOS Development
---


A couple of weeks ago, I started reading [_Test-Driven iOS Development_](http://www.amazon.de/gp/product/0321774183?ie=UTF8&tag=mytakeonthing-21&linkCode=as2&camp=1638&creative=6742&creativeASIN=0321774183) 
by [Graham Lee](http://twitter.com/secboffin). I had a blast reminiscing about my days as a 
Java developer, where every piece of code had a _unit test_ counterpart.

Graham is doing a great job introducing the notion behind unit testing and answering the basic question 
of why you should write unit tests for your code. The book mentions unit tests can be documentation, 
help you think about API design and a way to get to know [other people's code](http://dlinsin.blogspot.de/2007/07/hell-is-other-peoples-code.html). 

I especially like the way Graham talks about _Refactoring_. I've read a couple of books on 
this kind of topic, the difference with [_Test-Driven iOS Development_](http://www.amazon.de/gp/product/0321774183?ie=UTF8&tag=mytakeonthing-21&linkCode=as2&camp=1638&creative=6742&creativeASIN=0321774183) 
is that I really enjoyed how _Refactoring_ is a steady topic through-out the whole book. 

For me one of the most important reasons for writing unit tests is not so much to show that 
something works _now_, but to have that safety net some time in the _future_, which helps you 
to make sure things still work after refactoring your code. 

Graham uses a sample App, which is available on [Github](https://github.com/iamleeg/BrowseOverflow), 
to show how to approach unit testing on basically every layer of an iOS App. It covers 
setting up OCUnit in Xcode, a couple of interesting testing frameworks and tools, all the way 
to testing the view layer with a _UITableView_. 

The most interesting aspects of the chapters about the sample App, was how to design your classes 
with testing in mind. I've never been a big proponent of a [test-first](http://en.wikipedia.org/wiki/Test-first), 
however, Graham shows with no doubt, that it has advantages. The most important one, in my 
opinion, is that it makes you _think_ about the API of your class, _before_ starting to code. 

Overall, [_Test-Driven iOS Development_](http://www.amazon.de/gp/product/0321774183?ie=UTF8&tag=mytakeonthing-21&linkCode=as2&camp=1638&creative=6742&creativeASIN=0321774183) 
is really worth reading, especially if you are new to test-driven development or need some revision on 
the topic. The book contains lots of code and even though I usually don't mind, I sometimes had a 
hard time staying on top of it.

If you are not practicing test-driven development today, I highly recommend reading [_Test-Driven iOS Development_](http://www.amazon.de/gp/product/0321774183?ie=UTF8&tag=mytakeonthing-21&linkCode=as2&camp=1638&creative=6742&creativeASIN=0321774183) 
and let Graham show you its benefits. 