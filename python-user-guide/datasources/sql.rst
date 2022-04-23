.. _python-sql:

SQL
===

Execute a SQL query on one or more tables of a project. Permission to access values of these tables is required.

See more SQL query examples in the Project Tables :ref:`sql` section.

.. code-block:: bash

  opal sql <CREDENTIALS> [OPTIONS] [XTRAS]

Options
-------
=================================== =====================================
Option                              Description
=================================== =====================================
``--project PROJECT, -pr PROJECT``  Source project name, that will be used to resolve the table names in the FROM statement. If not provided, the fully qualified table names must be specified in the query (escaped by backquotes: \`<project>.<table>\`).
``--query QUERY, -q QUERY``	        The SQL query
``--format FORMAT, -f FORMAT``      The format of the output, can be ``json`` or ``csv``. Default is ``csv``.
``--id-name ID_NAME, -in ID_NAME``  Name of the ID column name. Default is ``_id``.
=================================== =====================================

.. include:: ../common-credentials.rst

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

Simple SQL query with CSV output and without specifying a project in the arguments:

.. code-block:: bash

  opal sql --opal https://opal-demo.obiba.org --user administrator --password password --sql "select * from `CNSIM.CNSIM1` limit 10"
