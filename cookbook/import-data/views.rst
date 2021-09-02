.. _cb-views:

How to Transform Tables with Views
==================================

A table is the result of importing data. Depending on the source of the data, the value types of the variables may not be correct (e.g. **text** instead of **integer**) and the data dictionary may be missing or incomplete (e.g. CSV provides only variable names).

Views are logical tables that can be used both for transforming data (e.g. recoding) and enhancing the data dictionary. The advantage of using a view instead of modifying the imported table's variables is that the table can be dropped, data can be updated/imported again without affecting the view's data dictionary.

From a Table
------------

This is a manual operation that can be very straightforward.

1. Go to the table's page
2. Select variables (either all or only the ones of interest)
3. Select **Add to view**

⇒ The view is created (or updated if it already exists) with the selected variables.

From a Variable
---------------

This operation allows to fine tune the transformation script, useful when setting categories from an originally continuous variable.

1. Go to the variable's page
2. Select from the **Derive** menu the appropriate derivation operation
3. Follow derivation wizard instructions

⇒ The view is created (or updated if it already exists) with the selected variables.

Using Excel
-----------

It can be convenient for batch processing and for Excel lovers, to prepare the view using an Excel file. This file will both contains the variable descriptions and the data transformation scripts.

* Either follow the instructions in the :download:`Excel template <../../archive/opalVariableTemplate.xls>` to make your data dictionary from scratch,
* Or download the table's dictionary to start from a prefilled Excel file.

The derivation script is to be defined in the **script** column (see :ref:`magmajs`).

When the Excel file is ready:

1. Go to the project's tables page
2. Select **Add Table > Add view...**
3. Upload the Excel file and select the table on which the view is based

⇒ The view is created with the provided variables.

Using R
-------

The `opalr R package <https://www.obiba.org/opalr>`_ is very powerful for interacting with a Opal server.

A view can be created with the `opal.table_create() <https://www.obiba.org/opalr/reference/opal.table_create.html>`_ function and its data dictionary updated with the `opal.table_dictionary_update() <https://www.obiba.org/opalr/reference/opal.table_dictionary_update.html>`_ function.

See also data dictionary management examples from the `Opal Projects vignette <https://www.obiba.org/opalr/articles/opal-projects.html#dictionaries-1>`_.
