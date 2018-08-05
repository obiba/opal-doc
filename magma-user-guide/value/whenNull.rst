whenNull
========

Returns its argument when the value is null. Using this method may avoid the use of an if/else block. It can be used to ensure that a method chain never returns a null value.

See also :doc:`../global/value`.

Syntax
------

.. code-block:: javascript

  whenNull(someValue)


=============== ============================
Parameter       Description
=============== ============================
``someValue``   The value to return when the original value is null.
=============== ============================


Examples
--------

.. code-block:: javascript

  // the call to any() may result is null. Thus, adding whenNull ensures that the chain never returns null.
  $('MyVar').any('YES').whenNull(false);

  // This complex chain, may result in null for many reasons. Again, adding the whenNull ensures the result is never null.
  $('MyVar').or(
  $('SomeOtherVar').and($('YetAnotherVar'))
  ).whenNull(false);

  // Returns a text Value when null
  $('MyTextVar').whenNull('foo');
  $('MyTextVar').whenNull($('AnotherTextVar'));

  // Returns a integer Value when null
  $('MyIntegerVar').whenNull(999);
  $('MyIntegerVar').whenNull('999');

  // Applies to each value in a value sequence
  $('MyRepeatableVar').whenNull(99);
