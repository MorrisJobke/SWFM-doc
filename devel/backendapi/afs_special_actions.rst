###########
AFS actions
###########

quota.get
=========

Receives quota for a given path.

Parameter
---------

*String* - path

Return Values
-------------

* Struct
	- *String* total - total quota
	- *String* used - used quota
	- *String* percent_used - percentage used/total ("1%" - "100%")
	- *String* percent_partition

Example::

	{
	  'total': '6000000',
	  'used': '2404858',
	  'percent_used': '40%',
	  'percent_partition': '34%'
	}

Errors
------

.. list-table::
	:header-rows: 1

	* - Code
	  - Description
	* - -1
	  - Dir doesn't exists.
	* - -2
	  - Permission denied.

acl.get
=======

Receives ACL for a given path.

Parameter
---------

*String* - path

Return Values
-------------

* *Array*
	* *Struct*
		* *String* username OR groupname - rights ('rlidwka)

Example::

	{
	  'test:mygroup': 'l',
	  'www:www-user': 'rl',
	  'test': 'rlidwka'
	}
	
Errors
------

.. list-table::
	:header-rows: 1

	* - Code
	  - Description
	* - -1
	  - Dir doesn't exists.
	* - -2
	  - Permission denied.

acl.set
=======

Set ACL for a given path.

Parameter
---------

* *Struct*
	- *String* path
	- (associative) *Array* acl - array of user-/groupname - rights-string (rlidwka) pairs
		* key - user-/groupname
		* value - rights ("rlidwka")
	- *Boolean* subdirs - set to true to apply recursively

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
	  - Dir doesn't exists.
	* - -2
	  - Permission denied.
	* - -3
	  - Incorrect rights.
	* - -4
	  - Incorrect user or group name.
	* - -5
	  - New group couldn't be created.
	* - -6
	  - Rights couldn't be set.

groups.get
==========

Receives all AFS groups the user owns.

Parameter
---------

None

Return Values
-------------

* *Array* - group names

Example::

	[
	  "test:group1",
	  "test:group2",
	  "test:group3"
	]

Errors
------

None

groups.create
=============

Create an AFS group.

Parameter
---------

* *String* - name of group (the inputs "testgroup" and "test:testgroup" results in "test:testgroup" for logged in user "test")

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
	  - New group couldn't be created, because you aren't own it.
	* - -2
	  - Group already exists.
	* - -3
	  - New group couldn't be created.

groups.delete
=============

Delete an AFS group.

Parameter
---------

* *String* - name of group (i.e. "test:testgroup")

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
	  - Group couldn't be deleted, because you aren't own it.
	* - -2
	  - Group doesn't exists.
	* - -3
	  - Group couldn't be deleted.

groups.members.get
==================

Retrieves members of an AFS group.

Parameter
---------

* *String* - name of group (i.e. "test:testgroup")

Return Values
-------------

* *Array* - group members

Example::

	[
	  "test1",
	  "test2",
	  "test3"
	]
	
Errors
------

.. list-table::
	:header-rows: 1

	* - Code
	  - Description
	* - -1
	  - Members couldn't be determined.

groups.members.add
==================

Adds an user to an AFS group.

Parameter
---------

* *Struct*
	- *String* group
	- *String* user

Example::

	{
	  'group': 'test:testgroup',
	  'user': 'testuser1'
	}
	

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
	  - Group doesn't exists.
	* - -2
	  - You aren't own this group.	
	* - -3
	  - User couldn't be added.

groups.members.delete
=====================

Deletes AFS group memberships for single users or the whole group inclusive the group.

Parameter
---------

* *Array* of *String* - groupnames and groupname/username pairs

Example::

	[
	  'test:group', # deletes whole group
	  'test:group2/user1' # removes only user membership
	]
	
Return Values
-------------

* *Array*
	- *Boolean* fail - true if error occured
	- *Array* result - list of all operations and their result

Example::

	{
	  'fail': true, # error occured
	  'result':
	   {
	     'test:testgroup1':true, # no error
	     'test:testgroup2/user2':true, # no error
	     'test:tesgroup3':false # error
	   }
	}
