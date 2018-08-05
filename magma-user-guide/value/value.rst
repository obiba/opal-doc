value
=====

Returns the primitive javascript value from the Value.

See also :doc:`../global/value`.

Syntax
------

.. code-block:: javascript

  value()

Examples
--------

In a if-else statement:

.. code-block:: javascript

  if($('Admin.Interview.exportLog.destination').empty().value()) {
    // true
  } else {
    // false
  }

With Geo value types, value() returns arrays of decimals:

.. code-block:: javascript

  // Point as a array of decimals: longitude and latitude
  $('Point').value()
  // Point longitude
  $('Point').value()[0]
  // Point latitude
  $('Point').value()[1]

  // LineString as a array of points (i.e. array of array of decimals)
  $('LineString').value()
  // Latitude of the first point in the line
  $('LineString').value()[0][1]

  // Polygon as a array of lines (i.e. array of array of array of decimals)
  $('Polygon').value()
  // Number of lines in the polygon
  $('Polygon').value().length
  // Number of points in the first line of the polygon
  $('Polygon').value()[0].length
  // First point of the first line (array of decimals: longitude and latitude)
  $('Polygon').value()[0][0]
