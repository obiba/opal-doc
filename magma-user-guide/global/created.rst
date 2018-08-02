$created
========

The current object is a value set. $created will access to the creation timestamp within this value set. The creation timestamp is the date time when the values for a given participant were imported into opal.

See also :doc:`lastupdate`.

Syntax
------

.. code-block:: javascript

  $created()

Examples
--------

Check if a value set was created after a given date time.

.. code-block:: javascript

  $created().after(newValue('2014-05-05 10:30', 'datetime'))
