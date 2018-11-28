lowerCase
=========

Returns a copy of the string, lower cased.

See also :doc:`capitalize`, :doc:`concat`, :doc:`replace`, :doc:`trim`, :doc:`upperCase`.

Syntax
------

.. code-block:: javascript

  lowerCase([locale])

=============== ============================
Parameter       Description
=============== ============================
``locale``      The optional locale to be used, as a string with syntax: ``language[_country[_variant]]``.
=============== ============================

Examples
--------

.. code-block:: javascript

  $('AVar').lowerCase()
  $('AVar').lowerCase('fr_CA')
