---
layout: documentation
# permalink:
title: Build And Release Pipeline
categories: Development
tags:
  - no_menu
---

## Build and Release Pipeline
1. Update CHANGELOG to reflect all of the changes that has happened between last release and now. The Unreleased link in the CHANGELOG gives you a nice diff.
1. make sure the README is updated as neccessary.
1. Update the version using [semver2](http://semver.org/spec/v2.0.0.html)
1. make a git release. Example with hub: `hub release create major.minor.patch`
1. Make sure the gem is actually uploaded to rubygems. It's rare but I've seen times when it doesn't upload for whatever reason.
1. travis will only deploy if the build is passing so make sure master is building before cutting a release.


### Additional Info

[Tom Servo](../tools/tom_servo.md)
[18]: https://travis-ci.org/
