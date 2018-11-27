valueAt
=======

Returns the value at a specified index within the sequence (0-based).

See also :doc:`first`, :doc:`last`.

Syntax
------

.. code-block:: javascript

  valueAt(index)

=============== ============================
Parameter       Description
=============== ============================
``index``       The 0-based index of the value to be retrieved from the sequence.
=============== ============================

Examples
--------

.. code-block:: javascript

  $('Admin.StageInstance.stage').valueAt(4)

When a view refers to several tables and a variable with same name exists in these tables, the resulting value is a sequence (see :doc:`../global/value` method). The order of the values in this sequence is the same as the order of the tables in the view. Then ``valueAt`` can be used to pick the value of a specific table.

.. code-block:: javascript

  // variable VAR is defined in tables T1 and T2 referred by the view
  // getting the value of table T2 by position
  $('VAR').valueAt(1)
  // is equivalent to fully qualifying the variable
  $('project.T2.VAR')
