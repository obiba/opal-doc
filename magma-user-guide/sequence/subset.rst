subset
======

Filter values of a sequence by subsetting the values according to their position.

See also :doc:`filter`.

Syntax
------

.. code-block:: javascript

  subset(from[,to])

=============== ============================
Parameter       Description
=============== ============================
``from``        0-based index (inclusive) from which value should be included.
``to``          Optional 0-based index (exclusive) to which value should be included
=============== ============================

Examples
--------

Subset sequence values from a position and its equivalent filter:

.. code-block:: javascript

  $('SequenceVar').subset(1)

  // is equivalent to the filter:
  $('SequenceVar').filter(function(value,index) {
    return index>=1;
  })

Subset sequence values in a position range and its equivalent filter:

.. code-block:: javascript

  $('SequenceVar').subset(1,4)

  // is equivalent to the filter:
  $('SequenceVar').filter(function(value,index) {
    return index>=1 && index<4;
  })
