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
``--download-password PASSWORD, -dlp PASSWORD``   Password to encrypt the file content.
``--upload UPLOAD, -up UPLOAD``                   Upload a local file to a folder in Opal file system
``--delete, -dt``                                 Delete a file on Opal file system
``--force, -f``                                   Skip confirmation
================================================= ====================================

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
``--json, -j``    Pretty JSON formatting of the response.
================= =================

Example
-------

Upload a file to Opal file system:

.. code-block:: bash

  opal file --opal https://opal-demo.obiba.org --user administrator --password password -up /path/to/local/file /home/administrator

Download a folder (zip file) from Opal file system:

.. code-block:: bash

  opal file --opal https://opal-demo.obiba.org --user administrator --password password -dl /home/administrator/export/collected > collected.zip

Download a file from Opal file system:

.. code-block:: bash

  opal file --opal https://opal-demo.obiba.org --user administrator --password password -dl /home/administrator/HOP-FNAC2.xml > HOP-FNAC2.xml

Delete a file from Opal file system:

.. code-block:: bash

  opal file --opal https://opal-demo.obiba.org --user administrator --password password -dt /home/administrator/HOP-FNAC2.xml
