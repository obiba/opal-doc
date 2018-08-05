any
===

Returns true value when the value is equal to any of the parameter, false otherwise. Note that this method will always return false value if the value is null. When applied to a value sequence, it is applied to each of its values and then returns true if at least one of the value verifies the comparison.

See also :doc:`../global/value`.

Syntax
------

.. code-block:: javascript

  any(param_1[, param_i[, ...]])

=============== ============================
Parameter       Description
=============== ============================
``param_i``     A string or a Value to be compared to or a comparison function that takes value argument (makes sense when applied to value sequences).
=============== ============================

Examples
--------

.. code-block:: javascript

  $('CategoricalVar').any('CAT1', 'CAT2')

Usage of a comparison function with the example of a (repeatable) variable representing a sequence of measures:

.. code-block:: javascript

  // check if there is any value greater than 100 in a value sequence
  $('Measures').any(function(value, index) { return value.le(100) })

  // equivalent to
  $('Measures').filter(function(value, index) { return value.le(100) }).empty().not()
