tripleo-patch-puppet-modules
============================

[![Build Status](https://travis-ci.org/sathlan/tripleo-patch-puppet-modules.svg)](https://travis-ci.org/sathlan/tripleo-patch-puppet-modules)

Patch puppet modules in tripleo deployment on the overcloud.

Usage
-----

usage: tripleo-patch-puppet-modules -r PUPPET-MODULE-SHORT-NAME:REVIEW_ID[_REVIEW_ID_...][,PUPPET-MODULE-SHORT-NAME:REVIEW_ID[_...],...]
                     -s SOURCE: source can be any of:
                         - "filesystem" : copy from filesystem
                         - "rpm": from a rpm
                         - git: clone the repo
       tripleo-patch-puppet-modules -v  : display version

For instance:

./tripleo-patch-puppet-modules -r tripleo:818072_828018,nova:820032 -s git

This will create:

    ~/puppet-modules/tripleo and puppet-modules/nova

directories, using the git master branch.  It will get the tripleo
818072 and 828018 reviews for gerrit.openstack.org and apply them.

It's then trivial to distribute the patched puppet modules to the
overcloud using:

    upload-puppet-modules -d ~/puppet-modules --environment ${HOME}/patch.yaml

You just have to add the ~/patch.yaml environment file to your heat
deployment as `-e ~/patch.yaml`.

`upload-puppet-modules` is part of the `openstack-tripleo-common`
package and should be available on all undercloud.

You can use other sources for your puppet module:
* copy: will copy the existing module on the local installation;
* rpm: will get the rpm;

Installation
------------

    aclocal
    automake --add-missing
    autoreconf
    ./configure
    make
    make check
    make install

Requirements
------------

Compatibility
-------------

License
-------

Authors
-------

tripleo-patch-puppet-modules was written by [Sofer Athlan-Guyot](chem@sathlan.org).
