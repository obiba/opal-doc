Web Services
============

This command is for advanced users wanting to directly access to the REST API of Mica server.

.. code-block:: bash

  mica rest ws <CREDENTIALS> [OPTIONS] [EXTRA]

Arguments
---------

======== ===========
Argument Description
======== ===========
``ws``	 Web service path, for instance: /user/xxx
======== ===========

Credentials
-----------

Authentication is done by username/password credentials.

==================================== ====================================
Option                               Description
==================================== ====================================
``--mica MICA, -mk MICA``            Mica server base url.
``--user USER, -u USER``             User name. User with appropriate permissions is expected depending of the REST resource requested.
``--password PASSWORD, -p PASSWORD`` User password.
==================================== ====================================

Options
-------

================================================= ====================================
Option                                            Description
================================================= ====================================
``--method METHOD, -m METHOD``                    HTTP method: GET (default), POST, PUT, DELETE, OPTIONS.
``--accept ACCEPT, -a ACCEPT``                    Accept header (default is application/json).
``--content-type CONTENT_TYPE, -ct CONTENT_TYPE`` Content-Type header (default is application/json).
``--json, -j``                                    Pretty JSON formatting of the response.
================================================= ====================================

Extras
------

================= =================
Option            Description
================= =================
``-h, --help``    Show the command help's message
``--verbose, -v`` Verbose output
================= =================

Example
-------

Get all the published studies visible to an anonymous user.

.. code-block:: bash

  mica rest /studies -m GET -mk https://mica-demo.obiba.org -u anonymous -p password -a application/json -j

Add a new individual study document:

.. code-block:: bash

  mica rest /draft/individual-studies -m POST -u administrator -p password -mk https://mica-demo.obiba.org -a application/json < patate-study.json

Search all files of the draft version of a network:

.. code-block:: bash

  mica rest /draft/files-search/network/some-network -m GET -mk https://mica-demo.obiba.org -u administrator -p password -a application/json -j
