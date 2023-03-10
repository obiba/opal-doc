.. _apipy:

Python API
==========

Opal Python can be easily extended by using the `exposed classes <https://github.com/obiba/opal-python-client/blob/master/obiba_opal/__init__.py>`_. The classes ``*Command`` return an Opal task object, to be followed with the ``TaskService``. The classes ``*Service`` perform immediate operations.

Packages
--------

Use the ``pydoc`` tool to get the Python documentation.

.. code-block:: shell

  pydoc obiba_opal.<package name>

=============================== ================================================
Package                         Description
=============================== ================================================
``obiba_opal.analysis``         Table analysis related classes, to launch an analysis command and export analysis output.
``obiba_opal.core``             Core classes for establishing a connection with an Opal server, send requests and aget responses.
``obiba_opal.data``             Table data and entities related classes, to get list of entities, values and value sets.
``obiba_opal.dictionary``       Table dictionary related classes, to list tables and variables and to manage variable annotations.
``obiba_opal.exports``          Various export commands.
``obiba_opal.file``             File management classes, to upload, download, get info and delete files.
``obiba_opal.imports``          Various import commands.
``obiba_opal.io``               Import/export base classes.
``obiba_opal.perm``             Permission management related classes, for various Opal items.
``obiba_opal.project``          Project management classes, to perform backup/restore commands and to add/delete/list projects.
``obiba_opal.security``         Encryption/decryption service.
``obiba_opal.sql``              Table SQL related classes, to perform SQL queries on tables.
``obiba_opal.subjects``         Users and Groups management classes.
``obiba_opal.system``           Various system services, to perform operations on tasks, taxonomys, plugins etc.
``obiba_opal.table``            Backup/restore views.
=============================== ================================================

Usage Example
-------------

.. code-block:: python

  from obiba_opal import OpalClient, HTTPError, Formatter, ImportCSVCommand, TaskService, FileService, DictionaryService

  # if 2-factor auth is enabled, user will be asked for the secret code
  # Personal access token authentication is also supported (and recommended)
  client = OpalClient.buildWithAuthentication(server='https://opal-demo.obiba.org', user='administrator', password='password')

  try:
      # upload a local CSV data file into Opal file system
      fs = FileService(client)
      fs.upload_file('./data.csv', '/tmp')

      # import this CSV file into a project
      task = ImportCSVCommand(client).import_data('/tmp/data.csv', 'CNSIM')
      status = TaskService(client).wait_task(task['id'])

      # clean data file from Opal
      fs.delete_file('/tmp/data.csv')

      if status == 'SUCCEEDED':
          dico = DictionaryService(client)
          table = dico.get_table('CNSIM', 'data')
          # do something ...
          dico.delete_tables('CNSIM', ['data'])
      else:
          print('Import failed!')
          # do something ...
  except HTTPError as e:
      Formatter.print_json(e.error, True)
  finally:
      client.close()
