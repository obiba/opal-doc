$this
=====

The current object is a value set in a view. $this will access to a variable value within this value set.

See also :doc:`value`, :doc:`group`, :doc:`id`, :doc:`join`, :doc:`variable`

Syntax
------

.. code-block:: javascript

  $this(name)

=============== ============================
Parameter       Description
=============== ============================
``name``        The name of the variable in the current view from which the value shall be retrieved.
=============== ============================

Examples
--------

Returns the value for current value set and the named variable DERIVED_VAR.

.. code-block:: javascript

  // Get the value of the DERIVED_VAR, which is a variable defined in the view
  $this('DERIVED_VAR')

  // $this is equivalent but much faster than the explicit variable definition
  $('my_datasource.my_view:DERIVED_VAR')
