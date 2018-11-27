round
=====

Returns the rounded value of the current value.

Syntax
------

.. code-block:: javascript

  round([scale])

=============== ============================
Parameter       Description
=============== ============================
``scale``       The number of decimals, default is 2.
=============== ============================

Examples
--------

.. code-block:: javascript

  // round to 2 decimals (default)
  $('AVar').round()
  // round to specified number of decimals
  $('AVar').round(4)
