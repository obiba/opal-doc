reduce
======

Reduce values of a sequence to a single value using a custom javascript accumulating function. The reduction result is the last accumulated value.

See also :doc:`../value/map`.

Syntax
------

.. code-block:: javascript

  reduce(accumulator[,initialValue])

.. list-table::
  :widths: 10 90

  * - Parameter
    - Description
  * - ``accumulator``
    - | Accumulating javascript function called for each value (with arguments: accumulated value, value and index of the value in the sequence)
      | and that returns the new accumulated value. Note that if the accumulated value resulting of the function call is null, it is not applied to the final reduction result.
  * - ``initialValue``
    - | Optional value to be used to initialize the accumulated value. If not provided, the accumulated value will be initialized with
      | the first not null value of the sequence (thus in this case the accumulating function is not called during this initialization phase).

Examples
--------

Reduce as sequence of measures to their sum:

.. code-block:: javascript

  $('Words').reduce(function(acc, value, index) {
    return acc.plus(value);
  })

Reduce a sequence of measures to their average value initialized to 0:

.. code-block:: javascript

  $('SequenceVar').reduce(function(acc, value, index) {
    return acc.multiply(index).plus(value).div(index+1);
  }, 0)
