min
===

Returns the minimum value of a value sequence.

If the sequence isn't a numerical sequence, magma exception is thrown.

If the sequence is null or empty, null is returned. Each null value of the sequence is ignored. This method also accepts a non-sequence value, in which case, it is returned untouched.

See also :doc:`max`.

Syntax
------

.. code-block:: javascript

  min()

Examples
--------

.. code-block:: javascript

  $('StandingHeight:Measure.RES_HEIGHT_MEASURE').min();
