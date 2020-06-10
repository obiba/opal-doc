Variable
========

A variable describes the data.

Operations
----------

Add variable to View
~~~~~~~~~~~~~~~~~~~~

This operation adds or updates a derived variable in a view for each selected variable.

Categorize this variable to another
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This operation adds or overwrites a variable in a view and allows to recode its values.

Categorize another variable to this
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This operation maps another variable's values to the current variable categories.

Custom derivation
~~~~~~~~~~~~~~~~~

Derive a variable by editing its derivation script manually.

Remove
~~~~~~

Removes the variable from the table.

Properties
----------

This section displays the proerties of the variable:

* Name
* Entity Type
* Value Type
* Repeatable
* Unit
* Referenced Entity Type
* Mime Type
* Occurence Group
* Index

Categories
----------

Some variables can have categories defined. The list of categories is displayed with a summary information:

* label (mapped `label` category attribute if this one is defined)
* missing (if the category indeicates a missing answer)

Edit Categories
~~~~~~~~~~~~~~~

This operation allows the addition, edition abd deletion of a variable's categories. Categories can also be removed or reordered by selecting one or multiple categories.

Attributes
----------

Some variables can have attributes defined. The list of attributes is displayed with full information:

* namespace
* language
* value

Add Attributes
~~~~~~~~~~~~~~

Thois operation addds a new attribute. The combination of namespace and name must be unique.

Edit
~~~~

To assign the attribute to another namespace, change its name or set its value. When editing multiple attributes only the namespace can be modified.

Remove
~~~~~~

Remove the attributes.

Summary
-------

Statistical summary of the variable:

* variables with categories:

  - frequency plot

* variables without categories:

  - histogram
  - normal probability plot
  - summary data: N, Min, Max, Mean, Median, etc
  - frequencies of missiong and non-missing values

Script
------

Derived variables (i.e  when the table is a view) are persisted in Opal's embedded Version Control System which tracks all changes to a script over time. One practical use case is revising the history of changes and if necessary revert the script to a previous revision.

Script History Revisions
~~~~~~~~~~~~~~~~~~~~~~~~

Each time a script is edited a new history revision is created or 'committed' to Opal's version control system.

Commit Differences
~~~~~~~~~~~~~~~~~~

Commit revisions are organized in a descending order, i.e., the latest commit at the top of the history stack. A simple 'diff' compares the  changes between two immediate commits. Opal also offers a comparison between any revisions to the current revision.

Reverting Changes
~~~~~~~~~~~~~~~~~

By editing and saving an older revision, a script  content is reverted to its previous version. This operation is tracked as a new revision.

Review Commit Differences
~~~~~~~~~~~~~~~~~~~~~~~~~

The commit differences are ordered by the oldest changes first (denoted in red) followed by the latest changes (denoted in green).

Values
------

Values can be displayed for a specific identifier or can be filtered to match to certain criteria.

Permissions
-----------

Specify the access rights to a particular variable and its content

View with summary Permission
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Allow the user to see the variable details with its data summary. Does not allow values querying. It induces the read-only access to the parent table and datasource.
