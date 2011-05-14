##############
Search actions
##############

This is the Search-Plugin. It provides an method to search via find command.

search
======

Searches for a given term in a specific path.

Parameter
---------

* *Struct*
	- *String* path - the path within should searched
	- *Struct* options
		* *String* name - search term

Return Values
-------------

* *Array*
	- *Array*
		* *String* - Name of file or folder
		* *String* - location of file or folder (relative to basepath and without leading /)
		* *Bool* - true if it's a folder

Example::

	[
	  [
	   'text',
	   'test-folder/'
	   true
	  ],
	  [
	   'text.txt',
	   'test-folder/tmp/'
	   false
	  ]
	]
	

Errors
------

.. list-table::
	:header-rows: 1

	* - Code
	  - Description
	* - -1
	  - Wrong path.
	* - -2
	  - File or directory doesn\'t exists.
	* - -7
	  - Unknown Error.
	* - -8
	  - Permission denied.
	* - -9
	  - Permission denied.