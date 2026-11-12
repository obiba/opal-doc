.. _table:

Table
=====

A table can be a raw table or a view

Dictionary
----------

List of the variables in the table with summary information for each of them:

* label (mapped on label variable if this one is defined)
* value type
* unit

Summary
-------

The data of the table can be indexed in Opal's internal search engine. Indexing the values allows:

* to have pre-computed variable summaries
* to filter the table-entities by their values (and subsequently copy/export a subset of the data)

Used by Views
-------------

The views that refer to the table (or to the view) are listed, whatever their project. The views that the user is not allowed to see are not named, only counted. While a view refers to it, a table or a view cannot be renamed or removed: the views must be removed first, or removed together with the table (see the **Remove** operation of the :ref:`tables`).

Values
------

The values of the table can be seen in this section. the view port of the values is limited by a number of rows and a number of visible variables (display options allow to modify these numbers). Right abnd left arrows in table header (with variable names) allows to move the variables view port.

When the table has been indexed (see Summary section) the rows can be filtered by varialbe criteria. the resulting subset of data can be exported/copied using the usual Export/Copy procedure.

Permissions
-----------

Specify the access rights to a particular table and its content.

View dictionary and summaries Permission
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Allow the user to see data dictionary with variable data summaries. Does not allow values querying. It induces the read-only access to the parent datasource.

View dictionary and values Permission
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Allow the user to see the table's data: values querying services are available. Automatically grants the View dictionary and summaries Permission.

Edit dictionary and view summaries Permission
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Applies only to plain tables (i.e. not views).

Allow edition of the table's data dictionary. Automatically grants the **View dictionary and summaries Permission**.

Edit dictionary and view summaries Permission
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Applies only to tables that are views.

Allow edition of the view's data dictionary: labels, descriptions, categories, attributes, etc. Automatically grants the **View dictionary and summaries Permission**. This permission does not grant access to individual-level data.

Changing how the view computes its values is subject to the permissions on its sources, see :ref:`view_derivation_permissions`.

Edit dictionary and view values Permission
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Applies only to tables that are views.

Allow edition of the view's data dictionary, as above, and access to the view's individual-level data. Automatically grants the **View dictionary and values Permission**.

Changing how the view computes its values is subject to the permissions on its sources, see :ref:`view_derivation_permissions`.

Administrate Permission
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Allow all operations on the table/view (including removing it).

.. _view_derivation_permissions:

Permissions on the Sources of a View
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Whatever the permission on the view, an operation that changes how the view computes its values requires to be allowed to see the values of all its sources:

* for a view over tables, the **View dictionary and values Permission** (or higher) on each of the referred tables,
* for a view over a resource, the **Administrate Permission** on the resource,
* in both cases, the **View dictionary and values Permission** (or higher) on every other table that the scripts of the view read (derivation scripts, *sameAs*, entity filter), once the change is applied.

Scripts that compute the name of the table they read cannot be checked: such changes are reserved to system administrators. System administrators are not subject to these checks.

The operations concerned are:

* editing the script of a derived variable, or adding a derived variable with a script (including the **Add Variables to View** operation),
* changing, adding or removing the referred tables, or changing the resource settings of the view (ID column, profile, all columns etc.),
* editing or removing the entity filter,
* adding variables to a view over a resource, or changing the column a variable is read from, or renaming such a variable,
* renaming a derived variable to the name of another variable of the view (which replaces it),
* adding or updating variables from a view XML or Excel file,
* restoring a script revision, an entity filter revision or a tag of the view (see :ref:`view_versions`),
* creating a view with derived variable scripts or an entity filter.

Other dictionary edits (labels, descriptions, categories, attributes, etc.) do not need these permissions. When a source is not accessible, the corresponding edit and restore actions are not proposed, and the table references of the view that cannot be accessed are not shown as links.

.. _view_versions:

Versions
--------

Only available if the table is a view and the user can edit it.

History
~~~~~~~

The history lists all the changes of the view, the latest first: the view itself, its entity filter and its variable scripts. Each change can be compared with the previous version or with the current one. The tags of a change are shown next to it.

Tags
~~~~

A tag is a name, with an optional message, given to the latest version of the view, for instance to mark the version used for a publication. The tags are listed most recent first. The name of a tag must be unique in the view and must not contain spaces or any of these characters: ``~ ^ : ? * [ \``.

Each tag can be:

* downloaded: the view definition at that version is saved as an XML file named after the view and the tag, in the same format as the **Download View XML** operation.
* restored: the dictionary, the variable scripts and the entity filter of the view are replaced by the tagged version. This is recorded as a new change, so the current version stays in the history.

A view cannot be restored if one of its source tables or its resource does not exist anymore. Restoring a tag that changes how the view computes its values requires to be allowed to see the values of its sources (see :ref:`view_derivation_permissions`). A user who can see the values of the view must also be allowed to see the values of the tables or the resource that the tagged version refers to.

A new view can also be created from a tag: the view definition at that version is copied into a view with a new name (default is the view name followed by the tag name), in the same project or in another one. If a view with this name already exists, a confirmation is asked before overriding it; the override is recorded as a new change of that view.

The tags are deleted when the view is renamed or removed.

Operations
----------

Reconnect Resource
~~~~~~~~~~~~~~~~~~

When the table is a view over a resource (see :ref:`resource_view` in Resource documentation), it is possible to reset the connection with the underlying resource. This can be convenient when the connection is lost (because resource lives in a remote server for instance) or has failed unexpectedly.

Add Variables to View
~~~~~~~~~~~~~~~~~~~~~

This operation consist of making a derived variable for each of the selected variables (see ) and adding them to a view (either an existing one or one that would be created for that purpose). Options are:

* derived variable name can be changed (default is the original variable name)
* categorical variables can be recoded (i.e. category names are turned to a numerical value)

If a derived variable with the same name already exists in the destination view, this derived variable will be overwritten with the new definition. Else a new derived variable is added.

Export Variable Dictionary
~~~~~~~~~~~~~~~~~~~~~~~~~~

The table/view data dictionary can be download as an Excel file. This file is compatible with the operations of Add/Update and Add View.

Export Data
~~~~~~~~~~~

Start Export Data procedure with the table preselected.

Copy Data
~~~~~~~~~

The table can be copied into another project or in the same project but with a different name.

Remove Table
~~~~~~~~~~~~

This operation deletes the data and the data dictionary associated with the table. This cannot be undone. It is refused when the table is used by a view (see the **Used by Views** section).

Variable Selection
~~~~~~~~~~~~~~~~~~

Variable can be selected to perform batch operations:

* Add variable to view: make an identity derived variable, added to a view
* Apply attribute: apply a custom attribute or a taxonomy term
* Remove attributes: remove variable attributes by specifying namespace (optional) and name, or taxonomy and vocabulary
* Remove: variable and associated data will be removed

View specific Operations
------------------------

Download View XML
~~~~~~~~~~~~~~~~~

Only available if the table is a view.

Copy View
~~~~~~~~~

The view definition (not the data) is copied into a new view, in the same project or in another one. If a view with the same name already exists in the destination project, a confirmation is asked before overriding it; the override is recorded as a new change of that view.

Edit View
~~~~~~~~~

**View over Tables**

When the view is based on other tables, you can edit the view properties, i.e. its name and the table references: these tables can be ordered and can be flagged as being *inner*. An *inner* table means that the entities of this table do not contribute to the entities of the view (similar to a SQL inner join). A typical use case is when data collected by the study are joined with data from a governmental database: if one would like to restrict the participants of the resulting view to the ones that of the study, the governmental table would be joined to the view as an *inner* table.

**View over Resource**

When the view is based on a resource (see :ref:`resource_view` in Resource documentation), you can edit the views properties: table name, ID column name, resource reference etc. Depending on the type of operation, the connection with the underlying resource could be reestablished.

The name of a view cannot be changed while another view refers to it (see the **Used by Views** section).

.. warning::

  Renaming a view restarts its history of changes: the earlier versions, including the history of its variables, are no longer listed and all its tags are deleted (see :ref:`view_versions`).

Remove View
~~~~~~~~~~~

This operation will only remove the logical description of the view and its tags (see :ref:`view_versions`). It will not affect the referred data.

Entity Filter
~~~~~~~~~~~~~

A script can be defined to restrict the view entities to the ones matching some criteria (for instance, all women older than 50 years). This scrip tmust return a logical value: *true*, the entity is kept, *false* (or *null*), it is excluded.

The changes of this script are listed in the **History** section of the Entity filter panel, which is shown to the users who can edit the view, once the view has had an entity filter. Each revision can be compared with the previous one or with the current one, and an older revision can be restored. This operation is tracked as a new revision.

Editing, removing or restoring the entity filter requires to be allowed to see the values of the sources of the view (see :ref:`view_derivation_permissions`).

Variable Search
~~~~~~~~~~~~~~~

Variables can be searched. Selecting the suggested name goes to the corresponding variable details.

Variable List Filtering
~~~~~~~~~~~~~~~~~~~~~~~

The list of the variables can be filtered the same way the variables can be searched. On `ENTER` key pressed, the list is refred with all variables matching the criteria.
