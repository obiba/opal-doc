How to Set up Multiple R Servers
================================

Opal is able to connect to multiple R servers: see :ref:`rserver` documentation. The benefits of having multiple R servers are:

* Having different versions of R and/or R packages installed, for reproducible science,
* Balance the computation load other several R servers with same profile.

Opal has two different strategies for establishing connection with R servers (see :ref:`apps` documentation):

* Self-registration, which is flexible and then appropriate for load balancing,
* Service discovery, which is preferred for managing multple R server profiles.

Whatever the chosen registration strategy, the name R profile in Opal is the name of the ``cluster`` declared in the Rock R server (see `Cluster Node Configuration <https://rockdoc.obiba.org/en/latest/admin/configuration.html#cluster-node-configuration>`_ documentation).

Using the `Docker <https://www.docker.com/>`_ technology, several R servers can run on the same host. A R server packaged in a Docker container is also easier to maintain, when R packages are to be updated or when a computation envrionment is to be restored. Therefore, the following instructions will recommend the Docker usage and more specifically the `Docker Compose <https://docs.docker.com/compose/>`_ tool.

Step 1 - Prepare Docker Images
------------------------------

The following R server Docker images are proposed:

.. list-table::
  :header-rows: 1

  * - Image
    - Description
  * - `obiba/rock <https://hub.docker.com/r/obiba/rock>`_
    - | `Rock R server <https://www.obiba.org/pages/products/rock/>`_ application with R and useful R packages and system libraries. Everything you need for a standard R server to connect to Opal (reporting, resources, analysis).
      | Available tags are: ``latest``, ``<rock_version>`` (for instance ``1.0``) and ``<rocker_version>-R<r-version>`` (for instance ``1.0-R4.1``).
  * - `datashield/rock-base <https://hub.docker.com/r/datashield/rock-base>`_
    - | Based on ``obiba/rock`` image and includes the `dsBase <http://datashield.github.io/dsBase/>`_ R package for basic DataSHIELD analysis. This is the recommended base image for the DataSHIELD users.
      | Available tags are: ``latest``, ``<dsbase_version>`` (for instance ``6.1``) and ``<dsbase_version>-R<r_version>`` (for instance ``6.1-R4.1``).

From these base images, it is possible to make your own, with additional R packages and system libraries installed. See for instance these demo images:

* `obiba/rock-demo:geo Dockerfile <https://github.com/obiba/docker-rock-demo/blob/geo/Dockerfile>`_ installs geo system libraries and a DataSHIELD R package for geolocalized data analysis.
* `obiba/rock-demo:omics Dockerfile <https://github.com/obiba/docker-rock-demo/blob/omics/Dockerfile>`_ installs some Bioconductor R packages for omics analysis, along with the dsOmics DataSHIELD interface.

Step 2 - Docker Compose Configuration
-------------------------------------

Your Docker Compose configuration can include the Opal server but it is not mandatory, as the Opal server can be installed from a native package, whereas the multiple R servers will be started from docker images.

.. rubric:: Compose Multiple Rock Servers

Different ``datashield/rock-base`` images can be used to expose different R packages versions. The DataSHIELD researcher can specify the appropriate profile name at connection time to ensure that the analysis envrionment is reproducible.

In the following example, several R servers will be accessible through their own port number, and the Opal server must me configured accordingly.

.. code-block:: yaml

  version: '3'
  services:
      datashield:
          image: datashield/rock-base:latest
          ports:
              - ${PORT_DEFAULT}:8085
          environment:
              - ROCK_ID=${ROCK_ID}
              - ROCK_CLUSTER=default
              - ROCK_TAGS=${ROCK_TAGS}
      datashield-61:
          image: datashield/rock-base:6.1-R4.1
          ports:
              - ${PORT_BASE61}:8085
          environment:
              - ROCK_ID=${ROCK_ID}-base-6.1
              - ROCK_CLUSTER=base-6.1
              - ROCK_TAGS=${ROCK_TAGS}

.. rubric:: Discover Rock Servers in Opal

To configure Rock apps discovery in Opal, you can:

* Either set the ``apps.discovery.rock.hosts`` property in the **opal-config.properties** file, see :ref:`appsconf` documentation. Opal server restart is then required.
* Or declare dynamically the new apps in the **Administration > Apps** page, *Discovery* section, see :ref:`apps-discovery` documentation. No Opal server restart is necessary.

Step 3 - Initialize DataSHIELD Settings
---------------------------------------

Connecting Opal to a R server with DataSHIELD R packages is not enough for having a functional DataSHIELD profile: DataSHIELD settings must be initialized, i.e. the allowed aggregate and assign functions along with R options must be declared.

From Administration Page
~~~~~~~~~~~~~~~~~~~~~~~~

.. note::

  1. Go to **Administration > DataSHIELD**
  2. Select a profile
  3. Press **Initialize** in the *Settings* section
  4. Press **Enable** in the *Status* section

  ⇒ The DataSHIELD settings are read from the installed DataSHIELD R packages and set as the profile's configuration.

Using R
~~~~~~~

The `opalr R package <https://www.obiba.org/opalr/>`_ has many functions for DataSHIELD administration, starting with ``dsadmin.*``.

.. code-block:: r

  library(opalr)
  o <- opal.login(username = "administrator", password = "password", url = "https://opal-demo.obiba.org")

  # init and enable the 'default' DS profile
  dsadmin.profile_init(o, "default")
  dsadmin.profile_enable(o, "default")

  opal.logout(o)
