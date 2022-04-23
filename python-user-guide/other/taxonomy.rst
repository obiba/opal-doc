Taxonomy
========

Manage taxonomies: list a summary of the available taxonomies if no option is provided, otherwise download, import or delete a taxonomy.

.. code-block:: bash

  opal taxonomy <CREDENTIALS> [OPTIONS] [EXTRAS]

Options
-------

================================================= ====================================
Option                                            Description
================================================= ====================================
``--download DOWNLOAD, -dl DOWNLOAD``             Download a taxonomy from the provided name, in YAML format
``--import-file IMPORT_FILE, -if IMPORT_FILE``    Import a taxonomy from a YAML file in Opal file system. Fail if the taxonomy already exists.
``--delete DELETE, -dt DELETE``                   Delete a taxonomy from the provided name
``--force, -f``                                   Skip taxonomy deletion confirmation
================================================= ====================================

.. include:: ../common-credentials.rst

Extras
------

================= =================
Option            Description
================= =================
``-h, --help``    Show the command help's message.
``--verbose, -v`` Verbose output.
``--json, -j``    Pretty JSON formatting of the response.
================= =================

Example
-------

List the taxonomies:

.. code-block:: bash

  opal taxonomy --opal https://opal-demo.obiba.org --user administrator --password password --json

Download a taxonomy in YAML format:

.. code-block:: bash

  opal taxonomy --opal https://opal-demo.obiba.org --user administrator --password password --download MyTaxo > MyTaxo.yml

Upload a local taxonomy file (in YAML format) into the Opal file system and import it:

.. code-block:: bash

  opal file --opal https://opal-demo.obiba.org --user administrator --password password --upload /path/to/MyTaxo.yml /home/administrator
  opal taxonomy --opal https://opal-demo.obiba.org --user administrator --password password --import-file /home/administrator/MyTaxo.yml

Delete a taxonomy:

.. code-block:: bash

  opal taxonomy --opal https://opal-demo.obiba.org --user administrator --password password --delete MyTaxo
