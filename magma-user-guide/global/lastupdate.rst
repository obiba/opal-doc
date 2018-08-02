$lastupdate
===========

The current object is a value set. $lastupdate will access to the last update timestamp within this value set. The last update timestamp is the date time when the values for a given participant were updated in opal. It usually close to the creation date time unless the values were overridden.

See also :doc:`created`.

Syntax
------

.. code-block:: javascript

  $lastupdate()

Examples
--------

Check if a value set was created after a given date time.

.. code-block:: javascript

  // compare to a date
  $lastupdate().after(newValue('2014-05-05', 'date'))

  // compare to a datetime (ISO 8601 format)
  $lastupdate().after(newValue('2015-02-18T11:56:27.280-0500', 'datetime'))
