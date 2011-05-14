############
Base actions
############

This is the Base-Plugin. It supports operations on standard filesystems and the AFS filesystem.

dir.create
==========

Create a directory.

Parameter
---------

* *Struct*
	- *String* path
	- *String* name

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
	  - A directory with the given name already exists.
	* - -2
	  - Can't create the folder.
	* - -3
	  - Can't create folder recursively.
	* - -4
	  - Wrong directory name.
	* - -9
	  - Permission denied.


dir.delete
==========

Delete a directory.

Parameter
---------

* *Struct*
	- *String* path
	- *String* name

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
	  - Folder doesn't exists.
	* - -2
	  - The folder with the given name is not a folder.
	* - -3
	  - Can't remove the folder.
	* - -4
	  - Wrong directory name.
	* - -9
	  - Permission denied.
	  
	  
dir.list
========

List all subfolders

Parameter
---------

* *Struct*
	- *String* path
	- *Boolean* showHidden
	
Return Values
-------------

* *Array*
	- *Struct*
		* *String* name
		* *String* path
		* *Boolean* hasSubDirs

Errors
------

.. list-table::
	:header-rows: 1

	* - Code
	  - Description
	* - -1
	  - Folder doesn't exists.
	* - -2
	  - Wrong directory name.
	* - -9
	  - Permission denied.

file.copy
=========

Copy a file

Parameter
---------

* *Struct*
	- *Struct* source
		* *String* path
		* *String* name
	- *Struct* destination
		* *String* path
		* *String* name
	- *Boolean* overwrite
	
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
	  - Source file doesn't exists.
	* - -2
	  - Destination file exists.
	* - -3
	  - An error occurs.
	* - -4
	  - Source is directory.
	* - -9
	  - Permission denied.

file.delete
===========

Delete a file.

Parameter
---------

* *Struct*
	- *String* path - the path
	- *String* name - the name of the file in the path

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
	  - File doesn't exists.
	* - -2
	  - Can't delete the file.
	* - -3
	  - Wrong filename.
	* - -9
	  - Permission denied.

file.list
=========

Gets a list of files and subfolders in a folder

Parameter
---------

* *Struct*
	- *String* path - the folder path
	- *Boolean* showHidden
	
Return Values
-------------

* *Array*
	- *Struct*
		* *String* type
		* *String* name
		* *String* path
		* *Integer* size
		* *String* mime-type
		* *Boolean* isDir
		* *Integer* atime
		* *Integer* ctime
		* *Integer* mtime

Example::

	[
	  {
	   'type': 'file',
	   'name': 'File1.html',
	   'path': '/tmp',
	   'size': 10,
	   'mime-type': 'text/html',
	   'isDir': false
	  },
	  {
	   'type': 'file',
	   'name': 'Folder',
	   'path': '/tmp',
	   'size': 0,
	   'mime-type': '',
	   'isDir': true
	  },
	]
	
Errors
------

.. list-table::
	:header-rows: 1

	* - Code
	  - Description
	* - -1
	  - Dir doesn't exists.
	* - -2
	  - Wrong path.
	* - -9
	  - Permission denied.

file.move
=========

Move a file from one location to an other.

Parameter
---------

* *Struct*
	- *Struct* source
		* *String* path
		* *String* name
	- *Struct* destination
		* *String* path
		* *String* name
	- *Boolean* overwrite

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
	  - The source file doesn't exists.
	* - -2
	  - A file with the destination name exists and the overwrite flag is not set.
	* - -3
	  - An error occurs.
	* - -4
	  - Wrong filename.
	* - -9
	  - Permission denied.
	  
file.rename
===========

Rename a file or a folder

Parameter
---------

* *Struct*
	- *String* path
	- *String* name
	- *String* name_new
	- *Boolean* overwrite

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
	  - Source file doesn't exists.
	* - -2
	  - Wrong filename for source.	
	* - -3
	  - Wrong filename for destination.
	* - -4
	  - Error while renaming the file.
	* - -9
	  - Permission denied.