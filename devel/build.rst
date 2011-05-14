#################
Build from Source
#################

How to build SmartWFM from source.

Requirements
============

* `Ant <http://ant.apache.org/>`_ >= 1.6
* `Git <http://git-scm.com/>`_

Get source
==========

Read-only::

	git clone git://swfm.git.sourceforge.net/gitroot/swfm/swfm

Build
=====

Go into the swfm source directory and type for ...

default build
-------------

This build strips all the comments and all the debug output from the source and optimizes the source.
::

	ant build

development build
-----------------

This build includes all the debug output and the source isn't optimized.
::

	ant build_dev

Build archive
=============

First get the source code for the version of SmartWFM you like to build the archive for. After that you have to build the default or the development version. Now you can run commands to build an archive.

Release
-------

The following command will create new archives in the 'dist/' directory.
::

	ant -Dswfm_version=<the version> archive_all

For example::

	ant -Dswfm_version=0.6 archive_all

Snapshot
--------

::

	ant archive_all
