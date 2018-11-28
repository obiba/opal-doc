upperCase
=========

Returns a copy of the string, upper cased.

See also :doc:`capitalize`, :doc:`lowerCase`, :doc:`replace`, :doc:`trim`, :doc:`concat`.

Syntax
------

.. code-block:: javascript

  upperCase([locale])

=============== ============================
Parameter       Description
=============== ============================
``locale``      The optional locale to be used, as a string with syntax: ``language[_country[_variant]]``.
=============== ============================

Examples
--------

.. code-block:: javascript

  $('AVar').upperCase()
  $('AVar').upperCase('fr_CA')
