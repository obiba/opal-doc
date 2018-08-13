Python Introduction
===================

Opal Python client, a command line scripting tool written in Python, enables automation of tasks in a Opal server.

Requirements
------------

Python 2.x must be installed on the system. See more about `Python <https://www.python.org/>`_.

Installation
------------

You can install Opal Python Client via the following two methods:

* use the Debian/RPM package manager
* use a Python package

Debian Package Installation
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Follow the `OBiBa Debian Repository <http://www.obiba.org/pages/pkg/>`_ instructions and run:

.. code-block:: bash

  sudo apt-get install opal-python-client

RPM Package Installation
~~~~~~~~~~~~~~~~~~~~~~~~

Follow the `OBiBa RPM Repository <http://www.obiba.org/pages/rpm/>`_ instructions and run:

.. code-block:: bash

  sudo yum install opal-python-client

Python Package Installation
~~~~~~~~~~~~~~~~~~~~~~~~~~~

This type of package is cross-platform (Linux, Windows, Mac).

**Install on Linux or Mac**

1. `Download the most recent version <https://github.com/obiba/opal/releases/download/2.10.12/opal-python-client-2.10.12.tar.gz>`_
2. Decompress the file and enter the installation folder:

.. code-block:: bash

  tar xvzf opal-python-client-X.XX.tar.gz
  cd opal-python-client-X.XX

3. Install the package:

.. code-block:: bash

  sudo python setup.py install --record installed_files.lst

.. note::
  The *--record* will generate a list of installed files on your system. Since there is no uninstaller, you can use this file to remove the Opal Python Client package. You can do this by executing the following command:
  ``sudo cat installed_files.lst | xargs rm -rf``

**Install on Windows**

* Using Cygwin

You can install Cygwin, making sure that CURL, Python, gcc are included and follow these steps inside a Cygwin BASH window:

.. code-block:: bash

  cd /usr/lib
  cp libcurl.dll.a libcurl.a
  cd <your-desired-dir>
  curl -C - -O https://github.com/obiba/opal/releases/download/X.XX/opal-python-client-X.XX.tar.gz
  tar xzvf opal-python-client-X.XX.tar.gz
  cd opal-python-client-X.XX
  python setup.py install --record installed_files.lst

* Using plain Windows tools

This Windows installation is the most complicated one but does not required any third party tools. You are required to do a few manual installations before the package is fully usable. The following steps were tested on a Windows 7.

1. You must have Python installed on your Windows system. Run this `installer <http://www.python.org/ftp/python/2.7.5/python-2.7.5.msi>`_ in case you don't have one.
2. Download the `Google protobuf binary <http://code.google.com/p/protobuf/downloads/detail?name=protoc-2.5.0-win32.zip&can=2&q=>`_ and make sure that its containing folder is in your path.
3. Download the `Google protobuf source <http://code.google.com/p/protobuf/downloads/detail?name=protobuf-2.5.0.zip>`_ package containing the setup.py file and follow these steps:

.. code-block:: bash

  unzip protobuf-2.5.0.zip
  cd protobuf-2.5.0/python
  python setup.py install

4. Go to the `Python Libs <http://www.lfd.uci.edu/~gohlke/pythonlibs/>`_ site and download the file pycurl-7.19.0.win-amd64-py2.7.‌exe
5. Run the installer and follow the instructions until the package is installed
6. `Download the most recent version <https://github.com/obiba/opal/releases/download/2.10.12/opal-python-client-2.10.12.tar.gz>`_ and follow these steps:

.. code-block:: bash

  unzip opal-python-client-X.XX.tar.gz
  cd opal-python-client-X.XX
  python setup.py bdist_wininst
  cd dist

7. Execute the generated installer and follow the instructions (opal-python-client-X.XX.win-amd64.exe)

Usage
-----

To get the options of the command line:

.. code-block:: bash

  opal --help

This command will display which sub-commands are available. Further, given a subcommand obtained from command above, its help message can be displayed via:

.. code-block:: bash

  opal <subcommand> --help

This command will display available subcommands.
