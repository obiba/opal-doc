Magma JS Methods
================

.. toctree::
   :maxdepth: 1

   global/index
   variable/index
   value/index
   sequence/index
   bool/index
   numeric/index
   text/index
   date/index
   geo/index
   unit/index


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
:doc:`value/all`        Returns true when the value contains all specified parameters, false otherwise.
:doc:`value/any`        Returns true value when the value is equal to any of the parameter, false otherwise.
:doc:`value/isNull`     Returns true if the value is null.
:doc:`value/whenNull`   Returns its argument if the value is null. This method may allow avoiding an if/else block.
:doc:`value/map`        Uses a lookup table to map the a value to another (which may be computed or derived).
:doc:`value/not`        Returns the contrary of a boolean value or return if it does not match any of the arguments.
:doc:`value/type`       Returns or changes the value's type.
:doc:`value/value`      Returns the javascript value from the value object.
:doc:`value/length`     Returns the length of the value.
======================= ===========================================================

**Value Sequence Methods**


============================ ===========================================================
Methods                      Description
============================ ===========================================================
:doc:`value/any`             Returns true value if of the provided values can be found in the value sequence.
:doc:`sequence/empty`        Returns true value if is operating on a sequence that contains zero values.
:doc:`sequence/first`        Returns the first value in a value sequence.
:doc:`sequence/firstNotNull` Returns the first not null value in a value sequence.
:doc:`sequence/indexOf`      Returns the first position of a value in a value sequence.
:doc:`sequence/last`         Returns the last value in a value sequence.
:doc:`sequence/lastIndexOf`  Returns the last position of a value in a value sequence.
:doc:`sequence/valueAt`      Returns the value at a specified index within the sequence (0-based).
:doc:`sequence/size`         Returns the number of values within a sequence.
:doc:`value/map`             Map each value in the sequence to another value.
:doc:`sequence/reduce`       Returns the reduction of the values within a sequence.
:doc:`sequence/filter`       Returns a sequence which values have been filtered using custom javascript predicating function.
:doc:`sequence/subset`       Returns a subset of a sequence according to provided begin and end positions.
:doc:`sequence/trimmer`      Returns a sequence without null values.
:doc:`sequence/sort`         Sorts a sequence in natural order of its values or using a custom javascript comparing function.
:doc:`sequence/max`          Returns the maximum value of a value sequence.
:doc:`sequence/min`          Returns the minimum value of a value sequence.
:doc:`sequence/avg`          Returns the average of a value sequence.
:doc:`sequence/sum`          Returns the sum of a value sequence.
:doc:`sequence/stddev`       Returns the standard deviation of a value sequence.
:doc:`sequence/push`         Adds one or more values after a value to produce a value sequence (deprecated in favor of append).
:doc:`sequence/append`       Adds one or more values after a value to produce a value sequence.
:doc:`sequence/prepend`      Adds one or more values before a value to produce a value sequence.
:doc:`sequence/insertAt`     Inserts one or more values at a given position to produce a value sequence.
:doc:`sequence/join`         Joins the text representation of the values in the sequence.
:doc:`sequence/zip`          Returns a sequence of values, where each value is the transformation of a tuple of values, the i-th tuple contains the i-th element from each of the argument sequences.
:doc:`sequence/asSequence`   Turns a value object into a value sequence object.
:doc:`sequence/isSequence`   Returns whether the value is a value sequence object.
============================ ===========================================================

**Boolean Value Methods**

======================= ===========================================================
Methods                 Description
======================= ===========================================================
:doc:`bool/and`         Applies the `ternary and logic <http://en.wikipedia.org/wiki/Ternary_logic>`_ on values.
:doc:`bool/compare`     Returns 0 if the value represents the same boolean value as the argument; a positive integer if the value represents ``true`` and the argument represents ``false``; and a negative integer if this value represents ``false`` and the argument represents ``true``.
:doc:`bool/eq`          Returns if left operand value is equal to right operand value.
:doc:`bool/not`         Returns the contrary of a boolean value or return if it does not match any of the arguments.
:doc:`bool/or`          Applies the `ternary and logic <http://en.wikipedia.org/wiki/Ternary_logic>`_ on values.
======================= ===========================================================

**Numeric Value Methods**

======================= ===========================================================
Methods                 Description
======================= ===========================================================
:doc:`numeric/compare`  Returns a negative integer, zero, or a positive integer as the value is less than, equal to, or greater than the value argument.
:doc:`numeric/eq`       Returns if left operand value is equal to right operand value.
:doc:`numeric/ge`       Returns if left operand value is greater equal than right operand value.
:doc:`numeric/gt`       Returns if left operand value is greater than right operand value.
:doc:`numeric/le`       Returns if left operand value is lower equal than right operand value.
:doc:`numeric/lt`       Returns if left operand value is lower than right operand value.
:doc:`numeric/plus`     Returns result of first operand value plus second operand value.
:doc:`numeric/minus`    Returns result of first operand value minus second operand value.
:doc:`numeric/multiply` Returns result of first operand value multiply second operand value.
:doc:`numeric/div`      Returns result of first operand value divided by second operand value.
:doc:`numeric/ln`       Returns the natural logarithm (base e) of the value.
:doc:`numeric/log`      Returns the base-10 logarithm of the value.
:doc:`numeric/abs`      Returns the absolute value.
:doc:`numeric/pow`      Returns the value raised to the power of the operand.
:doc:`numeric/sqroot`   Returns square root of the value.
:doc:`numeric/cbroot`   Returns cubic root of the value.
:doc:`numeric/root`     Returns arbitrary root of the value.
:doc:`numeric/round`	  Returns the rounded value.
:doc:`numeric/group`    Group values in a ranges.
======================= ===========================================================

**Text Value Methods**

========================= ===========================================================
Methods                   Description
========================= ===========================================================
:doc:`text/compare`       Returns a negative integer, zero, or a positive integer as the text value is less than, equal to, or greater than the text value argument.
:doc:`text/compareNoCase` Returns a negative integer, zero, or a positive integer as the text value is less than, equal to, or greater than the text value argument ignoring case.
:doc:`text/concat`        Returns the text type result of first operand concat second operand.
:doc:`text/date`          Returns a value of date type given a date format pattern.
:doc:`text/datetime`      Returns a value of datetime type given a date time format pattern.
:doc:`text/eq`            Returns if left operand value is equal to right operand value.
:doc:`text/matches`       Used to match a regular expression against a string.
:doc:`text/replace`       Used to find a match between a regular expression and a string, and to replace the matched substring with a new substring.
:doc:`text/trim`          Returns a copy of the string, with leading and trailing whitespace omitted.
:doc:`text/lowerCase`     Returns a copy of the string, lower case.
:doc:`text/upperCase`     Returns a copy of the string, upper case.
:doc:`text/capitalize`    Returns a copy of the string, with first character of each word capitalized.
========================= ===========================================================

**Date and Datetime Value Methods**

======================= ===========================================================
Methods                 Description
======================= ===========================================================
:doc:`date/add`         Adds days to a value of date time type.
:doc:`date/after`       Returns true if the date value is after the specified date value(s).
:doc:`date/before`      Returns true if the date value is before the specified date value(s).
:doc:`date/dayOfMonth`  Returns the day of month from a date as an integer starting from 1.
:doc:`date/dayOfWeek`   Returns the day of week from a date as an integer starting from 1 (Sunday).
:doc:`date/dayOfYear`   Returns the day of year from a date as an integer starting from 1.
:doc:`date/format`      Returns the text representation of the date formatted by the provided pattern.
:doc:`date/hour`        Returns the hour of the day for the 12-hour clock (0 - 11).
:doc:`date/hourOfDay`   Returns the hour of the day for the 24-hour clock.
:doc:`date/minute`      Returns the minute within the hour.
:doc:`date/millisecond` Returns the millisecond within the second.
:doc:`date/month`       Returns the month of a date as an integer starting from 0 (January).
:doc:`date/quarter`     Returns the quarter of a date as an integer starting from 0 (Q1).
:doc:`date/second`      Returns the second within the minute.
:doc:`date/semester`    Returns the semester of a date as an integer starting from 0 (S1).
:doc:`date/time`        Returns the number of milliseconds since January 1, 1970, 00:00:00 GMT (epoch time).
:doc:`date/weekday`     Returns a boolean value indicating whether the date denotes a weekday (between Monday and Friday inclusively).
:doc:`date/weekend`     Returns a boolean value indicating whether the date denotes a weekend (either Sunday or Saturday).
:doc:`date/weekOfMonth` Returns the week of month from a date as an integer starting from 1.
:doc:`date/weekOfYear`  Returns the week of year from a date as an integer starting from 1.
:doc:`date/year`        Returns the year value.
======================= ===========================================================

**Geo Value Methods**

======================= ===========================================================
Methods                 Description
======================= ===========================================================
:doc:`geo/latitude`     Get the latitude of a point value.
:doc:`geo/longitude`    Get the longitude of a point value.
======================= ===========================================================

**Measurement Unit Methods**

======================= ===========================================================
Methods                 Description
======================= ===========================================================
:doc:`unit/unit`        Sets the measurement unit of the current value to the specified unit. Returns the current unit when no argument is supplied.
:doc:`unit/toUnit`      Measurement unit conversion: converts the current value into a different measurement unit.
======================= ===========================================================
