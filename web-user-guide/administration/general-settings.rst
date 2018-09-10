General Settings
================

This section is about system level configuration. Accessible only by an administrator.

Properties
----------

===================== =====================
Property	            Description
===================== =====================
Name	                Name of the Opal server that will be displayed in the web interface. Helps to distinguish several Opal instances.
Default Character Set	When reading/writing files, if a character set is not specified, Opal defaults to ISO-8859-1. This is used for example when reading/writing CSV files.
Public URL	          Public base URL of the server (not the web-interface one) that will be used when sending notification emails on report generation.
Language	            Default languages to consider when editing a data dictionary.
===================== =====================

.. _encryption-keys:

Encryption Keys
---------------

HTTPS connection requires to have a private key and a public key (certificate) defined. A self-signed key-pair is available by default. You can provide your own. Opal server needs to be restarted after the encryption keys have been updated.
