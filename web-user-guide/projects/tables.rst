.. _tables:

Project Tables
==============

Tables give access to the project data along with their description. A table can be a raw table (i.e. with data persisted in the project's database) or a logical table (also called view) which is a set of derived variables (data are computed on-demand).

See also details about how to manage tables and variables individually:

.. toctree::
   :maxdepth: 1

   table-details
   variable-details

SQL
---

SQL queries can be executed on one or more tables (or views) of a project. Permission to access the values of the considered tables is required.

The supported SQL syntax is the the one of `SQLite <https://sqlite.org/>`_. More specifically see the `SQL syntax and functions documentation <https://sqlite.org/lang.html>`_.

The result of the SQL query can be downloaded from the web interface in CSV format. For a programmatic access to the SQL API, see the :ref:`python-sql` python command and the ``opal.sql()`` function in the `opalr R package <https://cran.r-project.org/package=opalr>`_.

Note that in Opal, the identifiers is not a variable. When performing assignment of the table data into the SQL environment, the identifiers column is called ``_id`` by default.

Permissions
-----------

Specify the access rights to any table of the project and its content.

View dictionary and values of all tables Permission
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Allow the user to see the data dictionary with individual-level data of any table.

Add table Permission
~~~~~~~~~~~~~~~~~~~~

Allow the addition of a table or of a view, directly or via import or copy tasks.

Administrate Permission
~~~~~~~~~~~~~~~~~~~~~~~

Allow all operations on any table/view (including removing it).


Operations
----------

Search Variables
~~~~~~~~~~~~~~~~

Variables of the project's tables can be searched. See :ref:`searchvars`.

Download Dictionary
~~~~~~~~~~~~~~~~~~~

The whole project data dictionary can be download as an Excel file. This file is compatible with the operations of Add/Update Tables and Add View. When no tables are selected, the downloaded dictionary contains the definition of all tables. When some tables are selected, the dictionary contains only their definitions.

Backup Views
~~~~~~~~~~~~

Create an archived backup of views selection (or all views).

Import Data
~~~~~~~~~~~

When importing data, Opal relies on the concept of datasource. This allows Opal to abstract the data importation process from the source datasource to the destination datasource regardless of their underlying implementations (file, SQL database etc.).

The importation process follows several steps:

* Data format selection: file-based (CSV, Opal Archive), server-based (SQL, Limesurvey, Opal)
* Data format specific options
* Incremental options
* Identifiers mapping options
* Data dictionary update review and table to to import selection
* Data to import review
* Archiving options when dealing with a file-based datasource

Some import options can be described as follow:

.. list-table::
  :header-rows: 1

  * - Option
    - Description
  * - Incremental
    - | Opal is able to detect new or updated data, relying on entity identifier and some timestamps. By default the data import is not
      | incremental, i.e. already existing data will be overridden.
  * - Limit
    - A maximum number of data rows to be imported. Combined with the  option, this allow to import small chunks of data at a time.
  * - Identifier Mapping
    - | If an identifiers mapping is selected, each participant identifier encountered in the imported datasource is expected to be one of
      | the identifiers registered for this mapping. Depending on the identifiers mapping strategy the import could fail:

      * Each identifiers must be mapped prior importation (default): the import will fail if an imported identifier does not have corresponding system identifier for the selected mapping
      * Ignore unknown identifiers at import: only data with identifier having a corresponding system identifier in the selected mapping will be imported
      * Generate a system identifier for each unknown imported identifiers: a system identifier will be generated for each unknown imported identifier

      | If no identifiers mapping is selected, the participant identifiers are imported as-is. Unknown participant identifiers will be automatically added in Opal.

Export Data
~~~~~~~~~~~

Selected tables (or currently viewed table) can be exported. The exportation process offers several options:

* Data format selection; file-based (CSV, Opal Archive), server-based (SQL)
* Data format specific options; destination folder or export database name
* Values filter options; available when a filter has been applied on the table's values
* Identifier mapping options:

  - if an identifiers mapping is selected each entity to be exported must have a mapped identifier. Otherwise the export will fail
  - if no identifiers is selected the data are exported with system identifiers

Copy Data
~~~~~~~~~

Selected tables (or all tables) can be copied into another project or in the same project but with a different name (table renaming is available only when one table is selected for copy).

Add Table
~~~~~~~~~

Adds a table to the project. Each table must have a unique name and an entity type.

Add/Update table from Dictionary
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A table can be added or updated from a data dictionary file. This data dictionary can be an Excel file (see Excel file template) or a view XML file (this can be obtained from an existing view by selecting "Download View XML"). For importing data dictionary from another format (SPSS file for instance), an alternate solution is to follow the process of importing data with the setting of limiting to 0 data rows (3rd screen in the import data wizard).

An advanced option offers the possibility to merge the data dictionaries when doing an update (otherwise default behavior is to override the properties and attributes).

Add View
~~~~~~~~

This operation follows a step-by-step procedure:

1. Specify the view name and the data dictionary (optional). The data dictionary can be provided as an XML file (this can be obtained from an existing view by selecting "Download View XML") or an Excel file (see Excel file template). If a view with same name already exists, confirmation for overriding it is required. If a plain table already exists with same name, the operation is not allowed.
2. Specify which tables this view refers to (required).

Derived variable algorithms are expressed using Magma Javascript API.

Restore Views
~~~~~~~~~~~~~

Restore backed up views. Restored views of the same name as those of existing views will be skipped unless the override options is checked.

Remove
~~~~~~

Removes the selected tables/views from the project and deletes its data.
