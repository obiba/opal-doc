Querying for Variables
======================

The data dictionary (i.e. the variables) can be searched for. Each variable properties, Categories and Attributes are indexed in Opal's search engine. Each time a table is updated, its data dictionary is automatically re-indexed, ensuring an up-to-date variable search service.

Note that variables of a table are always indexed (with a latency of 1 minute), whereas the indexing of the table values can be scheduled.

How to Search
-------------

When navigating in the data dictionary (datasources, tables, variables), the search box is pre-filled with the current context (datasource or table currently visited). Start typing a word that is looked for and the 10 first most relevant variables will be suggested. Selecting one of them will display it.

By default the fields that are searched for are:

* ``name``
* ``label`` attribute (any language)
* ``description`` attribute (any language)
* ``maelstrom`` attributes (any language)

Other fields can be searched for by explicitly defining a term using the pattern ``<field>``:``<value>``. The search terms can be combined using logical operators ``AND`` and ``OR`` (uppercase is required for the operator). The default logical operator is ``AND``. Wildcard character ``*`` can be used on the values.

Search Fields
~~~~~~~~~~~~~

The search fields corresponding to the variable properties are:

* ``datasource``
* ``table``
* ``name``
* ``fullName``
* ``entityType``
* ``valueType``
* ``occurrenceGroup``
* ``repeatable``
* ``unit``
* ``mimeType``
* ``referencedEntityType``
* ``category``
* ``nature``

The search fields corresponding to the variable Attributes are defined by the pattern: ``<namespace>-<name>-<locale>`` (``namespace`` and ``locale`` are not always defined).

Categories atttributes follow the same pattern, prefixed by ``<category>-<namespace>-<name>-<locale>``.

The nature of the variables can be: CATEGORICAL, CONTINUOUS, TEMPORAL or UNDETERMINED.

Examples
~~~~~~~~

Search for variables having words starting with "smok" (for instance "smoke", "smoked", "smoking" (case insensitive)) in their name or label or description:

::

  smok

You can provide a more accurate query by specifying the field name that is searched:
::

  name:Measure.RES_FVC

Criteria can be combined:
::

  Measure.RES_ valueType:binary

Default operator is AND, but OR and NOT operators with parenthesis can also be specified:
::

  RES_F AND NOT (FEV OR FEF)

Search for variables of numerical value type (``integer`` or ``decimal``):
::

  valueType:integer OR valueType:decimal

Search for variables with repeatable values in kilograms:
::

  unit:kg repeatable:true

Search for variables having category with name starting with ``Y``:
::

  category:Y*

Search for a chunk of phrase in English ``label`` attribute:
::

  label-en:"don't know"

Search for variables having a category with some words in their English ``label``:
::

  category-label-en:yes
