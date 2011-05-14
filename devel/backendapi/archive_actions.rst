###############
Archive actions
###############

This is the Archive-Plugin. It provides operations to create, read and extract archives of following types:

* zip (.zip, tar.gz, tgz)
* bz2 (.tbz, tbz2, tar.bz2)

archive.create
==============

Create an archive.

Parameter
---------

* *Struct*
	- *String* path
	- *String* archiveName
	- *String* archiveType
	- *Boolean* fullPath
	- *Array* files
		* *String*
		
Return Values
-------------

* *Boolean*

Errors
------

.. list-table::
	:header-rows: 1

	* - Code
	  - Description
	* - -1
	  - Wrong directory name.
	* - -2
	  - A file with the given name already exists.
	* - -3
	  - Wrong directory name.
	* - -4
	  - A file with the given name doesn't exists.
	* - -5
	  - Couldn't add file to archive.
	* - -6
	  - Couldn't create archive.
	* - -7
	  - Couldn't create archive.
	* - -8
	  - Wrong archive type.
	* - -9
	  - Permission denied.
	* - -10
	  - Couldn't create archive.

archive.extract
===============

Delete a directory.

Parameter
---------

* *Object*
	- *String* path
	- *String* archive
	- *Array* files - files in archive which should be extracted or an empty array for all files
		* *String*

Return Values
-------------

* *Boolean*

Errors
------

.. list-table::
	:header-rows: 1

	* - Code
	  - Description
	* - -1
	  - Wrong directory name.
	* - -2
	  - Wrong archive path.
	* - -3
	  - A file with the given name already exists.
	* - -4
	  - Couldn't open and extract archive.
	* - -5
	  - Couldn't extract archive.
	* - -6
	  - Couldn't extract archive.
	* - -7
	  - Couldn't open archive.
	* - -8
	  - Unreadable archive type.
	* - -9
	  - Permission denied.
	  
archive.list
============

List all subfolders

Parameter
---------

* *String* - path

Return Values
-------------

* *Array* - treeStruct

Example::

	{
	  'folder1': {
	    'folder11':{
	      'file111': false
	    },
	    'file12: false
	  },
	  'folder2':  {
	    'file9': false  
	  },
	  'file3': false,
	  'file4': false,
	  'file5': false,
	  'file6': false
	}

Errors
------

.. list-table::
	:header-rows: 1

	* - Code
	  - Description
	* - -1
	  - Wrong directory name.
	* - -2
	  - A file with the given name already exists.
	* - -3
	  - Couldn't open archive.
	* - -8
	  - Unreadable archive type.
	* - -9
	  - Permission denied.

