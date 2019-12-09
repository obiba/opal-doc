median
======

Returns the median value from a value sequence. The returned value will have the decimal value type.

If the sequence is empty or null, null is returned. All the null values of the sequence are excluded from the calculation. This method also accepts a non-sequence value, in which case, it is returned untouched.

See also :doc:`max`, :doc:`min`, :doc:`stddev`, :doc:`avg`, :doc:`reduce`.

Syntax
------

.. code-block:: javascript

  median()

Examples
--------

.. code-block:: javascript

  $('StandingHeight:Measure.RES_HEIGHT_MEASURE').median();
