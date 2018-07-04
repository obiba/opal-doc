Search Variables
================

Search for variables using facets and full-text query.

Controlled Vocabularies
-----------------------

The controlled vocabularies are the ones defined by the taxonomies and the variable properties. Once a vocabulary term has been selected, it will be used for filtering the variables. Given such a criterion different filters can be selected:


.. list-table::
   :widths: 30 70
   :header-rows: 1

   * - Operation
     - Description
   * - Any
     - The variable field can have any non null value.
   * - None
     - The variable field must be missing.
   * - In
     - The variable field must be in at least one of the selected predefined values
   * - Like
     - The variable field must match a query string (with wildcard support)
   * - Not in
     - The negation of In.
   * - Not like
     - The negation of Like.

**Taxonomies**

See Taxonomies Administration documentation. As the number of vocabulary terms can be very large, the interface allows to search for these terms (name, label, description) by providing keywords. These keywords can be negated, for instance ``alcohol -constructs`` will look up taxonomy terms containing the word alcohol AND NOT containing the word constructs in its name/label/description (or in the name/label/description of the associated vocabulary).

**Properties**

The variable properties that can be used are:

========================= =====================
Property                  Description
========================= =====================
``project``               The project the variable belongs to
``table``                 The table the variable belongs to
``name``                  The name of the variable.
``entityType``            The type of the entity: Participant, Sample etc.
``valueType``	            The type of the variable values: text, integer, decimal etc.
``nature``	              Nature of the variable: categorical, numerical, logical etc.
``repeatable``	          A variable is repeatable when it can have several values for one entity.
``occurrenceGroup``	      When a repeatable variable is in the same group of occurrence as other repeatable variables
``referencedEntityType``	When the values of the variable is an identifier, this property specifies what is the type of the referred entity.
``mimeType``	            The mime type of the data.
``unit``	                The measure unit.
``script``	              The variable attribute that holds the derivation script.
========================= =====================

The property lookup will be done on the property name or on its possible values. For instance ``nature`` will propose to choose among all the variable nature values (categorical, numerical etc.). Whereas typing ``categorical`` will propose the categorical nature only.

Full-text Search
----------------

The full-text search applies to:

* the variable name,
* the variable label(s) in any language.

Wildcard can be used.

Advanced Search
---------------

The advanced search option allows to define your own query. See `Elasticsearch Query Syntax <https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl-query-string-query.html#query-string-syntax>`_ for detailed explanation. We recommend to use the controlled vocabulary first to get the corresponding field names that are not necessarily obvious and then combine criteria at will by using AND, OR and NOT conjunction words.

Results
-------

The resulting variables are presented as a list. To make this list useful it is possible to select some variables and add them to the global Cart. Once in the cart the variables, that could be the result of several search, can be used to search for entities or make a view from them, etc.
