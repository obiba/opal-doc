not
===

Returns the contrary of a boolean value or return if it does not match any of the arguments.

See also :doc:`and`, :doc:`or`.

Syntax
------

.. code-block:: javascript

  not([value_1[, value_i[, ...]]])

=============== ============================
Parameter       Description
=============== ============================
``value``       The optional boolean value(s) or string to be compared to.
=============== ============================

Examples
--------

Get the contrary of a Boolean value:

.. code-block:: javascript

  $('BooleanVar').not()
  $('CategoricalVar').any('CAT1').not()

Check if a value is not any of the specified strings:

.. code-block:: javascript

  $('CategoricalVar').not('CAT1', 'CAT2')

Check if a value is not any of the specified values:

.. code-block:: javascript

  $('CategoricalVar').not($('OtherCategoricalVar'))
