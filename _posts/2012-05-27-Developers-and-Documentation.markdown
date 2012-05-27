---
layout: post
title: Developers and Documentation
---


The relationship between developers and documentation can be described like the bond 
between cats and dogs. They are on totally different levels of the food chain, so sometimes 
the relationship works out, but most of the time it doesn't. If the cat and dog get along well 
you'll have a happy home, but if they don't you'll live in a state of toleration - nothing 
more and nothing less. 

It is said that the best way of forming a healthy bond between a cat and a dog is to bring 
them up together. They'll get to know each other from the beginning and learn to respect 
each other. I think that works well for the relationship of developers and documentation as well.

When talking about documentation it's important to differentiate. There are lots of 
different kinds of documentation. Here's an excerpt: 

* comments in your code like _Javadocs_
* API docs in your code, framework or backend-service
* Use Cases, None-Functional Requirements
* Project Planing Documentation

In my book, all of the mentioned above are important and when I say documentation, I do mean 
all of the above. I realize, that depending on where you work and what your job is, only a
subset of the list applies to you. However, your bond or relationship with documentation can 
be described the very same way - no matter which kind documentation you come across.

When I was in university I took a class called "Software Engineering" - an introduction to 
[Object Oriented Analysis and Design](http://www.amazon.de/gp/product/0131489062?ie=UTF8&tag=mytakeonthing-21&linkCode=as2&camp=1638&creative=6742&creativeASIN=0131489062). 
The goal of the course was to fully analyze, design and implement a problem using _[UML](http://en.wikipedia.org/wiki/Unified_Modeling_Language)_ 
and the _[Unified Process](http://en.wikipedia.org/wiki/Unified_Process)_. Each step of the 
way would lead to a piece of documentation and ultimately to code. 

It was back then when I realized that __developing software is more than simply hacking away__. 
and I have been a [big proponent](http://dlinsin.blogspot.de/2008/06/does-your-api-docs-leave-users-in-dark.html) 
of documentation ever since. I believe in the value of __transparently sharing your thoughts 
and describing your ideas for fellow team members in other ways than code__. 

Now, don't get me wrong. I'm not at all for creating tons and tons of documentation and diagrams 
along with your actual code. In our "Software Engineering" course we created _Use Case Descriptions_, 
_Domain Models_, _Interaction Diagrams_ and _Class Diagrams_ - which all had their value - but 
were outdated as soon as one single variable changed at the beginning of the chain. 

Instead of going overboard, I suggest to __create as much documentation as necessary and 
as little as possible__.  

One of the most prominent excuses for not creating documentation is that no one will read 
it anyways later on. So ultimately there's no value in creating it in the first place. As you can see 
that's a classic catch-22. The poster child example for breaking this viscous circle is Apple. 
If you look at their [excellent documentation](http://dlinsin.blogspot.de/2009/12/book-review-iphone.html) 
of e.g. `UIKit`, you can see that people do read good documentation and that there is 
value in creating it. 

That's only an example for one bullet point of kinds of documentation mentioned before - API 
docs. However, I can ensure you, that __good documentation has value across all parts of your organization__. 

The second most stated excuse for not documenting your development efforts is that it takes 
too much time. There is never and there will be never enough time! That's a fact you'll have 
to get used to when developing software professionally. 

However, I worked on a mid-size enterprise project a couple of years ago, where we had to 
port a legacy application to a new technology stack. Of course there was close to zero 
documentation on the old application. The project manager decided to have a _documentation 
sprint_, in order to get as much knowledge from the soon to be put-off developers. So there 
actually was enough time for the developers to properly document their thoughts and ideas, 
but you can imagine how much value the documentation had in the end. If I remember correctly, 
I didn't look at it once. 

No matter if you have enough time or not, I suggest __treating documentation as an integral 
part of your development rather than an extension__ or a separate thing to do at the end. 
It'll come naturally after a while and you won't put it off until it will be cut due to 
time constraints.  

Now, I don't want to get into the process/tools/standards discussion, where I 
suggest a Methodology or a tool, that is supposed to solve all problems - including the 
documentation-lazy developers. Instead, I'd like to appeal to all developers to change 
their __mindset__ about documentation and follow these simple guidelines:

* transparently share your thoughts and describe your ideas for fellow team members in 
other ways than code
* create as much documentation as necessary and as little as possible
* realize that good documentation has value across all parts of your organization - not only 
developers
* treat documentation as an integral part of your development rather than an extension

My approach of how you could try to implement this mindset in your organization, team or dev 
shop might be part of one of my next blog posts - but I guess nobody would read it and 
I won't have time anyways.