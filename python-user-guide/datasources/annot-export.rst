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

Authentication can be done by username/password credentials OR by personal access token OR by certificate/private key pair (two-way SSL authentication).

===================================== ====================================
Option                                Description
===================================== ====================================
``--opal OPAL, -o OPAL``              Opal server base url
``--user USER, -u USER``              Credentials auth: user name (requires a password)
``--password PASSWORD, -p PASSWORD``  Credentials auth: user password (requires a user name)
``--token TOKEN, -tk TOKEN``          Token auth: User access token
``--ssl-cert SSL_CERT, -sc SSL_CERT`` Two-way SSL auth: certificate/public key file (requires a private key)
``--ssl-key SSL_KEY, -sk SSL_KEY``    Two-way SSL auth: private key file (requires a certificate)
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
