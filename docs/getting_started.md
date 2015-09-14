---
layout: documentation
# permalink:
title: Getting Started
doc_cat:
  - Development
tags:
  - no_menu
---

**Table of Contents**

- [Infrastructure](#Infrastructure)
    - [Github](#github)
    - [Trello](#trello)
    - [Website](#website)
- [Policies](#policies)
    - [Organization Access](#organization-access)
    - [Organization Structure](#organization-structure)

## Sensu-Plugin Org Guidelines

### Infrastructure

#### Github

Github and the issues and milestones within it are the primary way the project is managed.  All plugin repositories are created from a standard template using a rake task to ensure that they remain consistent and manageable at an organization level.  There are currently five teams in the org:

* Owners - unrestricted access to the org and all repos
* Admins - write access to all repos except core infrastructure
* Contributors - write access to all plugin repos
* Core Infra - write access to sensu-plugin, sensu-plugin-spec, GIR, Kryten, sensu-plugin.github.io, tom_servo, and the hubots
* Documentation - write access to the documentation repo

**Note**

Members in the Owners or Core Infra team must provide a voie number.  Due to the permissions and far reaching affect of these teams security  practices are heavily enforced and any compromises must be dealt with immediately.

#### Trello

There is a public Trello [board](https://trello.com/b/QjkJ8CS3/sensu-community-plugins) used for communicating various project wide items.  This is still a work in progress but it works for now.  Ideas are always welcome.

#### Website

[sensu-plugins.io](http://sensu-plugins.io/)


### Policies

This is a volunteer project and as such contributors are free to come and go.  No one is required to do any amount of work to continue as a contributor, some days you may do a ton of work or you may be on vacation or doing something that pays the bills for a few weeks.  No worries.

#### Organization Access

This is a public organization and as such anyone may join the only requirements are a firm belief in treating your infrastructure as code and 2FA on your github account.

#### Organization Structure

Becoming a member of each of these groups and teams is a community decision.  You may be invited by any member of the team and the majority of the other team members can approve.  There is no time limit before being invited into a team and no set amount of work that needs to be accomplished once you are in a team.

For security purposes though if you have not made any contributions in the last 6 months, you may be removed from a team and can request access again at any time.

Any membership issues will be resolved by members of the GitHub Owners group after consultation withh all parties and are final.

**core committer**

A committer who has read access to all public and private repos including these specific privilages:
* Can modify the build pipeline
* Can push directly to Github and RubyGems
* Access to the sensu-plugin bot account
* Access to the slack channel
* Accees to the Google Apps Account

Any member of this group must also provide a voice number that they can be reached at.  Due to the widespread permissions, security practices are heavily enforced and any compromises must be dealt with immediately.

**committer**

A commiter who has push access to any repos. They can either be a member of a team or be granted rights to specific repos using Github's new org permissions.

**contributor**

A Github user who has had one or more merges commited to any repo but does not yet have push access to a team.


