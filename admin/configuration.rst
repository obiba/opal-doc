Configuration
=============

The file **MICA_HOME/conf/application.yml** is to be edited to match your server needs. This file is written in YAML format allowing to specify a hierarchy within the configuration keys. The YAML format uses indentations to express the different levels of this hierarchy. The file is already pre-filled with default values (to be modified to match your configuration), just be aware that you should not modify the indentations. In the following documentation, the configuration keys will be presented using the dot-notation (levels are separated by dots) for readability.

HTTP Server Configuration
-------------------------

Mica server is a web application and as such, you need to specify on which ports the web server should listen to incoming requests.

=============== ==================
Property        Description
=============== ==================
``server.port`` HTTP port number. Generally speaking this port should not be exposed to the web. Use the https port instead.
``server.host`` Web server host name.
``https.port``  HTTPS port number.
=============== ==================

MongoDB Server Configuration
----------------------------

Mica server will store its data (system configuration, networks, studies, datasets, etc.) in a MongoDB database. You must specify how to connect to this database.

=========================== ===========================
Property                    Description
=========================== ===========================
``spring.data.mongodb.uri`` MongoDB URI. `Read Standard Connection <https://docs.mongodb.com/manual/reference/connection-string/>`_ String Format to learn more.
=========================== ===========================

By default MongoDB does not require any user name, it is highly recommended to configure the database with a user. This can be done by enabling the Client Access Control procedure.

Follow these steps to enable the Client Access Control on your server:

* create a user with the proper roles on the target databases
* restart the MongoDB service with Client Access Control enabled

.. note::

  Once the MongoDB service runs with Client Access Control enabled, all database connections require authentication.

**MongoDB User Creation Example**

The example below creates the *micaadmin* user for *mica* database:

.. code-block:: javascript

  use admin

  db.createRole({
    role: 'obibauser',
    privileges:[{
        resource: {anyResource: true},
        actions: ['anyAction']
    }],
    roles: []
  });

  db.createUser({
    user: "micaadmin",
    pwd: "micaadmin",
    roles: ['obibauser']
  });

Here is the required configuration snippet in **/etc/mica/application.yml** for the above user:

.. code-block:: yaml

  spring:
    data:
      mongodb:
        uri: mongodb://micaadmin:micaadmin@localhost:27017/mica?authSource=admin

.. note::

  Mica requires either **clusterMonitor** or **readAnyDatabase** role on the *admin* database for validation operations. The first role is useful for a cluster setup and the latter if your MongoDB is on a single server.

Opal Server Configuration
-------------------------

Mica server uses Opal to retrieve data dictionaries, data summaries and variable taxonomies. This server is sometimes referred as the Opal primary server (secondary servers can be defined at study level). If you want to publish datasets, the following Opal connection details needs to be configured.

================= ================================================================
Property          Description
================= ================================================================
``opal.url``      Opal server URL. It is highly recommended to use https protocol.
``opal.username`` User name for connection to Opal server.
``opal.password`` User password for connection to Opal server.
================= ================================================================

Mica server should connect to Opal and access to some selected tables only with the lowest level of permissions (View dictionary and summary, i.e. no access to individual data). Please refer to the Opal Table Documentation for more details about the permissions that can be applied on a table.

Mica Server Configuration
--------------------------

Mica server uses Mica as a user directory and as a notification emails service. From the Mica point of view, Mica is not a user: it is an application. Each time Mica needs a service from Mica, it will provide the information necessary to its identification. The application credentials registered in Mica are to be specified in this section. If you want to specify advanced permissions or allow users to submit data access requests, the following Mica connection details needs to be configured.

========================== ================================================================
Property                   Description
========================== ================================================================
``agate.url``              Mica server URL. It is highly recommended to use https protocol.
``agate.application.name`` Application name for connection to Mica server.
``agate.application.key``  Application key for connection to Mica server.
========================== ================================================================

Shiro Configuration
-------------------

`Shiro <http://shiro.apache.org/>`_ is the authentication and authorization framework used by Mica. There is a minimum advanced configuration that can be applied to specify how Shiro will hash the password. In practice this only applies to the users defined in the shiro.ini file. Default configuration is usually enough.

=================================== ================================
Property                            Description
=================================== ================================
``shiro.password.nbHashIterations`` Number of re-hash operations.
``shiro.password.salt``             Salt to be applied to the hash.
=================================== ================================

Elasticsearch Configuration
---------------------------

Mica server embeds `Elasticsearch <https://www.elastic.co/>`_ as its search engine. Elasticsearch is a key functionality of Mica as the process of publication consist in indexing documents (networks, studies, variables etc.) in the search engine. Advanced queries can be applied on the published documents. Elasticsearch is embeded, i.e. it is not an external application. Mica's Elasticsearch can be part of a cluster of Elasticsearch cluster. The configuration of the Elasticsearch node and how it should connect to the other nodes of the cluster can be specified in this section. Default configuration is usually enough.

=================================== ================================
Property                            Description
=================================== ================================
``elasticsearch.dataNode``          Boolean to specify if this node has data or if it is just a proxy to other nodes in a cluster.
``elasticsearch.clusterName``       Cluster identifier.
``elasticsearch.shards``            Number of shards.
``elasticsearch.replicas``          Number of replicas.
``elasticsearch.settings``          A string in JSON or YAML format to define other elasticsearch settings. See Elasticsearch Documentation for advanced settings.
``elasticsearch.transportClient``   Boolean to indicate to use the Transport Client instead of creating an elasticsearch Node.
``elasticsearch.transportAddress``  Elasticsearch service IP address and port when using the Transport Client, defaults to the localhost at port 9300.
``elasticsearch.transportSniff``    Boolean to indicate the Transport Client to collect IP addresses from nodes in an elasticsearch cluster.
=================================== ================================

**Elasticsearch Cluster**

Mica can be set to join or connect to an Elasticsearch cluster. You need to set *elasticsearch.clusterName* to the name of the cluster you want to join. There are different possible `cluster topologies <https://www.elastic.co/guide/en/elasticsearch/reference/current/modules-node.html>`_, each of which has different resource utilization profiles in terms or memory and CPU.

.. note::

  To avoid API incompatibility issues, the recommended version of `Elasticsearch server is 2.4 <https://www.elastic.co/downloads/past-releases/elasticsearch-2-4-4>`_.


An example of a configuration to join an elasticsearch cluster using a `Client Node <https://www.elastic.co/guide/en/elasticsearch/reference/2.2/modules-node.html#client-node>`_:

.. code-block:: yaml

  elasticsearch:
    clusterName: mycluster
    dataNode: false
    settings: '{"node.master": false, "node.local": false}'

An example of a configuration using the transport client:

.. code-block:: yaml

  elasticsearch:
    clusterName: mycluster
    transportClient: true
    transportAddress: "myhost:9300"

**Elasticsearch Server Configuration**

Mica uses the scripting capabilities of Elasticsearch. All the machines in the Elasticsearch cluster should have the scripting module enabled by setting the following values in the *elasticsearch.yml* configuration file (location of this file depends on how your elasticsearch service is installed):

.. code-block:: yaml

  script:
    inline: true
    indexed: true

User Directories
----------------

The security framework that is used by Mica for authentication, authorization etc. is `Shiro <http://shiro.apache.org/>`_. Configuring Shiro for Mica is done via the file **MICA_HOME/conf/shiro.ini**. See also `Shiro ini file documentation <http://cwiki.apache.org/confluence/display/SHIRO/Configuration#Configuration-INISections>`_.

.. note::

  Default configuration is a static user 'administrator' with password 'password' (or the one provided while installing Mica Debian/RPM package).

By default Mica server has several built-in user directories (in the world of Shiro, a user directory is called a realm):

* a file-based user directory (**shiro.ini** file),
* the user directory provided by Agate.

Although it is possible to register some additional user directories, this practice is not recommended as Agate provides more than a service of authentication (user profile, notification emails etc.).

In the world of Shiro, a user directory is called a *realm*.

**File Based User Directory**

The file-based user directory configuration file **MICA_HOME/conf/shiro.ini**.

.. note::

  It is not recommended to use this file-based user directory. It is mainly dedicated to define a default system super-user and a password for the anonymous user.

For a better security, user passwords are encrypted with a one way hash such as sha256.

The example shiro.ini file below demonstrates how encryption is configured.

.. code-block:: bash

  # =======================
  # Shiro INI configuration
  # =======================

  [main]
  # Objects and their properties are defined here,
  # Such as the securityManager, Realms and anything else needed to build the SecurityManager


  [users]
  # The 'users' section is for simple deployments
  # when you only need a small number of statically-defined set of User accounts.
  #
  # Password here must be encrypted!
  # Use shiro-hasher tools to encrypt your passwords:
  #   DEBIAN:
  #     cd /usr/share/mica2/tools && ./shiro-hasher -p
  #   UNIX:
  #     cd <MICA_DIST_HOME>/tools && ./shiro-hasher -p
  #   WINDOWS:
  #     cd <MICA_DIST_HOME>/tools && shiro-hasher.bat -p
  #
  # Format is:
  # username=password[,role]*
  administrator = $shiro1$SHA-256$500000$dxucP0IgyO99rdL0Ltj1Qg==$qssS60kTC7TqE61/JFrX/OEk0jsZbYXjiGhR7/t+XNY=,mica-administrator
  anonymous = $shiro1$SHA-256$500000$dxucP0IgyO99rdL0Ltj1Qg==$qssS60kTC7TqE61/JFrX/OEk0jsZbYXjiGhR7/t+XNY=

  [roles]
  # The 'roles' section is for simple deployments
  # when you only need a small number of statically-defined roles.
  # Format is:
  # role=permission[,permission]*
  mica-administrator = *

Passwords must be encrypted using shiro-hasher tools (included in Mica tools directory):

.. code-block:: bash

  cd /usr/share/mica2/tools
  ./shiro-hasher -p

Reverse Proxy Configuration
---------------------------

Mica server can be accessed through a reverse proxy server.

**Apache**

Example of Apache directives that:

* redirects HTTP connection on port 80 to HTTPS connection on port 443,
* specifies acceptable protocols and cipher suites,
* refines organization's specific certificate and private key.

.. code-block:: text

  <VirtualHost *:80>
      ServerName mica.your-organization.org
      ProxyRequests Off
      ProxyPreserveHost On
      <Proxy *>
          Order deny,allow
          Allow from all
      </Proxy>
      RewriteEngine on
      ReWriteCond %{SERVER_PORT} !^443$
      RewriteRule ^/(.*) https://mica.your-organization.org:443/$1 [NC,R,L]
  </VirtualHost>
  <VirtualHost *:443>
      ServerName mica.your-organization.org
      SSLProxyEngine on
      SSLEngine on
      SSLProtocol All -SSLv2 -SSLv3
      SSLHonorCipherOrder on
      # Prefer PFS, allow TLS, avoid SSL, for IE8 on XP still allow 3DES
      SSLCipherSuite "EECDH+ECDSA+AESGCM EECDH+aRSA+AESGCM EECDH+ECDSA+SHA384 EECDH+ECDSA+SHA256 EECDH+aRSA+SHA384 EECDH+aRSA+SHA256 EECDH+AESG CM EECDH EDH+AESGCM EDH+aRSA HIGH !MEDIUM !LOW !aNULL !eNULL !LOW !RC4 !MD5 !EXP !PSK !SRP !DSS"
      # Prevent CRIME/BREACH compression attacks
      SSLCompression Off
      SSLCertificateFile /etc/apache2/ssl/cert/your-organization.org.crt
      SSLCertificateKeyFile /etc/apache2/ssl/private/your-organization.org.key
      ProxyRequests Off
      ProxyPreserveHost On
      ProxyPass / https://localhost:8445/
      ProxyPassReverse / https://localhost:8445/
  </VirtualHost>

For performance, you can also activate Apache's compression module (mod_deflate) with the following settings (note the json content type setting) in file */etc/apache2/mods-available/deflate.conf*:

.. code-block:: text

  <IfModule mod_deflate.c>
    <IfModule mod_filter.c>
        # these are known to be safe with MSIE 6
        AddOutputFilterByType DEFLATE text/html text/plain text/xml
        # everything else may cause problems with MSIE 6
        AddOutputFilterByType DEFLATE text/css
        AddOutputFilterByType DEFLATE application/x-javascript application/javascript application/ecmascript
        AddOutputFilterByType DEFLATE application/rss+xml
        AddOutputFilterByType DEFLATE application/xml
        AddOutputFilterByType DEFLATE application/json
    </IfModule>
  </IfModule>
