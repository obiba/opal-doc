Variables and Data
==================

The variables are organized in an abstract way, independently of the way they are persisted.

The following diagram presents a 'traditional' view of what is a table:

* the 'columns' are the variables,
* the 'rows' are the value sets for each entity,
* the 'cells' are the variable entity values.

.. image:: images/magma-table.png

The following diagram shows the relationships between the different concepts:

.. image:: images/magma.png

Variables
---------

Variables and Categories
~~~~~~~~~~~~~~~~~~~~~~~~

A variable describes a set of values. The values of a variable are all of the same type. Possible value types are:

* integer
* decimal
* text
* binary
* locale
* boolean
* datetime
* date
* point
* linestring
* polygon

A variable is about an entity, i.e. all the values for a variable are from the same entity type. Possible entity types are:

* Participant
* Instrument
* ...

A category describe some of the possible values of a variable. A category is associated to one and only one variable.

Datasources and Tables
~~~~~~~~~~~~~~~~~~~~~~

A variable is in one and only one table.

A table has several variables and is in one and only one datasource.

A datasource has several tables. A datasource is not a database: it can be persisted in a database, using different schema. It can also be persisted in a file in xml or Excel formats. It is important to understand that Opal separates the formal description of the variables from the way they are persisted. This gives to Opal a lot of versatility.

Attributes
~~~~~~~~~~

Datasources, variables and categories have attributes. These attributes provide additional meta-information. An attribute is made of:

* a namespace (optional),
* a name (required),
* a locale (optional), that specifies in which language is the attribute value,
* a value (required even if null).

Example of a variable asked_age which has the following attributes:

============= ====== ==============
Name          Locale Value
============= ====== ==============
label         en     What is your age ?
label         fr     Quel est votre age ?
questionnaire        IdentificationQuestionnaire
page                 P1
============= ====== ==============

The variable asked_age has also some categories (with their attributes):

+------+------------------------------------+
| Name | Attributes                         |
+======+====================================+
| 888  | | label:en=Don't know              |
|      | | label:fr=Ne sait pas             |
+------+------------------------------------+
| 999  | | label:en=Prefer not to answer    |
|      | | label:en=Préfère ne pas répondre |
+------+------------------------------------+
