Import Amber
============

Import the case reports of a case report form, or the interviews of an interview design, with their data dictionary and their uploaded files, from an `Amber <https://www.obiba.org/pages/products/amber/>`_ server. Opal connects to Amber with an Amber API key, created by an Amber administrator in Amber Studio, giving access to the study (see :doc:`../../cookbook/import-data/amber`).

.. code-block:: bash

  opal import-amber <CREDENTIALS> <OPTIONS> [EXTRAS]

Options
-------

.. list-table::
   :widths: 30 70
   :header-rows: 1

   * - Option
     - Description
   * - ``--destination DESTINATION, -d DESTINATION``
     - Destination datasource name
   * - ``--tables TABLE1 [--tables TABLE2 ...], -t TABLE1 [-t TABLE2 ...]``
     - The list of tables to be imported (defaults to all)
   * - ``--incremental -i``
     - Incremental import
   * - ``--limit LIMIT, -li LIMIT``
     - Import limit (maximum number of value sets)
   * - ``--identifiers IDENTIFIERS, -id IDENTIFIERS``
     - Name of the ID mapping
   * - ``--policy POLICY, -po POLICY``
     - | ID mapping policy:
       |
       | ``required`` : each identifiers must be mapped prior importation (default),
       | ``ignore`` : ignore unknown identifiers,
       | ``generate`` : generate a system identifier for each unknown identifier.
   * - ``--amber AMBER, -am AMBER``
     - Amber API base url (e.g. ``https://amber.example.org/api``)
   * - ``--key KEY, -ak KEY``
     - Amber API key giving access to the study
   * - ``--study STUDY, -st STUDY``
     - Amber study name
   * - ``--crf CRF, -cr CRF``
     - Amber case report form name, to import its case reports (exclusive from ``--design``)
   * - ``--design DESIGN, -ds DESIGN``
     - Amber interview design name, to import its interviews, i.e. the data of each of its steps' forms (exclusive from ``--crf``)
   * - ``--campaign CAMPAIGN, -ca CAMPAIGN``
     - Amber campaign name, to filter the interviews
   * - ``--state STATE, -sta STATE``
     - | Record state:
       |
       | ``completed`` (default),
       | ``in_progress``,
       | ``initiated`` (interviews only),
       | ``all`` for any state.
   * - ``--from FROM, -fr FROM``
     - Records updated since this date (``YYYY-MM-DD``)
   * - ``--to TO, -to TO``
     - Records updated until this date (``YYYY-MM-DD``)
   * - ``--type TYPE, -ty TYPE``
     - Entity type (default is the one defined by Amber)
   * - ``--merge, -mg``
     - Merge imported data dictionary with the destination one (default is false, i.e. data dictionary is overridden).

.. include:: ../common-credentials.rst

.. include:: ../common-extras-json.rst

Example
-------

Import the completed case reports of the ``Baseline`` case report form of the study ``MyStudy``:

.. code-block:: bash

  opal import-amber -o http://localhost:8080 -u administrator -p password --amber https://amber.example.org/api --key amb_xxxxxx --study MyStudy --crf Baseline --destination mystudy

Import the interviews of the ``Autumn`` campaign of the ``Follow-up`` interview design, updated since January 1st 2026:

.. code-block:: bash

  opal import-amber -o http://localhost:8080 -u administrator -p password --amber https://amber.example.org/api --key amb_xxxxxx --study MyStudy --design Follow-up --campaign Autumn --from 2026-01-01 --incremental --destination mystudy
