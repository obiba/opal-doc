all
===

Returns true when the value contains all specified parameters, false otherwise. Note that this method will always return false if the value is null.

See also :doc:`../global/value`.

Syntax
------

.. code-block:: javascript

  all(param_1[, param_i[, ...]])

=============== ============================
Parameter       Description
=============== ============================
``param_i``     A string or a Value to be compared to.
=============== ============================

Examples
--------

.. code-block:: javascript

  $('CategoricalVar').all('CAT1', 'CAT2')
