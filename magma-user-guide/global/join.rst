$join
=====

Allows joining a variable value to another variable value that provides a entity identifier. The current object is a value set. $join will access to a variable value within this value set.

See also :doc:`value`.

Syntax
------

.. code-block:: javascript

  $join(name,idname[,flat])

.. list-table::
   :header-rows: 1
   :widths: 10 90

   * - Parameter
     - Description
   * - ``name``
     - The name of the variable from which the value shall be retrieved.
   * - ``idname``
     - The name of the variable from which the entity identifier shall be retrieved.
   * - ``flat``
     - | Specifies that if in case of the join operation result in a value sequence tree, the result should be flatten in a sequence of unique values.
       | Default is false and a value sequence tree will be transformed into a sequence of comma separated stringified values.

Examples
--------

Returns the BRAND_NAME of a medication which is identified by the MEDICATION_ID.

.. code-block:: javascript

  $join('medications.Drugs:BRAND_NAME','MEDICATION_ID')

Given the following datasets, a table with a repeatable variable named **code**:

==== ===============
ID	 code
==== ===============
aa	 Acode1,Acode2
bb	 Acode1
cc	 Acode3
dd
==== ===============

and **code_mapper** a table with a repeatable variable **parent**:

======= ===============
ID	    parent
======= ===============
Acode1	Bcode1,Bcode2
Acode2	Bcode1,Bcode3
Acode3
======= ===============

The following script:

.. code-block:: javascript

  $join('test.code_mapper:parent','code', true)

will return the following value sequences:

==== ===============
D	   flat
==== ===============
aa	 Bcode1,Bcode2,Bcode3
bb	 Bcode1,Bcode2
cc
dd
==== ===============

Without the flat option, the following script:

.. code-block:: javascript

  $join('test.code_mapper:parent','code')

would return the following value sequencies where value sequencies of second order have been stringified:

==== ===============
D	   non-flat
==== ===============
aa	 "Bcode1,Bcode2","Bcode1,Bcode3"
bb	 "Bcode1,Bcode2"
cc
dd
==== ===============
