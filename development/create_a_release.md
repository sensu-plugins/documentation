## How to create a github release and/or new gem release
**The github release and the gem release must point to the same commit**

All tests need to pass in Travis before any of the following steps should be taken.

### Testing

1. Pull the repo locally and build the gem `gem build <gemspec>` and make sure it builds without errors.
1. Exit out of the vagrant box and cleanup `vagrant destroy --force`

### Create A Release

1. Update the CHANGELOG and the version in lib/<repo>
1. Commit/push this to github **This must be a single commit**
1. Create a github release
    * the title is not necessary
    * the body of the message should include a summary of the change log with links back to pr's or issues if needed
    * prerelease should be used if this is an alpha/beta/rc release
1. Create a gem with the new version  (Travis will do this for you upon a tag commit at some point)
1. Push the gem to rubygems  (Travis will do this for you upon a tag commit at some point)

### Notes

Try to avoid merge commits when possible, you should always be rebasing `git pull --rebase` or however your workflow and tools reccomend you do this.

In order to build gems you will need the signing keys and in order to push to Rubygems you will need to account creds 
