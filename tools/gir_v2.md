## Sensu-Plugins Development Environment

### Components

* Chef
* Vagrant
* GIR

#### Chef

Chef is a configuration management and automation tool that can be used to provision various types of environments.  In this case we will be using chef-zero as the provisioner for Vagrant and Berkshelf to manage all necessary cookbooks.

#### Vagrant

Vagrant is a tool used to build development environments.  For our purposes we will be using it to create a development and manual testing environment for each plugin repo.  For example, if a user wants to develop a new Apache plugin or test an existing plugin with CentOS-7x, they would  clone *GIR* and the *sensu-plugins-apache* repos and install the necessary prerequisites.  Then  execute `vagrant up cent7` within the plugin directory.

This should provide the user with a functioning environment with which to test.  Any application specific cookbooks can be pulled at runtime from the Chef Supermarket using Berkshelf.  Any dependency's will be handled from a Berksfile within GIR, thus allowing the repos to only care about their particular environment.

The public cookbooks are a great starting place but where necessary they may need to be augmented to be truly useful.  This can be dealt with on a case by case basis.

#### Gir

Gir is a chef repo and contains the base Berksfile from which the other repo's pull,  a set of roles, and several cookbooks.  These roles are used to configure a base development environment for any supported OS.

### What you get

**every OS**

* git
* nano
* vim

**CentOS and Ubuntu**

* ruby 2.1.4 (embedded Chef)
* ruby_gems
* pry (gem)
* sensu-plugin (gem)

**Freebsd**

Currently freebsd uses the system ruby and the additional gems are not installed, although it is provisioned by Chef so you can use the embedded Ruby(2.1.4) if you wish.  It is trivial to do this by hand, not so to do it with Chef at this time.  It will be coming shortly though as time allows.  The ideal method would be to use the ark and chruby cookbooks but neither support freebsd at this time so some hacking will be required.

### Requirements

* [ChefDk](https://downloads.chef.io/chef-dk/)
* [vagrant-berkshelf](https://github.com/berkshelf/vagrant-berkshelf)
* [vagrant-omnibus](https://github.com/chef/vagrant-omnibus)

**Note** We are aware that vagrant-berkshelf is no longer supported and will most likely not work past Berkshelf 3.x.  At some point we will look at using kitchen but for now this works just fine and the converge times are much shorter.

### Installation

* install [ChefDk](https://downloads.chef.io/chef-dk/)
* install [vagrant-berkshelf](https://github.com/berkshelf/vagrant-berkshelf) plugin
* install [vagrant-omnibus](https://github.com/chef/vagrant-omnibus) plugin
* clone [GIR](https://github.com/sensu-plugins/GIR/) to ../sensu-plugins, this will be your **PROJECT_ROOT**

### Usage

#### Using a development machine

Currently supported OS's are:

* Cent[5,6,7]
 
* FreeBSD[9,10]

* Ubuntu[12,14]

1. Clone a sensu-plugins repo to your **PROJECT_ROOT**
1. execute `vagrant up OS` from within the plugin directory

#### Adding a role to GIR

The easiest way to add a role is to copy an existing one and change the name, description, and runlist.  Details on the file layout can be found in the [Chef docs](http://docs.chef.io/roles.html)  After this is done you either need to add it to *config/vagrant_config.json* or to to the Vagrantfile in the specific repo with 'chef.add_role ROLE`.

Make sure to add any cookbooks to either the local Berksfile or the Berksfile in GIR.

#### Adding a cookbook to a Vagrantfile

You can either add it to an existing role, create a new role, or add it to a Vagrantfile as a standalone entity. To add it to an existing role or create a new row see above, to add it to a Vagrantfile use `chef.add_recipe COOKBOOK`.

Make sure to add it to either the local Berksfile or the Berksfile in GIR.

#### Adding a new OS

For now this is an ass pain, it will be much easier shortly.

### Notes

All boxes are built by chef using bento to be as small as possible.  The omnibus plugin is used to install the chef-client on them for provisioning.

The BSD boxes have no support for using shared folders so they are setup to use rsync.  It is possible to use NFS but you run ithe risk of filenames being too long.  It is FAR easier to just use rsync and be done with it, not ideal but easier.

If at all possible no configuration information should be added to the local Vagrantfile.  At some point that will be dropped in a chef run.  All configuration information for a box should be added to the *vagrant_config.json* file in GIR.
