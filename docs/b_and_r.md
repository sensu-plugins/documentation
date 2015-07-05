---
layout: documentation
# permalink:
title: Build And Release Pipeline
doc_cat:
  - Development
tags:
  - no_menu
---

## Build and Release Pipeline

Currently we use [Codeship][1] for deploying plugins in an automated fashion while [Travis][2] is used to run tests across all forks.

When a Pull Request is submitted, Travis will automatically execute all default tasks defined in the `Rakefile` found in the repo root and display the results in the PR.  When a committer wishes to deploy a new release the following procedure should be followed:

1. ensure all tests pass (the deploy won't happen if this fails)
1. edit the CHANGELOG.md following the conventions laid out in [Keep A Changelog](http://keepachangelog.com/)
1. bump the version in *../lib/plugin/version.rb*
1. commit ONLY those two items with a message of **deploy**

This commit must be done against **Master** and not via a PR in order for Codeship to detect it.  At this point Codeship will run all tests and then execute the deploy script which will create a new Github tag/release with the current version and then build and publish a gem of the same version.

### Additional Info

[Tom Servo](https://github.com/sensu-plugins/documentation/blob/master/docs/tom_servo.md)
[1]: https://codeship.com/
[2]: https://travis-ci.org/
