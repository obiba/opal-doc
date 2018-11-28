and
===

Applies the `ternary AND logic <http://en.wikipedia.org/wiki/Ternary_logic>`_ on values. If no arguments is provided, returns the value of the left operand.

See also :doc:`or`.

Syntax
------

.. code-block:: javascript

  and(value_1[, value_i[, ...]])

=============== ============================
Parameter       Description
=============== ============================
``value_i``       The boolean value(s) to be compared to.
=============== ============================

Examples
--------

.. code-block:: javascript

  $('BooleanVar').and($('OtherBooleanVar'))
  $('BooleanVar').and($('OtherBooleanVar').not())
  $('BooleanVar').and($('SomeBooleanVar'), $('OtherBooleanVar'))
