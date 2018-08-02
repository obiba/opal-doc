$, $val, $value
===============

The current object is a value set. $ will access to a variable value within this value set.

Note that when joining several tables in a view and when the named variable is present in more than one of these tables, the value returned is a value sequence. Values of this sequence appear in the order of the tables defined in the view. For more details see also the presentation about `multilines <http://slides.com/yannickmarcon/opal-multilines>`_ support. If the values of the sequence are known to be identical (because the same data is repeated in several tables), it is possible to use the firstNotNull method to reduce the sequence to one value.

Note also that if a script returns a value sequence and if the derived variable is not "repeatable", the value sequence is automatically reduced with the :doc:`../sequence/firstNotNull` strategy.

See also :doc:`group`, :doc:`id`, :doc:`join`, :doc:`this`, :doc:`variable`.

Syntax
------

.. code-block:: javascript

  $(name)
  // alternate syntax
  $val(name)
  $value(name)

.. list-table::
   :header-rows: 1
   :widths: 10 90

   * - Parameter
     - Description
   * - ``name``
     - | The name of the variable from which the value shall be retrieved. If the name is fully qualified, ie. "<datasource>.<table>:<variable>", the lookup will be first done in
       | view's reference tables and if not found will be looked up out of the view's scope.

Examples
--------

Returns the value for current value set and the named variable DO_YOU_SMOKE.

.. code-block:: javascript

  $('DO_YOU_SMOKE')

Returns the value for the current entity from the fully qualified table.

.. code-block:: javascript

  $('project.table:SMOKING')

When using a fully qualifying the variable, if the variable is not a variable from the tables referred by the view, the performance could be very poor as it would result in one request on an individual value in the database.
