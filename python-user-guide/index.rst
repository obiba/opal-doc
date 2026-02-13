Python Introduction
===================

Opal Python client, a command line scripting tool (see :ref:`py`) and an API (see :ref:`apipy`) written in Python, enables automation of tasks in a Opal server.

Requirements
------------

Python 3.7+ must be installed on the system. See more about `Python <https://www.python.org/>`_.

Installation
------------

The Opal Python Client is available on the official `Python Package Index <https://pypi.org/>`_.

.. code-block:: bash

  sudo pip install obiba-opal

.. note::
  Previous versions were available as system packages. Make sure to remove them before installing the package with ``pip``.

  .. code-block:: bash

    # on Debian systems
    sudo apt-get remove opal-python-client

    # on RPM systems
    sudo yum remove opal-python-client

Usage
-----

To get the options of the command line:

.. code-block:: bash

  opal --help

This command will display which sub-commands are available. Further, given a subcommand obtained from command above, its help message can be displayed via:

.. code-block:: bash

  opal <subcommand> --help

This command will display available subcommands.

Upgrade Notes
-------------

Since version 6.0.0, the command line options have slightly changed. The new syntax for multiple values is to repeat the option for each value instead of providing a list of values.

For example, the new syntax for multiple tables is:

.. code-block:: bash

  opal <subcommand> --tables TABLE01 --tables TABLE02

instead of:

.. code-block:: bash

  opal <subcommand> --tables TABLE01 TABLE02

For backward compatibility, the old syntax is still supported with the alternative command `opal-legacy`:

.. code-block:: bash

  opal-legacy <subcommand> --tables TABLE01 TABLE02