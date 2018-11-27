sort
====

Sorts a sequence in natural order of its values or using a custom javascript comparing function.

See also :doc:`first`, :doc:`last`.

Syntax
------

.. code-block:: javascript

  sort([function])

=============== ============================
Parameter       Description
=============== ============================
``function``    Optional javascript comparing function.
=============== ============================

Examples
--------

.. code-block:: javascript

  $('Admin.StageInstance.stage').sort().first().any('MyStage')

Sorts a sequence of Datetime values according to their "dayOfYear" value:

.. code-block:: javascript

  $('Admin.Action.dateTime').sort(function(first, second) {
    // Custom sort method is expected to return a number
    return first.dayOfYear().value() - second.dayOfYear().value();
  })
