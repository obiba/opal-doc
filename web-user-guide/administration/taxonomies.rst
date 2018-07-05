Taxonomies
==========

Taxonomies are used to perform variables classification. Taxonomy items (vocabulary and term) have a title and a description (multi language support).

Taxonomy
--------

A taxonomy is a set of controlled vocabularies. It provides also authoring information (author, license). Recommended license is one of the `Creative Commons <https://creativecommons.org/choose/>`_ licenses.

Vocabulary
~~~~~~~~~~

A vocabulary is controlled in the way that it provides a set of terms. These terms are used to annotate the variables: a variable annotation is a variable attribute which namespace is a taxonomy, name is a vocabulary and value is one of the terms defined by the vocabulary.

When a vocabulary has no term, any text is accepted as a variable annotation for this vocabulary. Opal supports text formatted in `Markdown <https://guides.github.com/features/mastering-markdown/>`_.

Operations
----------

Add Taxonomy
~~~~~~~~~~~~

Add a taxonomy from scratch.

Import Maelstrom Research Taxonomies
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

`Maelstrom Research <https://www.maelstrom-research.org/>`_ provides a complete set of taxonomies to classify variables (classification `based on the experience of more than 700K variables <https://www.maelstrom-research.org/mica/repository#search>`_) and to describe the dataset harmonization process. Importing these taxonomies requires a download key that can be requested at Maelstrom Research (link to request form is provided).

Import Taxonomy from Github
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Import one or more taxonomies from a `Github <https://github.com/>`_ repository. Taxonomy `YAML <http://yaml.org/>`_ files are expected to be found in this repository. A taxonomy YAML file is the one that can be downloaded from a taxonomy page.
