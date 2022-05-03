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
``--delete, -de``                               Delete the project specified by the --name option
``--force, -f``                                 Skip confirmation on project deletion
``--add, -a``                                   Add a project specified by the --name option
``--database DATABASE, -db DATABASE``           Name of the database to be associated to the project at creation time (optional, unless you intend to import data).
``--title TITLE, -t TITLE``                     The project's title at creation time (optional).
``--description DESCRIPTION, -dc DESCRIPTION``  The project's description at creation time (optional).
``--tags TAGS [TAGS ...], -tg TAGS [TAGS ...]`` The project tags at creation time (optional, separated by space).
``--export-folder EXPORT_FOLDER``               The project's preferred export folder (optional).
=============================================== =====================================

.. include:: ../common-credentials.rst

.. include:: ../common-extras-json.rst

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
