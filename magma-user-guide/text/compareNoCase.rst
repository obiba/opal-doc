compareNoCase
=============

Returns a negative integer, zero, or a positive integer as the text value is less than, equal to, or greater than the text value argument ignoring case.

See also :doc:`../bool/compare`.

Syntax
------

.. code-block:: javascript

  compareNoCase(value)

=============== ============================
Parameter       Description
=============== ============================
``value``       The value to be compared to, ignoring case.
=============== ============================

Examples
--------

.. code-block:: javascript

  $('AVar').compareNoCase($('OtherVar'));
