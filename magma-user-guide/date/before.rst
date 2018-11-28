before
======

Returns true if the date value is before the specified date value(s).

See also :doc:`after`.

Syntax
------

.. code-block:: javascript

  before(date_1[, date_2[, ...]])

=============== ============================
Parameter       Description
=============== ============================
``date_i``      The dates to be compared to.
=============== ============================

Examples
--------

Before one date:

.. code-block:: javascript

  $('Date').before($('OtherDate'))
  // string representation of dates are supported as well
  $('Date').before('2017-01-15')

Before several dates:

.. code-block:: javascript

  $('Date').before($('OtherDate'), $('SomeOtherDate'))
