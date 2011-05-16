#################
Build from Source
#################

How to build SmartWFM from source.

********
Frontend
********

Requirements
============

* `Ant <http://ant.apache.org/>`_ >= 1.6
* `Git <http://git-scm.com/>`_

Get source
==========

Read-only::

	git clone git://swfm.git.sourceforge.net/gitroot/swfm/swfm

.. note::

	For read/write access check the `develop page on Sourceforge
	<https://sourceforge.net/projects/swfm/develop>`_.

Build
=====

Go into the swfm source directory and type for ...

... default build
-----------------

This build strips all the comments and all the debug output from the source and
optimizes the source.
::

	ant build

... development build
---------------------

This build includes all the debug output and the source isn't optimized.
::

	ant build_dev

Build archive
=============

First get the source code for the version of SmartWFM you like to build the
archive for. After that you have to build the default or the development
version. Now you can run commands to build an archive.

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

.. note::

	There are also separate commands to build only a .tar.bz2, a .tar.gz or a
	.zip package. Just replace *archive_all* with one of the following:
	*archive_bz2*, *archive_gz*, *archive_zip*.

Build documentation
===================

This commands creates the API documentation directly from the source code::

	ant doc

Now there is a new **doc/api** folder, where the API documentation is located.

*************
Backend (PHP)
*************

Requirements
============

* `Git <http://git-scm.com/>`_

Get source
==========

Read-only::

	git clone git://swfm.git.sourceforge.net/gitroot/swfm/backend-php

.. note::

	For read/write access check the `develop page on Sourceforge
	<https://sourceforge.net/projects/swfm/develop>`_.

Build
=====

There isn't really any build process, because you can just copy the files
inside **src/** directly to the web server.

Build archive
=============

You are able to build to different versions of archives, on the one side
releases and on the other so called snapshots.

Release
-------

The following command will create new archives in the 'dist/' directory,
where *<the version>* have to be a valid git commit identifier (i.e. HEAD,
*tags*, *short/long commit hash*, ...)
::

	make archive ARCHIVE_VERSION=<the version>

For example::

	make archive ARCHIVE_VERSION=0.4
	make archive ARCHIVE_VERSION=ed7365344fe57f8015acdb15af542636d58aee49
	make archive ARCHIVE_VERSION=ed73653

Snapshot
--------

For a snapshot the current status of the repository is used
(ARCHIVE_VERSION=HEAD).

::

	make archive

Build documentation
===================

.. note::

	Till version 0.5 doxygen is used as documentation tool. Maybe this changes to `Sphinx <http://sphinx.pocoo.org/>`_ too.

::

		make apidoc
