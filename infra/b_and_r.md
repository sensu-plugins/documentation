## Build and Release Pipeline

Currently we use [Codeship][17] for deploying plugins in an automated fashion while [Travis][18] is used to run tests across all forks.

When a Pull Request is submitted, Travis will automatically execute all default tasks defined in the `Rakefile` found in the repo root and display the results in the PR.  When a contributor wishes to deploy a new release the following procedure should be followed:

1. ensure all tests pass (the deploy won't happen if this fails)
1. edit the CHNAGELOG.md following the conventions laid out in [Keep A Changelog](http://keepachangelog.com/)
1. bump the version in *../lib/plugin/version.rb*
1. commit ONLY those two items with a message of **deploy**

This commit must be done against Master and not via PR in order for Codeship to detect it.  At this point Codeship will run any tests and then execute the deploy script which will create a new Github tag/release with the current version and then build and publish a gem of the same version.

If a repo is not connected to Codeship, there will be no badge, it will need to be added by an admin.

### Additional Info

[Tom Servo](../tools/tom_servo.md)
[17]: https://codeship.com/
[18]: https://travis-ci.org/
