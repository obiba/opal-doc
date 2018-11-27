stddev
======

Returns the standard deviation of a value sequence.

If the sequence isn't a numerical sequence, magma exception is thrown.

If the sequence is empty, 0 is returned. If the sequence is null, null is returned. Each null value of the sequence is turned into 0. This method also accepts a non-sequence value, in which case, it is returned untouched.

See also :doc:`max`, :doc:`min`, :doc:`sum`, :doc:`avg`, :doc:`reduce`.

Syntax
------

.. code-block:: javascript

  stddev()

Examples
--------

.. code-block:: javascript

  $('StandingHeight:Measure.RES_HEIGHT_MEASURE').stddev();
