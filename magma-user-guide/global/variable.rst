$var, $variable
===============

Returns the variable object at the given name. The name resolution is done given an execution context.

See also :doc:`value`, :doc:`id`.

Syntax
------

.. code-block:: javascript
  
  $var(name)
  // alternate syntax
  $variable(name)

=============== ============================
Parameter       Description
=============== ============================
``name``        The name that identifies the variable.
=============== ============================

Examples
--------

Get the variable with name DO_YOU_SMOKE.

.. code-block:: javascript

  $var('DO_YOU_SMOKE')
