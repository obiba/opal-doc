zip
===

Returns a sequence of values, where each value is the transformation of a tuple of values. The i-th tuple contains the i-th element from each of the argument sequences. The returned list length is the length of the longest argument sequence (shortest argument sequence values are null). Not sequential arguments have their value repeated in each tuple.

See also :doc:`join`.

Syntax
------

.. code-block:: javascript

  zip(value_1[, value_2[, ...]]], function)

=============== ============================
Parameter       Description
=============== ============================
``value``       The value(s) to be zipped to.
``function``    The transformation function to be applied to each tuple of values.
=============== ============================

Examples
--------

Zip the value sequences:

* [A,B,C]
* [1,2,3]
* [X,Y]

And concatenate the string representation of the values for each tuples.

.. code-block:: javascript

  // returns the text values sequence ["A: 1X","B: 2Y","C: 3null"]
  $('SequenceVarABC').zip($('SequenceVar123'),$('SequenceVarXY'),function(o1, o2, o3) {
      return o1.concat(': ', o2, o3);
    });

Increment each values of a sequence of integers: [1,2,3]

.. code-block:: javascript

  // returns the integer values sequence [2,3,4]
  $('SequenceVar123').zip(1,function(o1, o2) {
      return o1.plus(o2);
    });
