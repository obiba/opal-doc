SQL History
===========

Extract the list of the SQL queries executed, with their error status (if any), start/end time and project context (if any). Regular users can only retrieve their own queries, whereas administrators can retrieve queries from all or any users.

.. code-block:: bash

  opal sql-history <CREDENTIALS> [OPTIONS] [XTRAS]

Options
-------
=================================== =====================================
Option                              Description
=================================== =====================================
``--project PROJECT, -pr PROJECT``  Project name used as the SQL execution context to filter. If not specified, history from any context is returned. If '*' is specified, history of SQL execution without context is returned.
``--offset OFFSET, -os OFFSET``     Number of history items to skip. Default is 0 (note that the items are ordered by most recent first).
``--limit LIMIT, -lm LIMIT``        Maximum number of history items to return. Default is 100.
``--subject SUBJECT, -sb SUBJECT``  Filter by user name, only administrators can retrieve SQL history of other users. If '*' is specified, history of all users is retrieved. Default is the current user name.
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

Get own SQL queries history:

.. code-block:: bash

  opal sql-history --opal https://opal-demo.obiba.org --user administrator --password password

Get own SQL queries history on project CNSIM:

.. code-block:: bash

  opal sql-history --opal https://opal-demo.obiba.org --user administrator --password password --project CNSIM

Get other user SQL queries history on project CNSIM (requires administrator rights):

.. code-block:: bash

  opal sql-history --opal https://opal-demo.obiba.org --user administrator --password password --subject someuser --project CNSIM

Get all users, one thousand most recent SQL queries history (requires administrator rights):

.. code-block:: bash

  opal sql-history --opal https://opal-demo.obiba.org --user administrator --password password --subject '*' --limit 1000
