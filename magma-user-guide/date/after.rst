after
=====

Returns true if the date value is after the specified date value(s).

See also :doc:`before`.

Syntax
------

.. code-block:: javascript

  after(date_1[, date_2[, ...]])

=============== ============================
Parameter       Description
=============== ============================
``date_i``      The dates to be compared to.
=============== ============================

Examples
--------

After one date:

.. code-block:: javascript

  $('Date').after($('OtherDate'))
  // string representation of dates are supported as well
  $('Date').after('2017-01-15')

After several dates:

.. code-block:: javascript

  $('Date').after($('OtherDate'), $('SomeOtherDate'))
