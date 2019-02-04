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
============================================================================= =====================================
Option                                                                        Description
============================================================================= =====================================
``--output OUTPUT, -out OUTPUT``                                              CSV/TSV file path where to write the exported annotations. When not specified, standard output is used.
``--locale LOCALE, -l LOCALE``                                                Exported locale (default is none)
``--separator SEPARATOR, -s SEPARATOR``                                       The character separator to be used in the output. When not specified tab character is used.
``--taxonomies TAXONOMIES [TAXONOMIES ...], -tx TAXONOMIES [TAXONOMIES ...]`` The list of taxonomy names of interest (default is any that are found in the variable attributes).
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

Export annotations of the Mlstr_area taxonomy from a specific table:

.. code-block:: bash

  opal export-annot --opal https://opal-demo.obiba.org --user administrator --password password CLSA --taxonomies Mlstr_area --out /tmp/clsa-area.tsv
