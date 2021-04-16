Projects
========

List
----

.. http:get:: /projects?[digest=(boolean:digest)]

  Get the list of projects.

  **Example requests**

  Using cURL

  .. sourcecode:: shell

     curl -H "Authorization: X-Opal-Auth `echo -n 'administrator:password'|base64`" -H "Accept: application/json" https://opal-demo.obiba.org/ws/projects

  Using the :doc:`../python-user-guide/project/project` Python command line tool

  .. sourcecode:: shell

     opal project -o https://opal-demo.obiba.org -u administrator -p password --json

  :query boolean digest: Do not include associated :doc:`datasource` information. Default value is ``false``.

Create
------

.. http:post:: /projects

  Create a new project.

  **Example requests**

  Using cURL

  .. sourcecode:: shell

     curl -H "Authorization: X-Opal-Auth `echo -n 'administrator:password'|base64`" -H "Accept: application/json" --data-binary "@project.json" -X POST https://opal-demo.obiba.org/ws/projects

  Using the :doc:`../python-user-guide/project/project` Python command line tool

  .. sourcecode:: shell

     opal project -o https://opal-demo.obiba.org -u administrator -p password --add foo --database somedb --title "Foo" --description "Foo project"
