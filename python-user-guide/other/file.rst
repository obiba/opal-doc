File
====

Manage files in the Opal file system.

.. code-block:: bash

  opal file <PATH> <CREDENTIALS> [OPTIONS] [EXTRAS]

Arguments
---------

======== ===========
Argument Description
======== ===========
``PATH`` The path of the file in the Opal file system
======== ===========

Options
-------

================================================= ====================================
Option                                            Description
================================================= ====================================
``--download, -dl``                               Download a file or a folder (as a zip file)
``--download-password PASSWORD, -dlp PASSWORD``   Password to encrypt the file content (8 characters minimum).
``--upload UPLOAD, -up UPLOAD``                   Upload a local file to a folder in Opal file system
``--delete, -dt``                                 Delete a file on Opal file system
``--force, -f``                                   Skip confirmation
================================================= ====================================

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

Upload a file to Opal file system:

.. code-block:: bash

  opal file --opal https://opal-demo.obiba.org --user administrator --password password -up /path/to/local/file /home/administrator

Download a folder (encrypted zip file) from Opal file system:

.. code-block:: bash

  opal file --opal https://opal-demo.obiba.org --user administrator --password password --download-password foobar123 /home/administrator/export/collected > collected.zip

Download a file from Opal file system:

.. code-block:: bash

  opal file --opal https://opal-demo.obiba.org --user administrator --password password -dl /home/administrator/HOP-FNAC2.xml > HOP-FNAC2.xml

Delete a file from Opal file system:

.. code-block:: bash

  opal file --opal https://opal-demo.obiba.org --user administrator --password password -dt /home/administrator/HOP-FNAC2.xml
