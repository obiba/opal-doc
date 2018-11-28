trimmer
=======

Filter values of a sequence by removing null values.

See also :doc:`filter`, :doc:`subset`.

Syntax
------

.. code-block:: javascript

  trimmer()

Examples
--------

Trim sequence values and its equivalent filter:

.. code-block:: javascript

  $('SequenceVar').trimmer()

  // is equivalent to the filter:
  $('SequenceVar').filter(function(value) {
    return value.isNull().not();
  })
