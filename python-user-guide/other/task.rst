Task
====

Manage a task, for shell scripts submitting tasks (import/export) and waiting for their completion.

.. code-block:: bash

  opal task <CREDENTIALS> [OPTIONS] [EXTRAS]

Options
-------

========================= ====================================
Option                    Description
========================= ====================================
``--id ID``               The task ID. If not provided, it will be read from the standard input (from the JSON representation of the task or a plain value).
``--show, -sh``           Show JSON representation of the task
``--status, -st``         Get the status of the task
``--wait, -w``            Wait for the task to complete (successfully or not)
``--cancel, -c``          Cancel the task
``--delete, -d``          Delete the task
========================= ====================================

.. include:: ../common-credentials.rst

.. include:: ../common-extras-json.rst

Example
-------

Get the full status of a task:

.. code-block:: bash

  opal task -o https://opal-demo.obiba.org -u administrator -p password --id 1 --json

Get the status token of a task:

.. code-block:: bash

  opal task -o https://opal-demo.obiba.org -u administrator -p password --id 1 --status

Wait for the task to complete and get its status token:

.. code-block:: bash

  opal task -o https://opal-demo.obiba.org -u administrator -p password --id 1 --wait
