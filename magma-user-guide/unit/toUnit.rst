toUnit
======
Converts the current value with a measurment unit to another measurement unit. For example, this method can convert the value 1kg to 2.2lb or 1000g.

See also :doc:`unit`.

Syntax
------

.. code-block:: javascript

  toUnit(newUnit)

=============== ============================
Parameter       Description
=============== ============================
``newUnit``     The new measurement unit (must be a string).
=============== ============================

Examples
--------

Converts the value from meters to centimeters:

.. code-block:: javascript

  $('HEIGHT').unit('m').toUnit('cm')

Converts the value from its current unit to centimeters (the current unit is take from the unit property of the HEIGHT variable):

.. code-block:: javascript

  $('HEIGHT').toUnit('cm')
