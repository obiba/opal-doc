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

.. note::

  This python package depends on the `pycurl <https://pypi.org/project/pycurl/>`_ package which has some system dependencies. One simple solution
  is to install the ``pycurl`` system package before.

  .. code-block:: bash

    # on Debian systems
    sudo apt-get install python3-pycurl

    # on RPM systems
    sudo yum install python3-pycurl


Usage
-----

To get the options of the command line:

.. code-block:: bash

  opal --help

This command will display which sub-commands are available. Further, given a subcommand obtained from command above, its help message can be displayed via:

.. code-block:: bash

  opal <subcommand> --help

This command will display available subcommands.
