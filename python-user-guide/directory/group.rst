Group
=====

Manage a group in the Opal internal user directory.

.. code-block:: bash

  opal group <CREDENTIALS> [OPTIONS] [EXTRAS]

Options
-------

========================== =====================================
Option                     Description
========================== =====================================
``--name NAME, -n NAME``   Group name
``--fetch, -f``            Fetch a user (all groups are returned if no option --name is given)
``--delete, -de``          Delete the group specified by the --name option
========================== =====================================

.. include:: ../common-credentials.rst

.. include:: ../common-extras-json.rst

Example
-------

Get the list of groups with associated users

.. code-block:: bash

  opal group --opal https://opal-demo.obiba.org --user administrator --password password --fetch

Get a specific group with associated users

.. code-block:: bash

  opal group --opal https://opal-demo.obiba.org --user administrator --password password --fetch --name editor

Delete the group study_editor

.. code-block:: bash

  opal group --opal https://opal-demo.obiba.org --user administrator --password password --delete --name study_editor
