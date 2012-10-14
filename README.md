Drupal On OpenShift
===================

This stands up a fully functional Drupal installation (no need to run the
 installer).  Feel free to fork and use as a basis for your own Drupal projects.

It is designed with single site deployments in mind, changes will be needed for multi site.

It also handles redeployment to OpenShift without all the settings and files being wiped out.

Notable Features
----------------
- public and private files are kept under misc, these get copied to the correct
location at deploy time.  Please note the repo is authoritative and will overwrite
existing files if a conflict occurs.
- Zen 7.x-5.1 is included under sites/all/themes
- Cron tasks are run hourly
- Admin password randomly generated at deploy time
- drush (7.x-5.7) is available in misc/drush

Using
-----

You'll need to have a (free) Openshift account first.  So go and sign up if
you haven't already.  You'll also need git (e.g. on Ubuntu sudo apt-get install git)

Most of this guide will assume a command line on Mac/Linux, but if this is all
new to you have a read of https://openshift.redhat.com/community/get-started before
going any further.

Create a php app called drupal.

`$ rhc app create -a drupal -t php-5.3`

Add a couple of required cartridges.

`$ rhc app cartridge add -a drupal -c mysql-5.1`

`$ rhc app cartridge add -a drupal -c cron-1.4`

Add NetSrv's repo as a remote to your local repo:

`$ cd drupal`

`$ git remote add netsrv git://github.com/netsrv/openshift-drupal.git`

Pull in the project

`$ git pull -X theirs -s recursive netsrv master`

Deploy to Openshift

`$ git push`

Make a note of Drupal's admin username/password as you'll need that later.

Open a browser and browse to http://drupal-[your rhc domain].rhcloud.com

FIN
