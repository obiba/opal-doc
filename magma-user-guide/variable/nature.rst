nature
======

Returns the nature of the variable as a Text value. The nature indicates the kind of summary statistics that can be performed on values. Nature values are:

* ``CATEGORICAL``: the values of the variable are discrete and described by the categories of the variable or the value type is ``boolean``,
* ``CONTINUOUS``: values can be any in the considered value type (applies also to variables having categories that are all flagged as being *missing*),
* ``TEMPORAL``: value of type ``date`` or ``datetime``,
* ``GEO``: value of type ``point``, ``linestring`` or ``polygone``,
* ``BINARY``: value of type ``binary``,
* ``UNDETERMINED`` when non of the above apply.

See also :doc:`../global/variable`.

Syntax
------

.. code-block:: javascript

  nature()

Examples
--------

.. code-block:: javascript

  $('VAR1').nature()
