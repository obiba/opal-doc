How to Import Data from R
=========================

If the Opal server's data importers are not sufficient (unsupported data format, missing data extraction options etc.), the recommended alternative is to use a R script to:

* Extract data by connecting to a data source in R
* [optional] Perform data cleansing
* [optional] Build the data dictionary
* Save data into a Opal table
* [optional] Automate data import operations

Prerequisite
------------

Opal is a server application. The client R script will connect the Opal server. Then the prerequisites are:

* Server: having Opal connected to a functional R server,
* Client: having the `opalr R package <https://www.obiba.org/opalr/>`_ installed, and data sources accessible.

See also the :ref:`r` documentation.

Your script must start with:

.. code-block:: r

  # load opal library
  library(opalr)
  # connect to the opal server
  o <- opal.login(...)

See the `opal.login() <https://www.obiba.org/opalr/reference/opal.login.html>`_ documentation for more details about credentials.

Prepare Project
---------------

If the destination project does not exist yet, it is possible to create it using R:

.. code-block:: r

  # create a new project with a database backend for storing tables' data
  opal.project_create(o, "dummy", database = TRUE)

You can find more information in the `Opal Projects vignette <https://www.obiba.org/opalr/articles/opal-projects.html>`_.

Import Data
-----------

There are many ways of having data available in R whether the source is a file, a database, a remote service etc. Some reference manuals can be found at:

* `R Data Import/Export <https://cran.r-project.org/doc/manuals/r-release/R-data.html>`_
* `R for Data Science: Data import <https://r4ds.had.co.nz/data-import.html>`_
* `rio: A Swiss-Army Knife for Data I/O <https://cran.r-project.org/package=rio>`_
* ...

Make sure your data are `tidy <https://r4ds.had.co.nz/tidy-data.html>`_, and identify which column holds the identifiers. The expected R data structure for data import into Opal is a `tibble <https://r4ds.had.co.nz/tibbles.html>`_. Saving the data into a Opal table is as simple as:

.. code-block:: r

  # save 'mydata' tibble into 'mytable' table
  opal.table_save(o, mydata, project = "dummy", table = "mytable")

See the `opal.table_save() <https://www.obiba.org/opalr/reference/opal.table_save.html>`_ documentation for more details about saving operation options.

Data Dictionary
---------------

The data dictionary in Opal is a rich description of the data.

Before Import
~~~~~~~~~~~~~

The data dictionary can be fully or partially described directly in the tibble that will be imported.

.. rubric:: Raw R Attributes

The data dictionary can be fine-tuned before saving the data into a Opal table. As an example, a R column of type ``double`` can be saved as a variable with the ``integer`` value type in place of the default ``decimal`` one. This is done by setting the R vector attributes with some Opal keys. For instance, the column *var1* will be interpreted as a vector of integer values at *mydata* importation time:

.. code-block:: r

  attributes(mydata$var1) <- list(opal.value_type = 'integer')

The R attribute keys that can be used are:

.. list-table::
  :header-rows: 1

  * - R attribute
    - Description
  * - ``opal.value_type``
    - Variable value type, as described in the :ref:`vars-cats` section.
  * - ``opal.unit``
    - The measurement unit of the variable values.
  * - ``opal.referenced_entity_type``
    - The type of the entity referred when variable values are identifiers.
  * - ``opal.mime_type``
    - The mime type of the variable values.
  * - ``opal.repeatable``
    - Whether the variable has repeated values. True when value is "1", false otherwise.
  * - ``opal.occurrence_group``
    - Name of the occurrence group, when several variables are repeated together.
  * - ``opal.index``
    - Position in the variables list, for ordering.

.. rubric:: Full Data Dictionary

Another approach is to apply the full data dictionary (same structure as in the :download:`Excel template <../../archive/opalVariableTemplate.xls>`) to the tibble to be saved. Use the `dictionary.apply() <https://www.obiba.org/opalr/reference/dictionary.apply.html>`_ for that purpose.

.. rubric:: Taxonomy Term Annotations

To annotate one or more variables with a taxonomy term without having to define a full data dictionary, see the `dictionary.annotate() <https://www.obiba.org/opalr/reference/dictionary.annotate.html>`_ documentation.

After Import
~~~~~~~~~~~~

After the data import, the data dictionary can be amended in Opal.

.. rubric:: Table Dictionary

After data have been saved it is NOT possible to modify the value types. See previous section (*Before Import*) to control value types at importation time.

Other data dictionary properties and attributes can be set using the same data structure as in the :download:`Excel template <../../archive/opalVariableTemplate.xls>`, expressed in R.

See the `opal.table_dictionary_update() <https://www.obiba.org/opalr/reference/opal.table_dictionary_update.html>`_ documentation (that can be usefully combined with `opal.table_dictionary_get() <https://www.obiba.org/opalr/reference/opal.table_dictionary_get.html>`_).

.. rubric:: View Dictionary

See also the :ref:`cb-views` for making a view based on the imported table using R.

Procedure
---------

.. note::

  0. Preliminary: install opalr R package
  1. Connect to Opal server using ``opal.login()``
  2. Load and prepare data in R as a ``tibble`` object
  3. [optional] Fine tune data dictionary using ``attributes()`` or ``dictionary.apply()`` or ``dictionary.annotate()``
  4. Save data using ``opal.table_save()``
  5. [optional] Update data dictionary using ``opal.table_dictionary_get()``

  ⇒ The table is created/updated with the imported data and is to be accessed directly or through a view
