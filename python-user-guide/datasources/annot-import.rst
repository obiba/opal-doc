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

Credentials
-----------

Authentication is done by username/password credentials.

===================================== ====================================
Option                                Description
===================================== ====================================
``--opal OPAL, -o OPAL``              Opal server base url.
``--user USER, -u USER``              User name. User with appropriate permissions is expected depending of the REST resource requested.
``--password PASSWORD, -p PASSWORD``  User password.
``--ssl-cert SSL_CERT, -sc SSL_CERT`` Path to the certificate (public key) file
``--ssl-key SSL_KEY, -sk SSL_KEY``    Path to the private key file
===================================== ====================================

Extras
------

================= =================
Option            Description
================= =================
``-h, --help``    Show the command help's message.
``--verbose, -v`` Verbose output.
================= =================

Example
-------

Import some annotations to a specified table:

.. code-block:: bash

  opal import-annot --user administrator --password password --destination Study2 --tables datasetA --input /tmp/area-annotations.tsv
