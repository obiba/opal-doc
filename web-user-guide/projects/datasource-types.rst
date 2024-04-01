Datasource Types
================

Datasources are the entry point in Opal for accessing to :doc:`../../variables-data`. Datasources can be of different kinds, some being more suitable for different purposes (variables import, data import and export, permanent storage).

.. list-table::
  :header-rows: 1

  * - Datasource type
    - Variables Import
    - Variables and Data Import
    - Variables and Data Export
    - Storage
  * - CSV Datasource
    -
    - x
    - x
    -
  * - Opal Archive Datasource
    -
    - x
    - x
    -
  * - SPSS Datasource
    - x
    - x
    -
    -
  * - SPSS R Datasource
    -
    - x
    - x
    -
  * - SAS R Datasource
    -
    - x
    - x
    -
  * - Stata R Datasource
    -
    - x
    - x
    -
  * - Excel Datasource
    - x
    -
    -
    -
  * - Opal SQL Datasource (deprecated)
    -
    -
    -
    - x
  * - Tabular SQL Datasource
    -
    - x
    - x
    - x
  * - Limesurvey Datasource
    -
    - x
    -
    -
  * - Opal Datasource
    -
    - x
    -
    -
  * - MongoDB Datasource
    -
    -
    -
    - x

File Based Datasources
----------------------

File based datasources are convenient for import and export operations.

CSV Datasource
~~~~~~~~~~~~~~

CSV datasource will expect the file to use a "delimiter separated values" format (default delimiter being comma). The first column will represent the entity identifiers and the subsequent column names will identify variables. Each row of the file (except the first row) are the values for one entity. The entity identifier must be unique: there cannot be two rows starting with the same identifier.

Due to the nature of the CSV format, the data dictionary is limited to the variable names (i.e. the name of the columns). A CSV file can be imported as-is but the variables will be considered as being of text type only. When importing CSV data, if the destination table already exists, Opal will consider that the data dictionary of the CSV file is the one of the destination table. Then before importing CSV data it is recommended to prepare the destination table variables first.

Example

The following data dictionary is used in this example:

* Var1: text value type
* Var2: integer value type
* Var3: text value type, repeatable (i.e. each value is a sequence of value)

The data to be represented in CSV are for instance:


.. list-table::
  :header-rows: 1

  * - ID
    - Var1
    - Var2
    - Var3
  * - 123
    - This is a value
    - 1
    - "Value 1","Value 2"
  * - 234
    -
    - 2
    - x,y
  * - 345
    - | This is a
      | multi-line value
    -
    - a

The CSV file uses the options:

* the separator character: ,
* the quote character: "

.. code-block:: text

  ID,Var1,Var2,Var3
  123,"This is a value",1,"""Value 1"",""Value 2"""
  234,,2,"x,y"
  345,"This is a
  multi-line value",,a

For more information about CSV format:

* `Comma separated values <https://en.wikipedia.org/wiki/Comma-separated_values>`_
* `Delimiter separated values <https://en.wikipedia.org/wiki/Delimiter-separated_values>`_
* `RFC4180 <https://tools.ietf.org/html/rfc4180>`_

Opal Archive Datasource
~~~~~~~~~~~~~~~~~~~~~~~

Opal Archive datasource is a fully featured file-based datasource. This datasource comes as a .zip file (that can be optionally encrypted) containing a folder for each table having: the full data dictionary in a XML file, a XML data file per entity. This is the file format used when exporting data from Onyx.

SPSS Datasource
~~~~~~~~~~~~~~~

An SPSS datasource is a read-only datasource. The SPSS source file must be a valid non-compressed binary file with a .sav extension. In Opal an SPSS file represents a table and its variables are used as the table's data dictionary. An Opal compatible SPSS file must have its first variable represent the identifiers. If this is not the case, before a file import, the identifier variable must be moved to the first position of the SPSS variable sheet.

The following SPSS variable attributes are imported to the data dictionary:

* width
* decimals
* measure
* shortname
* format (F9.2, ADate10, etc)

In addition, variable categories and missing values are also imported and converted to their Opal counterparts

Currently, Opal does not handle missing values with large intervals (-9999..9999). Until a more robust solution is implemented, try to keep the intervals small or discrete.

Excel Datasource
~~~~~~~~~~~~~~~~

Opal supports both Excel 97 and Excel 2007 formats. Excel format limitations are:

========= =========== ===========
Extension Format used Limits
========= =========== ===========
.xls      Excel 97    256 columns and 64K lines
.xlsx     Excel 2007  16K columns and 1M lines
========= =========== ===========

R Based Datasources
~~~~~~~~~~~~~~~~~~~

R based datasources are datasources that are using R server to extract/write data in a given format. The supported formats are the ones defined in the `haven <http://haven.tidyverse.org/>`_ R package (package which is expected to be installed on the R server). Note that this is still an experimental feature: value type mappings with R could change in a future release and some limitations of the `haven <http://haven.tidyverse.org/>`_ package may apply.

SPSS R Datasource
^^^^^^^^^^^^^^^^^
The expected/produced file extension is .sav.

SAS R Datasource
^^^^^^^^^^^^^^^^
The expected/produced file extension is .sas7bdat. If when importing, a file exists with same base name in the same parent folder and with extension .sas7bcat, it will be automatically used as the catalog file.

Stata R Datasource
^^^^^^^^^^^^^^^^^^

The expected/produced file extension is .dta.

SQL Based Datasources
---------------------

SQL based datasources are convenient for variables and data storage. With some limitations, this type of datasource can be used for import and export.

Opal SQL Datasource (deprecated)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Opal SQL is the most versatile datasource type with MongoDB datasource. The underlying SQL database schema is a `EAV <https://en.wikipedia.org/wiki/Entity%E2%80%93attribute%E2%80%93value_model>`_ which allows to store an unlimited number of variables.

For more information about this datasource see :ref:`opal-sql` Schema documentation.

Tabular SQL Datasource
~~~~~~~~~~~~~~~~~~~~~~

Tabular SQL datasources are suitable for datasets with a (relatively) small number of variables. Data copied into Tabular SQL datasource are stored in classical SQL tables, i.e. one row per entity and one variable per column. Check SQL database vendor specifications to know the number of columns (i.e. variables) that can be defined for a table: see for instance `MySQL Table Column-Count and Row-Size Limits <http://dev.mysql.com/doc/refman/5.6/en/column-count-limit.html>`_. Comprehensive meta-data for each column field can be optionally stored in separated tables. Opal is able to increment copies into Tabular SQL datasources if update timestamp column is given.

For more information about this datasource see :ref:`tabular-sql` Schema documentation.

Document Oriented Datasources
-----------------------------

NoSQL document oriented datasources are convenient alternative to SQL based datasources. It allows to store an unlimited number of variables.

MongoDB Datasource
~~~~~~~~~~~~~~~~~~

MongoDB is the most versatile datasource type and is the recommended one for replacing deprecated Opal SQL datasources.

Other Server Based Datasources
------------------------------

Server based datasources are convenient for import operations, from a data collection application usually.

Limesurvey Datasource
~~~~~~~~~~~~~~~~~~~~~

Limesurvey datasource is able to extract, from a `Limesurvey <http://www.limesurvey.org/>`_ SQL database, one table per survey with its fully described data dictionary. The data that will be imported are the interviews that are completed.

Opal Datasource
~~~~~~~~~~~~~~~

Opal datasource allows one Opal server to connect to a remote Opal server. This can be useful when syncing datasources in different Opal instances.
