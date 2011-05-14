###############
Setting actions
###############
	  
setting.load
============

TODO

..
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
		  
setting.save
============

Save settings as defined in config.

Parameter
---------

* *Array*
	- *Struct*
		* *String* *nameOfSetting*
		* *String* *valueOfSetting*

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
	  - Can't save settings.
		  