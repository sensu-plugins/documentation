The goal of the Sensu Plugins This project contains example plugins, handlers and other use code to maximize the effective use of Sensu in various types of auto-scaling and traditional environments. Most of them are implemented in Ruby and use the sensu-plugin framework; some also depend on additional gems or packages(e.g. mysql). Some are shell scripts! All languages are welcome.

In the future, some sort of browsing/metadata/installation system will be implemented. For now, just clone the various repositories, take a look around, and copy the plugins you want to use.

Production usage
Linters currently run against Ruby 2.0 and 2.1 and tests are being run against 1.9.3, 2.0, and 2.1 if they are written. There are no plans to support prior versions of Ruby, if you have no access to these versions please use the embedded Ruby that is installed with Sensu, directions on this can be found in the Sensu FAQ or below.

Gems will be built against all current versions of Ruby and one EOL Ruby, currently 1.9.3, will be actively supported.
Because of the nature of these repositories:

little test coverage
specific and exotic software being checked
no versioning system for plugins
at this time is not recommended that you use master for your production instances. Better pick something which works for you and lock it via :ref in your cookbook, manifest, or bash script.

If you have installed Sensu using the omnibus package it will use an embedded version of ruby, but the ruby plugins here will use the system one. If you want to use the embedded ruby, which has the sensu-plugin gem installed as well, you can set EMBEDDED_RUBY=true in /etc/default/sensu and restart the Sensu services. This will put the embedded ruby first in the $PATH for commands run by the Sensu services.