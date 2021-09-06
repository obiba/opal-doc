How to Import Data from R
=========================

If the Opal server's data importers are not sufficient (unsupported data format, missing data extraction options etc.), the recommended alternative is to use a R script to:

* Extract data by connecting to a data source in R
* [optional] Perform data cleansing
* [optional] Build the data dictionary
* Save data into a Opal table
* [optional] Automate data import operations

Prerequisites
-------------

Install R Packages
~~~~~~~~~~~~~~~~~~

Opal is a server application. The client R script will connect the Opal server. Then the prerequisites are:

* Server: having Opal connected to a functional R server,
* Client: having the `opalr R package <https://www.obiba.org/opalr/>`_ installed, and data sources accessible.

See also the :ref:`r` documentation.

Connect with Server
~~~~~~~~~~~~~~~~~~~

Your script must start with:

.. code-block:: r

  # load opal library
  library(opalr)
  # connect to the opal server
  o <- opal.login(...)

See the `opal.login() <https://www.obiba.org/opalr/reference/opal.login.html>`_ documentation for more details about credentials.

Prepare Project
~~~~~~~~~~~~~~~

If the destination project does not exist yet, it is possible to create it using R:

.. code-block:: r

  # create a new project with a database backend for storing tables' data
  opal.project_create(o, "myproject", database = TRUE)

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

  # save 'data' tibble into 'mytable' table, using 'id' column to provide identifiers
  opal.table_save(o, data, project = "myproject", table = "mytable", id.name = "id")

See the `opal.table_save() <https://www.obiba.org/opalr/reference/opal.table_save.html>`_ documentation for more details about saving operation options.

Data Dictionary
---------------

The data dictionary in Opal is a rich description of the data.

Before Import
~~~~~~~~~~~~~

The data dictionary can be fully or partially described directly in the tibble that will be imported.

.. rubric:: Raw R Attributes

The data dictionary can be fine-tuned before saving the data into a Opal table. As an example, a R column of type ``double`` can be saved as a variable with the ``integer`` value type in place of the default ``decimal`` one. This is done by setting the R vector attributes with some Opal keys.

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

For instance, the column *cyl* will be interpreted as a vector of integer values at *data* importation time:

.. code-block:: r

  data <- tibble::as_tibble(mtcars)
  # apply 'opal.value_type' attribute to 'cyl' column
  attributes(data$cyl) <- list(opal.value_type = 'integer')

Another example makes a numerical variable with categories in Opal from a factor column in R:

.. code-block:: r

  data <- tibble::as_tibble(mtcars)
  # make column a factor, each level will be a category
  data$cyl <- as.factor(data$cyl)
  # append 'opal.value_type' attribute to 'cyl' column
  attributes(data$cyl) <- append(attributes(data$cyl), list(opal.value_type = 'integer'))

.. rubric:: Full Data Dictionary

Another approach is to apply the full data dictionary (same structure as in the :download:`Excel template <../../archive/opalVariableTemplate.xls>`) to the tibble to be saved. Use the `dictionary.apply() <https://www.obiba.org/opalr/reference/dictionary.apply.html>`_ for that purpose.

It is not necessary to use Excel to define this data dictionary:

.. code-block:: r

  data <- tibble::as_tibble(mtcars)
  variables <- tibble::tribble(
    ~name, ~valueType, ~`label:en`,  ~`Namespace::Name`, ~unit, ~repeatable, ~index,
    "mpg", "decimal", "Mpg label",  "Value1", "years", 0, 1,
    "cyl", "integer", "Cyl label",  "Value2", "kg/m2", 0, 2,
    "disp", "decimal", "Disp label", NA, NA, 1, 3
  )
  categories <- tibble::tribble(
    ~variable, ~name, ~missing, ~`label:en`,
    "cyl", "4", 0, "Four",
    "cyl", "6", 0, "Six",
    "cyl", "8", 1, "Height"
  )
  data <- dictionary.apply(data, variables, categories)

.. rubric:: Taxonomy Term Annotations

To annotate one or more variables with a taxonomy term without having to define a full data dictionary, see the `dictionary.annotate() <https://www.obiba.org/opalr/reference/dictionary.annotate.html>`_ documentation.

.. code-block:: r

  # annotate some variables with a taxonomy term
  data <- dictionary.annotate(data,
    variables = c("A_SDC_EDU_LEVEL", "A_SDC_EDU_LEVEL_AGE"),
    taxonomy = "Mlstr_area",
    vocabulary = "Sociodemographic_economic_characteristics",
    term = "Education")

After Import
~~~~~~~~~~~~

.. rubric:: Table Dictionary

After data have been saved the data dictionary can be amended, except the variable value types. See previous section (*Before Import*) to control value types at importation time.

Other data dictionary properties and attributes can be set using the same data structure as in the :download:`Excel template <../../archive/opalVariableTemplate.xls>`, expressed in R.

See the `opal.table_dictionary_update() <https://www.obiba.org/opalr/reference/opal.table_dictionary_update.html>`_ documentation (that can be usefully combined with `opal.table_dictionary_get() <https://www.obiba.org/opalr/reference/opal.table_dictionary_get.html>`_).

As an example the following data dictionary defined in R is applied to an Opal table:

.. code-block:: r

  variables <- tibble::tribble(
    ~name, ~valueType, ~`label:en`,  ~`Namespace::Name`, ~unit, ~repeatable, ~index,
    "mpg", "decimal", "Mpg label",  "Value1", "years", 0, 1,
    "cyl", "integer", "Cyl label",  "Value2", "kg/m2", 0, 2,
    "disp", "decimal", "Disp label", NA, NA, 1, 3
  )
  categories <- tibble::tribble(
    ~variable, ~name, ~missing, ~`label:en`,
    "cyl", "4", 0, "Four",
    "cyl", "6", 0, "Six",
    "cyl", "8", 1, "Height"
  )
  opal.table_dictionary_update(o, "myproject", "mytable", variables, categories)

.. rubric:: View Dictionary

When data type has not been specified before the import and needs to be changed, an Opal view can transform values on the fly. See the :ref:`cb-views` for making a view based on the imported table using R.

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
