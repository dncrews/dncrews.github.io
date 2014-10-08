---
layout: post
category : webdev
title: Localhost and Mobile Devices
tagline: "What are your options, and how do you do them?"
tags : [webdev, proxy, mobile]
---
{% include JB/setup %}

## Problem

Web development is fun. Building a layout that is responsive to any
device is a great thing. Unfortunately, testing it in your desktop
web browser is not always good enough, and you don't want to "push
to prod" without testing it properly on your phone. What can be done?

<!--more-->

## Solutions

Well, you've got a couple choices, depending on what your requirements are:

### IP Address

Say you're starting a Node.js (or whatever) server, and your app is listening
on port 5000. It's really listening at 0.0.0.0:5000, which means "if the network
comes to me on that port, whatever they're asking for, serve this".

As long as your mobile device is on the same wifi network, you can run 
```sh
$ ifconfig
```
from your Mac which returns a bunch of information. Look for your IPv4
address in there. It's probably 10.x.x.x or 192.x.x.x. Then in your mobile
browser, you're just going to hit your IP address + your port number:

```
http://192.168.0.5:5000
```

### Proxy

Well, what if you can't just have any old domain name. e.g. What if you have are
using oAuth2, for authentication, and you have to manually configure your callbacks.
Then there's going to be the problem that you have to set up your OAuth callbacks
every time your IP changes, and no one wants to do that:

```
http://localhost:5000/auth/callback
http://192.168.0.5:5000/auth/callback
http://192.168.0.7:5000/auth/callback
http://192.168.0.15:5000/auth/callback
```

What you can do instead is grab yourself an HTTP proxy and use that to handle this
for you. I personally have a Charles license, so I'll show you that. I'm using Charles
v3.9.2:

From Charles -> Proxy -> Proxy Settings

Here are the defaults. We'll stick with that.

![Charles Settings]({{ site.url }}/assets/img/charlesSettings.png)

Now we will use the IP address for our computer as a proxy for our mobile device:

```sh
$ ifconfig

# It doesn't really look like this, but find it
192.168.0.5
```

Here's what the setting looks like on an iPhone:

![Wifi Proxy Settings]({{ site.url }}/assets/img/wifiSettings.jpg)

Now we need to define a domain name we'd like to use for our local development
that we will be happy using for our secondary oauth callback. Don't forget your
port number:

```
http://superawesomewebsite.dev:5000/auth/callback
```

Now we just have to set that up in our system. I'll use `nano` because it's easy:

```sh
$ sudo nano /etc/hosts
Password:
```

Now you'll see something like this:

```sh
##
# Host Database
#
# localhost is used to configure the loopback interface
# when the system is booting.  Do not change this entry.
##
127.0.0.1       localhost
255.255.255.255 broadcasthost
::1             localhost
```

and we're going to add a line to the end:

```sh
127.0.0.1       superawesomewebsite.dev
```

Save and exit.

Now we'll use that url from our mobile device:

```
http://superawesomewebsite.dev:5000
```

and Voila! You know have a set domain for use in your mobile device.

(hopefully it was easy enough to justify the "voila")
