How to Import Data from Files
=============================

Importing CSV Data
------------------

The following applies to any delimited textual file formats, CSV (comma delimiter) being is the most common one.

Opal supports two CSV importers:

* **CSV**, which is the built-in one,
* **CSV (R)**, available as a plugin (*opal-datasource-readr*, see :ref:`admin-plugins` administration), based on the `readr R package <https://readr.tidyverse.org/>`_.

The main difference between these two CSV importers is how the data types are handled.

CSV Importer
~~~~~~~~~~~~

In the case of **CSV** importer, the data types are not guessed from the provided CSV file:

* Either the destination table already exists and then the variable value types are the ones declared (if there is an inconsistency with the provided data, import will fail),
* Or all the value types are **text**.

Setting up the destination table variables prior to the **CSV** import can be counter intuitive and error prone (missing variables, wrong data types): this is NOT a recommended procedure. The recommended approach is to import first the CSV data as-is and then make a view (i.e. a logical table) to transform variable value types to the correct ones.

The import steps to follow are:

1. Go to the destination project's tables page,
2. Select **Import**,
3. Select the Data Format **CSV**, follow instructions (upload CSV file, set options etc.) and launch the import task,
4. When the CSV import task is completed, go to the new table's page (note that all variables have **text** type),
5. Make a view based on the imported table: :ref:`cb-views`.

CSV (R) Importer
~~~~~~~~~~~~~~~~

This R-based importer will attempt to detect the data types by reading the first 1000 rows. In case a variable has no values in these first rows, the **text** value type will be used.

The import steps to follow are:

0. Preliminary: having the *opal-datasource-readr* plugin installed and a functional R server,
1. Go to the destination project's tables page,
2. Select **Import**,
3. Select the Data Format **CSV (R)**, follow instructions (upload CSV file, set options etc.) and launch the import task,
4. When the CSV (R) import task is completed, go to the new table's page.

Importing SPSS, SAS, Stata Data
-------------------------------

Unlike the CSV file format, the SPSS/SAS/Stata file formats contain their own data dictionary. Opal uses the `haven R package <https://haven.tidyverse.org/>`_ (and then require a functional R server) to import data in these formats: value types, categories, missing values etc. are extracted from the R data structure.
