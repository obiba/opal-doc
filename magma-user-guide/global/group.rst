$group
======

The current object is a value set. $group will access to variable values within this value set. This method will map the values of the variables in the same occurrence group. The group of values considered in the value sequence is the first group matching the provided criteria.

See also :doc:`value`, :doc:`id`, :doc:`join`, :doc:`variable`

Syntax
------

.. code-block:: javascript

  $group(name,criteria[,select])


.. list-table::
   :header-rows: 1
   :widths: 10 90

   * - Parameter
     - Description
   * - ``name``
     - The name of the variable on which the selection criteria is to be applied.
   * - ``criteria``
     - Value to be compared to or a function for evaluating the matching criteria.
   * - ``select``
     - | Name of the variable from which the value shall be retrieved. This parameter is optional. If not provided a mapping of values for each variables
       | of the same occurrence group is returned (affects script execution performance if useless data are extracted).

Examples
--------

In the following example StageName, StageDuration, StageOperator are repeatable variables in the same occurrence group.
For a value set, the corresponding value sequences could be as follow:

============= ============= ===============
StageName     StageDuration StageOperator
============= ============= ===============
Consent       123           roger
Questionnaire 234           michelle
Weight        23            jack
============= ============= ===============

$group allows to extract a value of a variable given a matching criteria on a variable value in the same occurrence group:

.. code-block:: javascript

  // Returns 234
  $group('StageName','Questionnaire', 'StageDuration')

  // Returns 'michelle'
  $group('StageName','Questionnaire','StageOperator')

  // Returns 234 as well but extracts also values for the 'StageOperator' variable
  $group('StageName','Questionnaire')['StageDuration']

  // Criteria can also be expressed using a function.
  // Returns 'jack'
  $group('StageDuration', function(value) {
          return value.le(100);
        },'StageOperator')

$group handles value sequences. If multiple occurrences match the criteria, the value that is returned is a value sequence.

============= ============= ===============
StageName     ActionType    ActionComment
============= ============= ===============
Consent       START
Consent       COMPLETE
Questionnaire START
Questionnaire INTERRUPT     Participant needs a rest
Questionnaire RESUME        Participant still looks tired
Questionnaire COMPLETE      Answers cannot be trusted
============= ============= ===============

.. code-block:: javascript

  // Returns the value sequence: '','Participant needs a rest','Participant still looks tired','Answers cannot be trusted'
  $group('StageName','Questionnaire','ActionComment')

  // Returns the value: 'Participant needs a rest'
  $group('ActionType','INTERRUPT','ActionComment')

  // Use asSequence() to ensure consistency with values returned for other participants (if multiple actions are of type 'INTERRUPT' in this example).
  // Returns a value sequence with one item: 'Participant needs a rest'
  $group('ActionType','INTERRUPT','ActionComment').asSequence()
