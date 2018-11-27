compare
=======

When comparing Boolean values: returns 0 if the value represents the same boolean value as the argument; a positive integer if the value represents true and the argument represents false; and a negative integer if this value represents false and the argument represents true.

When comparing Numeric values (i.e. integer and/or decimal types) or Text values: returns a negative integer, zero, or a positive integer as the value is less than, equal to, or greater than the value argument.

See also :doc:`eq`.

Syntax
------

.. code-block:: javascript

  compare(value)

=============== ============================
Parameter       Description
=============== ============================
``value``       The value to be compared to.
=============== ============================

Examples
--------

.. code-block:: javascript

  $('AVar').compare($('OtherVar'));
