![GIR](http://www.roomwithamoose.com/pictures/official/gir_suit_stand_optimized.jpg)

GIR is how developers can get things accomplished quickly, simply, and efficiently.  At the root it's nothing more than a ton of rake tasks for doing common things.  Where it gets helpful is when the sensu-plugins org grows to 20..30...40+ repos, then these tasks become awesome time and disk space savers.  

### Initial Setup

Create a directory called sensu-plugins and clone this repo into it, this will be the **PROJECT_DIRECTORY**.  Now copy the *Rakefile* from GIR to the project directory.  You should have something like this:

```bash
sensu-plugins/
sensu-plugins/Rakefile
sensu-plugins/GIR
```
That's it.

You can see the list of available tasks using Rake -T.  Some of the tasks, primarily the Github ones, may require a Github token with Admin rights but many of the others can be executed with no or very minor configuration.  You can check the configuration settings for various things using the `:config` namespace.


### USAGE

GIR is designed as a framework for working with the sensu-plugins as a whole.  There should be no need to clone specific repos or deal with them directly.  Once you clone GIR all common tasks necessary for developing, testing, and building Sensu Plugins are available to you.  To interact with a specific repo you will use *plugin=X*, in order to launch vagrant for developing the sensu-aws-plugins you would issue the following commands from the **PROJECT_DIRECTORY**

```bash
rake vagrant:up plugin=aws             # clone the repo (if it is not already
                                       # in PROJECT_ROOT and start the included
                                       # default vagrant box

rake vagrant:ssh plugin=aws            # shh into the vagrant box

rake vagrant:halt plugin=aws           # halt the vagrant box

rake vagrant:destroy plugin=aws        # destroy the vagrant box

rake vagrant:destroy plugin=aws remove # destroy the vagrant box and remove the
                                       # copy of the local repo
```

If you are unsure of which repos are available and what each contains `rake github:list_repos` will give you the repo name, plugin, and description of all repos in the sensu-plugins organization.

This will allow a developer to not worry about managing the various repos or even what ones exist, they can just work with a single repo or many and when done, remove them from their system if they chose.

### Example Workflow

A few thoughts on a workflow that may work for some people.  Perform the initial setup as stated above, and decide you would like to work on disk checks.  If you are unsure where the disk checks are located or what the plugin name is then execute `rake github:list_repos`  in the output will be:

```bash
Name                        Plugin          Description
sensu-plugins-disk-checks   disk-checks     Sensu disk and filesystem checks
```

You can either run `rake git:clone plugin=disk-checks` to clone the repo for your own workflow or you could run

```bash
rake vagrant:up plugin=disk-checks
rake vagrant:ssh plugin=disk-checks
```

to launch the vagrant box and ssh into the machine for development and testing.  When you are done you have several choices depending on your mood.

```bash
rake vagrant:halt plugin=disk-checks # halt the machine, preserving its state
rake vagrant:destroy plugin=disk-checks #halt and remove the machine, preserving the repo
rake vagrant:destroy remove plugin=disk-checks # halt and remove the machine and the repo
```

Of note is the final task, it will leave your machine as it was, with no trace of the work you have been doing.  It may be useful if you work on a lot of repos and commit or PR often and don't want to store the local code on your disk.

This is just a small sample, there are tasks for bootstrapping a repo from scratch both locally and on Github.  This may be useful if you want to add or develop a new plugin that has no home or doesen't fit in anywhere yet.  In this case use 'rake gem:boilerplate plugin=my_new_plugin'.

This will create a local directory called sensu-plugins-my-new-plugin and populate it with a stock gemspec, readme, spec_helper, etc.  When you are ready to add it to the sensu-plugins org submit a pull request for the entire repo against the community repository.  If all goes well and tests, linters, docs, etc pass then it will be broken out and made it's own repo or you may be asked to refactor it into an existing repo.

There are many more uses and tasks which may be added to GIR, if you have one then submit a PR, the easier it is to work on the project, the more people will contribute to it.
