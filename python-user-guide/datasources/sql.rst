.. _python-sql:

SQL
===

Execute a SQL query on one or more tables of a project. Permission to access values of these tables is required.

.. code-block:: bash

  opal sql <CREDENTIALS> [OPTIONS] [XTRAS]

Options
-------
=================================== =====================================
Option                              Description
=================================== =====================================
``--project PROJECT, -pr PROJECT``  Source project name
``--query QUERY, -q QUERY``	        The SQL query
``--format FORMAT, -f FORMAT``      The format of the output, can be ``json`` or ``csv``. Default is ``csv``.
``--id-name ID_NAME, -in ID_NAME``  Name of the ID column name. Default is ``_id``.
=================================== =====================================

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
``--json, -j``    Pretty JSON formatting of the response.
================= =================

Example
-------

Simple SQL query with CSV output:

.. code-block:: bash

  opal sql --opal https://opal-demo.obiba.org --user administrator --password password --project CNSIM --sql "select * from CNSIM1 limit 10"

Simple SQL query with JSON output:

.. code-block:: bash

  opal sql --opal https://opal-demo.obiba.org --user administrator --password password --project CNSIM --sql "select * from CNSIM1 limit 10" --format json

More advanced SQL query:

.. code-block:: bash

  opal sql --opal https://opal-demo.obiba.org --user administrator --password password --project CNSIM --sql "select count(*) as N, avg(LAB_HDL) as HDL_AVG, GENDER from (select * from CNSIM1 union all select * from CNSIM2) where LAB_HDL is not null group by GENDER"
