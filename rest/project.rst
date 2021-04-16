Project
=======

Get
---

.. http:get:: /project/(string: id)

  Get a project.

  **Example requests**

  Using cURL

  .. sourcecode:: shell

     curl -H "Authorization: X-Opal-Auth `echo -n 'administrator:password'|base64`" -H "Accept: application/json" https://opal-demo.obiba.org/ws/project/CNSIM

  Using the :doc:`../python-user-guide/project/project` Python command line tool

  .. sourcecode:: shell

     opal project -o https://opal-demo.obiba.org -u administrator -p password --name CNSIM --json

Summary
-------

.. http:get:: /project/(string: id)

   Get a project's summary.

   **Example requests**

   Using cURL

   .. sourcecode:: shell

      curl -H "Authorization: X-Opal-Auth `echo -n 'administrator:password'|base64`" -H "Accept: application/json" https://opal-demo.obiba.org/ws/project/CNSIM/summary

   Using the :doc:`../python-user-guide/other/rest` Python command line tool

   .. sourcecode:: shell

      opal rest -o https://opal-demo.obiba.org -u administrator -p password -m GET /project/CNSIM/summary --json

State
-----

.. http:get:: /project/(string: id)

   Get a project's :doc:`datasource` loading state.

   **Example requests**

   Using cURL

   .. sourcecode:: shell

      curl -H "Authorization: X-Opal-Auth `echo -n 'administrator:password'|base64`" https://opal-demo.obiba.org/ws/project/CNSIM/state

   Using the :doc:`../python-user-guide/other/rest` Python command line tool

   .. sourcecode:: shell

      opal rest -o https://opal-demo.obiba.org -u administrator -p password -m GET /project/CNSIM/state --json

Update
------

.. http:put:: /project/(string: id)

   Update a project.

   **Example requests**

   Using cURL

   .. sourcecode:: shell

      curl -H "Authorization: X-Opal-Auth `echo -n 'administrator:password'|base64`" --data-binary "@project.json" -X PUT https://opal-demo.obiba.org/ws/project/CNSIM

   Using the :doc:`../python-user-guide/other/rest` Python command line tool

   .. sourcecode:: shell

      opal rest -o https://opal-demo.obiba.org -u administrator -p password --content-type "application/json" -m GET /project/CNSIM < project.json

Remove
------

.. http:get:: /project/(string: id)

  Remove a project.

  **Example requests**

  Using cURL

  .. sourcecode:: shell

     curl -H "Authorization: X-Opal-Auth `echo -n 'administrator:password'|base64`" -X DELETE https://opal-demo.obiba.org/ws/project/CNSIM

  Using the :doc:`../python-user-guide/project/project` Python command line tool

  .. sourcecode:: shell

     opal project -o https://opal-demo.obiba.org -u administrator -p password --name CNSIM --delete
