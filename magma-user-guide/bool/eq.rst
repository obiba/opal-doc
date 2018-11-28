eq
==

Returns if left operand value is equal to right operand value. The operands must be either be both of:

* integer or decimal type.
* boolean type.
* text type.

If the left operand is a value sequence, the method will check equality for each of the values provided (sequences must be of same length and content must be equal). See also any to check if one of the value is in the value sequence.

See also :doc:`compare`.

Syntax
------

.. code-block:: javascript

  eq(value_1[, value_i[, ...]])

=============== ============================
Parameter       Description
=============== ============================
``value_i``       The value to be compared to, can be a primitive type or a Value object.
=============== ============================

Examples
--------

.. code-block:: javascript

  $('AVar').eq($('OtherVar'));

Check sequence equality:

.. code-block:: javascript

  $('VAR1').eq('a','b');
