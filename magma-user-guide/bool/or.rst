or
==

Applies the `ternary OR logic <http://en.wikipedia.org/wiki/Ternary_logic>`_ on values. If no arguments is provided, returns the value of the left operand.

See also :doc:`and`.

Syntax
------

.. code-block:: javascript

  or(value_1[, value_i[, ...]])

=============== ============================
Parameter       Description
=============== ============================
``value_i``       The boolean value(s) to be compared to.
=============== ============================

Examples
--------

.. code-block:: javascript

  $('BooleanVar').or($('OtherBooleanVar'))
  $('BooleanVar').or($('OtherBooleanVar').not())
  $('BooleanVar').or($('SomeBooleanVar'), $('OtherBooleanVar'))
