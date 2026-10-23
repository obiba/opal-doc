How to Import Data from Amber
=============================

`Amber <https://www.obiba.org/pages/products/amber/>`_ is the OBiBa data collection application. The case reports and the interviews it collects, with their data dictionary and their uploaded files, can be imported directly in Opal (see also the Amber datasource description in :doc:`../../web-user-guide/projects/datasource-types`).

Getting an Amber API Key
------------------------

Opal connects to Amber with an API key, not with a user account. The key is created by an Amber administrator in Amber Studio (**API Keys** page, see the `Amber API keys documentation <https://amberdoc.obiba.org/en/latest/studio-user-guide/administration/api-keys.html>`_):

* the key gives access to the data of the selected studies only, and it cannot modify anything,
* the key value is shown only once, when the key is created (or regenerated): copy it then,
* an expiry date can be set, and the key can be deactivated at any time,
* each extraction made with the key is visible in the Amber Studio **Audit** page.

Importing Case Reports or Interviews
------------------------------------

.. rubric:: Procedure

.. note::

  0. Preliminary: having an Amber API key giving access to the study,
  1. Go to the destination project's tables page,
  2. Select **Import**,
  3. Select the Data Format **Amber**,
  4. Enter the **Amber URL** (the Amber API URL, e.g. ``https://amber.example.org/api``) and the **API key**,
  5. Select **Case reports** or **Interviews**, and enter the name of the **Study** and of the **Case report form** (or of the **Interview design**),
  6. Optionally, restrict the records to import:

     * **Campaign** (interviews only), the name of the campaign,
     * **State**, the state of the records (``Completed`` by default),
     * **From** and **To**, the period in which the records were last updated,

  7. Optionally, set the **Entity type** that replaces ``Participant`` (the ``CaseReport`` tables of a case report form that allows several records per participant keep their entity type),
  8. Follow the next import steps (incremental, identifiers mapping, tables selection) and launch the import task,
  9. When the import task is completed, go to the new tables' page.

  ⇒ One table per form revision (and per interview step) is created/updated with the imported data and files

Importing New Records Periodically
----------------------------------

To import only the records collected since a previous import, either:

* set the **From** date to the date of the previous import,
* or select the **Incremental** option of the import, so that only the new or updated records are written in the destination tables.

About the Imported Variables
----------------------------

The data dictionary is built from the Amber form items:

* the item labels and choices are the variable labels and categories (in the languages of the form),
* the uploaded files are **binary** variables: their content is imported in Opal,
* a matrix question is split into one variable per row: categorical for a radio matrix, **boolean** for a checkbox matrix,
* the variables of a repeatable group are repeatable, with one value per occurrence.

As the variables follow the form design, a new form revision makes a new table. A view can then be made to combine the tables of the different revisions: :ref:`cb-views`.
