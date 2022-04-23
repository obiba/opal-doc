Plugin
======

Manage system plugins.

.. code-block:: bash

  opal plugin <CREDENTIALS> [OPTIONS] [EXTRAS]

Options
-------

======================================== ====================================
Option                                   Description
======================================== ====================================
``--list, -ls``                          List the installed plugins.
``--updates, -lu``                       List the installed plugins that can be updated.
``--available, -la``                     List the new plugins that could be installed.
``--install INSTALL, -i INSTALL``        Install a plugin by providing its name or name:version or a path to a plugin archive file (in Opal file system). If no version is specified, the latest version is installed. Requires system restart to be effective.
``--remove REMOVE, -rm REMOVE``          Remove a plugin by providing its name. Requires system restart to be effective.
``--reinstate REINSTATE, -ri REINSTATE`` Reinstate a plugin that was previously removed by providing its name.
``--fetch FETCH, -f FETCH``              Get the named plugin description.
``--configure CONFIGURE, -c CONFIGURE``  Configure the plugin site properties. Usually requires to restart the associated service to be effective.
``--status STATUS, -su STATUS``          Get the status of the service associated to the named plugin.
``--start START, -sa START``             Start the service associated to the named plugin.
``--stop STOP, -so STOP``                Stop the service associated to the named plugin.
======================================== ====================================

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

List the plugins that are currently installed:

.. code-block:: bash

  opal plugin -o https://opal-demo.obiba.org -u administrator -p password --list --json
