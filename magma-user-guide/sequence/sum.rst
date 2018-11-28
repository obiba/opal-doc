sum
===

Returns the sum of a value sequence. The returned value will have the operands value type (summing an integer sequence produces an integer).

If the sequence isn't a numerical sequence, magma exception is thrown.

If the sequence is empty, 0 is returned. If the sequence is null, null is returned. Each null value of the sequence is turned into 0. This method also accepts a non-sequence value, in which case, it is returned untouched.

See also :doc:`max`, :doc:`min`, :doc:`stddev`, :doc:`avg`, :doc:`reduce`.

Syntax
------

.. code-block:: javascript

  sum()

Examples
--------

.. code-block:: javascript

  $('StandingHeight:Measure.RES_HEIGHT_MEASURE').sum();
