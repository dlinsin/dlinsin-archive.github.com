---
layout: post
title: Mantis to Issues Safari Extension
---


Back in January I wrote a [Safari Extension](https://extensions.apple.com/) called [Mantis-Issues-Ext](https://github.com/dlinsin/Mantis-Issues-Ext):

> It extracts information from an issue of a Mantis bugtracking system and adds it to a GitHub issue

It's available on [GitHub](https://github.com/dlinsin/Mantis-Issues-Ext/downloads), where you can download it or directly install it into Safari.

At my day job our whole development workflow is based on GitHub. We document our 
requirements, push our code and keep our issues in GitHub. Unfortunately, our customers are 
using different systems. Among others, the horrible [Mantis Bug Tracker](http://www.mantisbt.org/). 

Instead of going the route of forcing our customers to use our system, we are usually going 
the extra mile of maintaining two systems - e.g. Mantis and GitHub (at least for issues). In 
order to make life easier for our developers, I came up with Mantis-Issues-Ext. 

Here is how it works: you can navigate to an issue in Mantis, hit a shortcut, create a 
new issue in GitHub and with another shortcut fill in all the relevant information. 

Although it doesn't help with the maintenance part, it makes life easier when creating issues.

Now let me say that I'm not a JavaScript guru and Safari Extensions are mainly based 
on JavaScript. I don't really enjoy developing with web technologies - I'm a downright native 
guy. That said, I think my code probably sucks and could definitely be improved. However, it 
works and that's the main goal of this extension.

Apple makes a great job - as always - in [documenting Safari Extentions](http://developer.apple.com/library/safari/#documentation/Tools/Conceptual/SafariExtensionGuide/Introduction/Introduction.html). 
However, the development experience in Safari is not as great as I would have imagined. 
You need to add a lot of logging in order to really see what's going on, but I guess if 
JavaScript is your thing, it should be quite easy for your to get something going. 

Unfortunately, I wasn't able to setup an automatic update mechanism for [Mantis-Issues-Ext](https://github.com/dlinsin/Mantis-Issues-Ext) 
yet. You need to fiddle with the MIME types of your web server and I just don't have anything 
in place for that. 

I hope Mantis-Issues-Ext makes life easier for some folks out there and helps you focus on 
working in GitHub instead of Mantis.