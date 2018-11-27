max
===

Returns the maximum value of a value sequence.

If the sequence isn't a numerical sequence, magma exception is thrown.

If the sequence is null or empty, null is returned. Each null value of the sequence is ignored. This method also accepts a non-sequence value, in which case, it is returned untouched.

See also :doc:`min`.

Syntax
------

.. code-block:: javascript

  max()

Examples
--------

.. code-block:: javascript

  $('StandingHeight:Measure.RES_HEIGHT_MEASURE').max();
