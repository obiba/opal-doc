filter
======

Filter values of a sequence using a custom javascript predicating function.

See also :doc:`subset`, :doc:`map`, :doc:`reduce`.

Syntax
------

.. code-block:: javascript

  filter(predicate)

=============== ============================
Parameter       Description
=============== ============================
``predicate``   Predicating javascript function called for each value (with arguments: value and index of the value in the sequence) and that returns a boolean value (true if value is to be kept).
=============== ============================

Examples
--------

Filter sequence values being greater than a given value:

.. code-block:: javascript

  $('SequenceVar').filter(function(value) {
    return value.ge(100);
  })

Filter sequence values based on value position in the sequence:

.. code-block:: javascript

  $('SequenceVar').filter(function(value,index) {
    return value.ge(100).value() && index<3;
  })

Filter sequence based on another variable (in the same occurrence group) value at the same position:

.. code-block:: javascript

  var timepoint = $('TimePoint')
  $('Measure').filter(function(value,index) {
    return timepoint.valueAt(index).isNull().not();
  })
