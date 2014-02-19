---
layout: post
category : lessons
tagline: "Supporting tagline"
tags : [intro, beginner, jekyll, tutorial]
---
{% include JB/setup %}

tl;dr: If you’re building a web app (tree, search, etc) yes. Else probably not.

All,

A recent email chain has reminded me that we should probably touch on what our current Angular.js policy is.


Angular.js is good at what it’s good at

Angular.js is a framework for building rich, client-driven web applications. Angular.js is not a tool to make websites. Take Node.js for example: if I were building a web app to do functional calculations (like the Fibonacci sequence), I would not choose to use Node.js. If I were building a CMS or “front-end bland” website, I would not choose Angular.js. If I was building something that isn’t very dynamic and is (and should be) just server-rendered information that is not going to have interaction, I would not choose Angular.


Angular.js is our choice for front-end applications

When we decided we wanted to change from using our own home-grown solution for building a single-page app to using a community-grown one, we looked at a few options: Angular.js, Backbone.js, and Ember.js being at the forefront. A few of us sat down in a conference room and talked pros/cons of each. One of the biggest wins for Angular was that it was already very similar to Gadgets, which was our home-grown solution. There was still a learning curve, but they had made many of the same decisions we did. With that and other wins, we went with Angular.js as our choice.


Angular.js is NOT for everyone

If you — as a FamilySearch Front-end Dev — are building a [single-page] web application, you should be using Angular.js. Obviously this does not apply right out of the box for apps that we already have (e.g. tree), but we have migration paths for such, and all new applications should be build in Angular. If you’re not building an application, you should not be using Angular. If you are building an application, you should probably be using Angular. If you’re trying to get what you have to become an application, go ahead and start using Angular so that you can become familiar and begin the migration. Otherwise, Angular.js is just too "big and bloated" to be used as a toolset if you don’t need most of the tools. If all you need is directives, you might just need Controls.


What is a Web Application?

The definition of “application” is the hard part. Here are some of the things that I think about:

Am I going to be using forms to change data that is displayed on the page? (binding)
Am I going to be saving off a lot of data (services)?
Am I going to be building a large “page” with a lot of dynamic server-driven (and changing) content?
Would this “page” benefit from small reusable pieces that each knows how to handle itself? (directives)
Do I need client-side route handling? (single-page app)

If you don’t fall into these bins, I suggest that you are not a web application, and you do not need Angular. You may simply need a Control to give yourself a little client-side functionality. You may need a few lines of jQuery or Bootstrap to make a popups, hovers, or drop downs.


Angular is too big and bloated

I really want to reiterate this one. Angular.js (as with any tool set) is just too "big and bloated" to be used as a toolset if you don’t need most of the tools. If all you wanted was jQuery’s dom-selection, you probably want Sizzle. If all you wanted was Underscore’s _extend, only use the function (paste that function in your code, documenting accordingly). If all you need is Angular#Directive, you might just need Frontier Controls.


Caveat and Corrections

This is the policy as I’ve been trying to help preach it. I want to state up front (though technically last in this email) that it may contain fallacies I’m not aware of or policy that may change or have changed since I last visited this topic. I especially encourage any correction from any manager, supervisor, etc. who have more insight (and weight) into the issues and policies than I do. Nic, Tyler, Rob, Bryan, this is especially to you guys. Please call out anything I may have overlooked.
