Project
=======

Manage a project.

.. code-block:: bash

  opal project <CREDENTIALS> [OPTIONS] [EXTRAS]

Options
-------

=============================================== =====================================
Option                                          Description
=============================================== =====================================
``--name NAME, -n NAME``                        Project name. If no name and no action is specified, the list of the projects will be returned.
``--fetch, -f``                                 Fetch a project.
``--delete, -de``                               Delete the project specified by the --name option
``--force, -f``                                 Skip confirmation on project deletion
``--add, -a``                                   Add a project specified by the --name option
``--database DATABASE, -db DATABASE``           Name of the database to be associated to the project at creation time (optional, unless you intend to import data).
``--title TITLE, -t TITLE``                     The project's title at creation time (optional).
``--description DESCRIPTION, -dc DESCRIPTION``  The project's description at creation time (optional).
``--tags TAGS [TAGS ...], -tg TAGS [TAGS ...]`` The project tags at creation time (optional, separated by space).
=============================================== =====================================

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
``--json, -j``    Output pretty-print JSON
================= =================

Example
-------

Get the list of projects with pretty JSON formatted output:

.. code-block:: bash

  opal project --opal https://opal-demo.obiba.org --user administrator --password password --json

Get a specific project:

.. code-block:: bash

  opal project --opal https://opal-demo.obiba.org --user administrator --password password --name CNSIM

Create the project foo without associated database:

.. code-block:: bash

  opal project --opal https://opal-demo.obiba.org --user administrator --password password --add --name foo

Delete the project foo:

.. code-block:: bash

  opal project --opal https://opal-demo.obiba.org --user administrator --password password --delete --name foo
