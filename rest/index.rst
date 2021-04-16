REST API Introduction
=====================

The REST API allows to do all necessary operations for managing :doc:`../variables-data` and :doc:`../resources`.

.. _rest-auth:

Authentication
--------------

Opal supports a slightly modified version of `Basic authentication <https://tools.ietf.org/html/rfc7617>`_, which consists of a HTTP request's header field in the form of ``Authorization: X-Opal-Auth <credentials>``, where credentials is the Base64 encoding of user's (or application's) ID and password joined by a single colon ``:``.

Using cURL, it consists of applying the ``Authorization`` header as follow:

.. sourcecode:: shell

   curl -H "Authorization: X-Opal-Auth `echo -n 'administrator:password'|base64`" [...]

Authorization
-------------

Authorizations are group based. The only built-in group is:

============ ===============
Role         Description
============ ===============
``admin``    Can access to all content and settings of the system.
============ ===============

Other groups needs to be granted specific permissions.

Clients
-------

Usage examples provided are based on `cURL <https://curl.se/>`_, a command line client, the Python command line tool (see :doc:`../python-user-guide/index`) and the R package `opalr <https://github.com/obiba/opalr>`_.
