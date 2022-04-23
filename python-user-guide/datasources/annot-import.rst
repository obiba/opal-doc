Annotations Import
==================

Import the variable annotations of one or more tables. This can be used to restore annotations that were backed up using :doc:`annot-export`.

.. code-block:: bash

  opal import-annot <CREDENTIALS> [OPTIONS] [EXTRAS]

Options
-------
============================================================================= =====================================
Option                                                                        Description
============================================================================= =====================================
``--input INPUT, -in INPUT``                                                  CSV/TSV input file, typically the output of the export-annot command (default is stdin)
``--locale LOCALE, -l LOCALE``                                                Destination annotation locale (default is none)
``--separator SEPARATOR, -s SEPARATOR``                                       Separator char for CSV/TSV format (default is the tabulation character)
``--destination DESTINATION, -d DESTINATION``	                                Destination project name (default is the one(s) specified in the input file)
``--tables TABLES [TABLES ...], -t TABLES [TABLES ...]``                      The list of tables which variables are to be annotated (defaults to all that are found in the input file)
``--taxonomies TAXONOMIES [TAXONOMIES ...], -tx TAXONOMIES [TAXONOMIES ...]`` The list of taxonomy names of interest (default is any that is found in the input file)
============================================================================= =====================================

.. include:: ../common-credentials.rst

.. include:: ../common-extras.rst

Example
-------

Import some annotations to a specified table:

.. code-block:: bash

  opal import-annot --user administrator --password password --destination Study2 --tables datasetA --input /tmp/area-annotations.tsv
