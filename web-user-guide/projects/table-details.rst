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

Allow edition of the view's data dictionary, i.e. the edition of the derived variables algorithms. Automatically grants the **View dictionary and summaries Permission**. This permission does not grant access to individual-level data.

Edit dictionary and view values Permission
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Applies only to tables that are views.

Allow edition of the view's data dictionary, i.e. the edition of the derived variables algorithms. Automatically grants the **View dictionary and summaries Permission**. This permission does not grant access to individual-level data.

Administrate Permission
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Allow all operations on the table/view (including removing it).

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

This operation deletes the data and the data dictionary associated with the table. This cannot be undone.

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

Edit View
~~~~~~~~~

**View over Tables**

When the view is based on other tables, you can edit the view properties, i.e. its name and the table references: these tables can be ordered and can be flagged as being *inner*. An *inner* table means that the entities of this table do not contribute to the entities of the view (similar to a SQL inner join). A typical use case is when data collected by the study are joined with data from a governmental database: if one would like to restrict the participants of the resulting view to the ones that of the study, the governmental table would be joined to the view as an *inner* table.

**View over Resource**

When the view is based on a resource (see :ref:`resource_view` in Resource documentation), you can edit the views properties: table name, ID column name, resource reference etc. Depending on the type of operation, the connection with the underlying resource could be reestablished.

Remove View
~~~~~~~~~~~

This operation will only remove the logical description of the view. It will not affect the referred data.

Entity Filter
~~~~~~~~~~~~~

A script can be defined to restrict the view entities to the ones matching some criteria (for instance, all women older than 50 years). This scrip tmust return a logical value: *true*, the entity is kept, *false* (or *null*), it is excluded.

Variable Search
~~~~~~~~~~~~~~~

Variables can be searched. Selecting the suggested name goes to the corresponding variable details.

Variable List Filtering
~~~~~~~~~~~~~~~~~~~~~~~

The list of the variables can be filtered the same way the variables can be searched. On `ENTER` key pressed, the list is refred with all variables matching the criteria.
