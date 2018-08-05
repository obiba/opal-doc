Magma JS Methods
================

.. toctree::
   :maxdepth: 1

   global/index
   variable/index
   sequence/index


**Global Methods**

========================= ===========================================================
Methods                   Description
========================= ===========================================================
:doc:`global/value`       Return the variable value within the current value set.
:doc:`global/this`        Return the variable value within the current view value set.
:doc:`global/join`        Return the joined variable value referenced by a variable value within the current value set.
:doc:`global/group`       Return a map of variable values in the same group of occurrence within the current value set.
:doc:`global/id`          Return the entity identifier within the current value set.
:doc:`global/variable`    Returns the variable object at the given name.
:doc:`global/log`         Provides 'info' level logging of messages and variable values.
:doc:`global/now`         Returns the current date time wrapped in a value object.
:doc:`global/newValue`    Creates a new value.
:doc:`global/newSequence` Creates a new value sequence.
:doc:`global/created`     Return the value set creation time.
:doc:`global/lastupdate`  Return the value set last update time.
:doc:`global/source`      Load a javascript file.
========================= ===========================================================

**Variable Methods**

=============================== ===========================================================
Methods                         Description
=============================== ===========================================================
:doc:`variable/attribute`       Get the variable attribute value with the given name.
:doc:`variable/name`            Get the name of the variable as a Text value.
:doc:`variable/type`            Returns the value type of the variable, as a Text value.
:doc:`variable/entityType`      Returns the entity type of the variable, as a Text value.
:doc:`variable/refEntityType`   Returns the referenced entity type of the variable, as a Text value.
:doc:`variable/repeatable`      Returns if the variable is repeatable, as a Boolean value.
:doc:`variable/occurrenceGroup` Returns the occurrence group of the variable, as a Text value.
:doc:`variable/mimeType`        Returns the mime type of the variable, as a Text value.
:doc:`variable/unit`            Returns the unit of the variable, as a Text value.
:doc:`variable/nature`	        Returns the nature of the variable (``CATEGORICAL``, ``CONTINUOUS``, etc.), as a Text value.
:doc:`variable/isNumeric`	      Returns whether the variable value type is ``integer`` or ``decimal``, as a Boolean value.
:doc:`variable/isDateTime`	    Returns whether the variable value type is ``date`` or ``datetime``, as a Boolean value.
:doc:`variable/isGeo`	          Returns whether the variable value type is ``point``, ``linestring`` or ``polygon``, as a Boolean value.
=============================== ===========================================================

**Value Methods**

======================= ===========================================================
Methods                 Description
======================= ===========================================================
======================= ===========================================================

**Value Sequence Methods**


============================ ===========================================================
Methods                      Description
============================ ===========================================================
:doc:`sequence/firstNotNull` Returns the first not null value in a value sequence.
:doc:`sequence/asSequence`   Turns a value object into a value sequence object.
============================ ===========================================================

**Boolean Value Methods**

======================= ===========================================================
Methods                 Description
======================= ===========================================================
======================= ===========================================================

**Numeric Value Methods**

======================= ===========================================================
Methods                 Description
======================= ===========================================================
======================= ===========================================================

**Measurement Unit Methods**

======================= ===========================================================
Methods                 Description
======================= ===========================================================
======================= ===========================================================

**Text Value Methods**

======================= ===========================================================
Methods                 Description
======================= ===========================================================
======================= ===========================================================

**Date and Datetime Value Methods**

======================= ===========================================================
Methods                 Description
======================= ===========================================================
======================= ===========================================================

**Geo Value Methods**

======================= ===========================================================
Methods                 Description
======================= ===========================================================
======================= ===========================================================
