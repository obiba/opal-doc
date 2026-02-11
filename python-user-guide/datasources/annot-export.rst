Annotations Export
==================

Export the variable annotations of one or all tables of a project. This can be used to backup annotations, that can be restored using :doc:`annot-import`.

.. code-block:: bash

  opal export-annot <RESOURCE> <CREDENTIALS> [OPTIONS] [EXTRAS]

Arguments
---------

============= ===========
Argument      Description
============= ===========
``RESOURCE``	Resource identification in the format ``<datasource>[.<table>]``. Each project has a datasource which is identified by the project's name.
============= ===========

Options
-------
========================================================================================== =====================================
Option                                                                                     Description
========================================================================================== =====================================
``--output OUTPUT, -out OUTPUT``                                                           CSV/TSV file path where to write the exported annotations. When not specified, standard output is used.
``--locale LOCALE, -l LOCALE``                                                             Exported locale (default is none)
``--separator SEPARATOR, -s SEPARATOR``                                                    The character separator to be used in the output. When not specified tab character is used.
``--taxonomies TAXONOMY1 [--taxonomies TAXONOMY2 ...], -tx TAXONOMY1 [-tx TAXONOMY2 ...]`` The list of taxonomy names of interest (default is any that are found in the variable attributes).
========================================================================================== =====================================

.. include:: ../common-credentials.rst

.. include:: ../common-extras.rst

Example
-------

Export annotations of the Mlstr_area taxonomy from a specific table:

.. code-block:: bash

  opal export-annot --opal https://opal-demo.obiba.org --user administrator --password password CLSA --taxonomies Mlstr_area --output /tmp/clsa-area.tsv
