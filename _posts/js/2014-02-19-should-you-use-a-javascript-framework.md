---
layout: post
category : javascript
title: Should I use a JavaScript framework?
tagline: "If you’re building a web app yes. Else no."
tags : [framework, javascript, angular.js, ember.js, backbone.js]
---
{% include JB/setup %}


***tl;dr: If you’re building a web app yes. Else no.***

## Purpose

JS Frameworks are wonderful. They provide a great set of tools to do all of the
boring stuff no one wants to write over and over again. In our world, people often
want to try out a new toy, and if they like it, they want to use it for EVERYTHING.
When I noticed that trend happening within my current organization [FamilySearch](http://familysearch.org "FamilySearch.org"),
I wrote [basically] the following in an email to our discipline. You will find I
say "Angular.js" a lot for 2 reasons: 1) that's the framework we chose for our own,
2) I was trying to make a point, so I reiterated the topic often.

<!--more-->

## JS Frameworks are good at what they're good at

Angular.js is a framework for building rich, client-driven web applications.
Angular.js is not a tool to make websites. Take Node.js for example: if I
were building a web app to do functional calculations (like the Fibonacci
sequence), I would not choose to use Node.js. If I were building a CMS or
"front-end bland" website, I would not choose Angular.js. If I was building
something that isn’t very dynamic and is (and should be) just server-rendered
information that is not going to have interaction, I would not choose Angular.


## Angular.js is our choice for front-end applications

When we decided we wanted to change from using our own home-grown solution for
building a single-page app to using a community-grown one, we looked at a few
options: Angular.js, Backbone.js, and Ember.js being at the forefront. A few of
us sat down in a conference room and talked pros/cons of each. One of the biggest
wins for Angular was that it was already very similar to "Gadgets", which was our
home-grown solution. There was still a learning curve, but they had made many
of the same decisions we did. With that and other wins, we went with Angular.js
as our choice.


## JS Frameworks are NOT for everyone

If you - as a theoretical FamilySearch Front-end Dev - are building a [single-page] web
application, you should be using Angular.js. Obviously this does not apply
right out of the box for apps that we built using Gadgets, but we have
migration paths for such, and all new applications should be build in Angular.
If you’re not building an application, you should not be using Angular. If you
are building an application, you should probably be using Angular. If you’re
trying to get what you have to become an application, go ahead and start using
Angular so that you can become familiar and begin the migration. Otherwise,
Angular.js is just too **big and bloated** to be used as a toolset if you don’t
need most of the tools. If all you need is directives, you might just need Controls.


## What is a Web Application?

The definition of "application" is the hard part. Here are some of the things that I think about:

- Am I going to be using forms to change data that is displayed on the page? (binding)
- Am I going to be saving off a lot of data (services)?
- Am I going to be building a large "page" with a lot of dynamic server-driven (and changing) content?
- Would this "page" benefit from small reusable pieces that each knows how to handle itself? (directives)
- Do I need client-side route handling? (single-page app)

If you don’t fall into these bins, I propose that you are not a web application,
and you do not need a JavaScript framework. You may simply need a tool to give
yourself a little client-side functionality.


## JS Frameworks are too big and bloated

I really want to reiterate this one. Any framework is just too "big and bloated"
to be used as a toolset if you don’t need most of the tools. If all you wanted
was jQuery’s dom-selection, you probably want [Sizzle](http://sizzlejs.com/).
If all you wanted was Underscore’s \_extend, only [use the function](http://underscorejs.org/docs/underscore.html#section-84)
(paste that function in your code, documenting accordingly). If all you need is
Angular#Directive, you might just need [Controls](https://github.com/schlegelrock/Control.js).

## Final Thoughts

JS Frameworks (in our case Angular.js) are wonderful. They provide a great set of
tools to do all of the boring stuff no one wants to write. However, there is a common
desire for people to want to write **everything** in their new language of favor.
This is a mistake. Always choose a tool based on if it's right for your job.
