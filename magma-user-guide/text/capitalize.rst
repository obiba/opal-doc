capitalize
==========

Returns a copy of the string, with first characters of each word capitalized.

See also :doc:`upperCase`, :doc:`lowerCase`, :doc:`replace`, :doc:`trim`, :doc:`concat`.

Syntax
------

.. code-block:: javascript

  capitalize([delimiters])

=============== ============================
Parameter       Description
=============== ============================
``delimiters``  The optional delimiting characters for identifying words. Default is ' '.
=============== ============================

Examples
--------

.. code-block:: javascript

  $('AVar').capitalize()
  $('AVar').capitalize(':;,( .["')
