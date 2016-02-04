---
layout: page
# permalink:
title: Build And Release Pipeline
doc_cat:
  - Development
---

Currently we use [Codeship](https://codeship.com/) for testing and [Travis](https://travis-ci.org/) is used to run tests across all forks and deploying the gems.

When a Pull Request is submitted, Travis will automatically execute all default tasks defined in the `Rakefile` found in the repo root and display the results in the PR.  When a committer wishes to deploy a new release the following procedure should be followed:

1. ensure all tests pass (the deploy won't happen if this fails)
1. ensure the CHANGELOG.md is updated by the end user following the conventions laid out in [Keep A Changelog](http://keepachangelog.com/)
1. ensure the version was bumpped in *../lib/plugin/version.rb* by the user
1. create a release in the gh gui or create a tag and push it. The tag should be the same as the new version. 

All tag commits that pass tests in **all** supported runtimes will kick a deploy to Rubygems.
