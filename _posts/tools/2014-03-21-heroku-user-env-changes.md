---
layout: post
category : tools
title: What you should know about Heroku buildpack environment changes
tags : [tools, hosting, Heroku, buildpacks, env_dir, user-env-compile]
---
{% include JB/setup %}

# Overview
Heroku allows you to set environment variables during the buildpack compilation
stage of your build, but the method of doing so is changing. Be advised.

<!--more-->

## What are Buildpacks?

[Heroku](https://heroku.com) is a hosting provider for virtually any kind of web app.
They are a simple and inexpensive alternative for standard hosting, and they support
a multitude of languages, frameworks, and tools. You can even customize their offerings
by extending their built-in functionality with something called ["buildpacks"](https://devcenter.heroku.com/articles/buildpacks).
Stated bluntly: the only reason they offer, for example, NodeJS support is basically
because they have a buildpack FOR Node.js. When slug compilation begins, they trigger
your buildpacks, which set up your environment for you.


## Enter user-env-compile
During this compilation stage, the environment variables you have defined are not
yet compiled into the environment, and are not yet available. Heroku created a
"labs feature" to address this called "user-env-compile". This was an opt-in feature
(that's what their labs are) that precompiled the environment before the compilation
stage, so that your buildpack could use environment variables. Formerly, you simply
enabled the feature `heroku labs:enable user-env-compile`, and you had access to
those variables in your buildpacks.

## Exit user-env-compile; Enter ENV_DIR
This feature is now going away, to be replaced with ENV_DIR. ENV_DIR is a feature
that is enabled for all apps (not an opt-in lab), and uses a directory of your
variables, instead of simply precompiling them into the script environment beforehand.
On one hand, Heroku no longer has to include all of the variables you've defined.
On the other, you now have to manually inject your variables into the environment
for yourself. Fortunately, I can show you how.

According to the documentation, the buildpack compile step is called as:
```
bin/compile BUILD_DIR CACHE_DIR ENV_DIR
```
$ENV_DIR is that 3rd parameter, so we can use that for our benefit. Let's say we
had a script that would check to make sure that you had a couple variables set,
and would just echo them. Here's how you used to do it:
```bash
# Former way of accomplishing this

[ -z "$ENV_VAR1" ] && echo "You didn't set $ENV_VAR1, and this is required." && exit 1
[ -z "$ENV_VAR2" ] && echo "You didn't set $ENV_VAR2, and this is required." && exit 1

echo "HOORAY, you set the variables! ENV_VAR1: $ENV_VAR1; ENV_VAR2: $ENV_VAR2."
```

```bash
# New way of doing it
ENV_DIR=$3 # remember, it was the 3rd parameter passed in up there
for KEY in ENV_VAR1 ENV_VAR2; do
  [ -f $ENV_DIR/$KEY ] && export "$KEY=$(cat $ENV_DIR/$KEY)"
  [ -z "${!KEY}" ] && echo "You didn't set $KEY, and this is required." && exit 1
done
echo "HOORAY, you set the variables! ENV_VAR1: $ENV_VAR1; ENV_VAR2: $ENV_VAR2."
```

It's a pretty straight-forward change. Basically, instead of the variables being
auto-set into your environment, they're just files in ENV_DIR that you need to
`cat` the values from.

Hope it helps. Hit up the comments if you have any questions / feedback. Big
thanks to [@ryanbrainard](https://twitter.com/ryanbrainard) for the guidance
in figuring all of this out.
