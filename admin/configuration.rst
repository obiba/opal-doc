Configuration
=============

Main Configuration File
-----------------------

The file **OPAL_HOME/conf/opal-config.properties** is to be edited to match your server needs.

HTTP Server Configuration
~~~~~~~~~~~~~~~~~~~~~~~~~

Opal web services and web application user interface can be accessed through HTTP or secured HTTP requests. The HTTP(S) connection ports can be configured.

=========================================== =========================================================================
Property                                    Description
=========================================== =========================================================================
``org.obiba.opal.http.port``                The port to use for listening for HTTP connections. Default value is 8080, -1 to disable.
``org.obiba.opal.https.port``               The port to use for listening for HTTPS connections. Default value is 8443, -1 to disable.
``org.obiba.opal.ajp.port``                 The port to use for the Apache JServ Protocol. Default is -1 (disabled).
``org.obiba.opal.maxIdleTime``              The maximum time a single read/write HTTP operation can take in millis (default is 30000). See `idleTimeout Jetty configuration <http://www.eclipse.org/jetty/documentation/current/configuring-connectors.html>`_.
``org.obiba.opal.ssl.excludedProtocols``    Specify the SSL/TLS protocols to be excluded. Usually SSLv3 will be excluded. Use commas for separating multiple protocol names. Default is no protocol is excluded (for legacy reason). See `JSSE Provider documentation <http://docs.oracle.com/javase/8/docs/technotes/guides/security/SunProviders.html#SunJSSEProvider>`_.
``org.obiba.opal.ssl.includedCipherSuites`` Specify which Cipher Suites to be included. Use commas for separating multiple cipher suites names. Default is all that is available. See `JSSE Provider documentation <http://docs.oracle.com/javase/8/docs/technotes/guides/security/SunProviders.html#SunJSSEProvider>`_.
=========================================== =========================================================================

The HTTPS server requires a certificate. If none can be found Opal creates a default one to ensure that HTTPS is always available. It should be configured afterward, following the procedure described in HTTPS Configuration.

SSH Server Configuration
~~~~~~~~~~~~~~~~~~~~~~~~

Opal is accessible using SSH clients: SFTP is available through SSH connections. The SSH connection port can be configured.

=========================== =========================================================================
Property                    Description
=========================== =========================================================================
``org.obiba.opal.ssh.port`` The port to use for listening for SSH connections. Default value is 8022.
=========================== =========================================================================

SMTP Server Configuration
~~~~~~~~~~~~~~~~~~~~~~~~~

Opal is able to send emails to notify that a rapport has been produced. To allow this, it is required to configuration to a SMTP server.

================================ =========================================================================
Property                         Description
================================ =========================================================================
``org.obiba.opal.smtp.host``     The SMTP server host name.
``org.obiba.opal.smtp.port``     The SMTP server port number.
``org.obiba.opal.smtp.from``     The "From" email address when sending emails.
``org.obiba.opal.smtp.auth``     A flag to indicated if authentication against SMTP server is required. Allowed values are: true/false. Default is false (usually not required when server is in the same intranet).
``org.obiba.opal.smtp.username`` The SMTP user name to be authenticate (if authentication is activated).
``org.obiba.opal.smtp.password`` The SMTP user password (if authentication is activated).
================================ =========================================================================

R Server Configuration
~~~~~~~~~~~~~~~~~~~~~~

Opal is able to perform R queries by talking with a running Rserve. Opal does not provide R and Rserve: see R Server Installation Guide. Rserve version must be 0.6+. The properties for connecting to Rserve are the following:

=================================== =========================================================================
Property                            Description
=================================== =========================================================================
``org.obiba.rserver.port``          Port number of the R server controller (allows Opal to start/stop the R server).
``org.obiba.opal.Rserve.host``      Hostname of the Rserve daemon (default is blank, i.e. the one defined by Rserve (localhost))
``org.obiba.opal.Rserve.port``      TCP port to connect to (default is blank, i.e. the one defined by Rserve (6311))
``org.obiba.opal.Rserve.username``  Username to use for login-in to Rserve (none by default)
``org.obiba.opal.Rserve.password``  Password to use for login-in to Rserve (none by default)
``org.obiba.opal.Rserve.encoding``  Character encoding for strings (default is utf8)
``org.obiba.opal.r.sessionTimeout`` Time in minutes after which an active R session will be automatically terminated (default is 4 hours).
=================================== =========================================================================

Agate Server Configuration
~~~~~~~~~~~~~~~~~~~~~~~~~~

Opal user lookup can include the Agate's user realm. Default configuration enables connection to a Agate server.

================================ =========================================================================
Property                         Description
================================ =========================================================================
``org.obiba.realm.url``          Address to connect to Agate server. Default is https://localhost:8444. To disable Agate connection, specify an empty value for this property.
``org.obiba.realm.service.name`` Application name of this Opal instance in Agate. Default is opal.
``org.obiba.realm.service.key``  Application key of this Opal instance in Agate. Default is changeit.
================================ =========================================================================

.. _misc-config:

Miscelaneous Configuration
~~~~~~~~~~~~~~~~~~~~~~~~~~

Advanced settings.

======================================== =========================================================================
Property                                 Description
======================================== =========================================================================
``org.obiba.opal.keys.entityType``       Type of entities to store in the identifiers table.
``org.obiba.opal.keys.tableReference``   Fully-qualified name of the identifiers table
``org.obiba.opal.taxonomies``            Comma separated list of URIs to taxonomy files in YAML format. Note that file URI schema is supported (allows to read locally defined taxonomy).
``org.obiba.opal.plugins.site``          The URL to the plugins repository (default is https://plugins.obiba.org). A plugin repository is not just a list of files, meta-data information about plugins are expected to be provided by a plugins.json file.
``org.obiba.opal.ssl.excludedProtocols`` SSL/TLS (comma separated) protocols that HTTPS server must not reply to. Typical configuration value would be: SSLv3. Default is to not exclude any of the SSL/TLS protocols.
``org.obiba.opal.maxFormContentSize``    Maximum body size of a HTTP(S) form post request. Default value is "200000" bytes.
``org.obiba.opal.ws.messageSizeLimit``   Limit of the Protobuf message size. Default value is "524288000" bytes (500MB).
``org.obiba.magma.entityIdNames``        Specify the column name per entity type to be used for the entity identifier when exporting data to a file (CSV, SAS, SPSS, Stata). If empty for the considered entity type, the default column name will apply. The format to be used is a comma-separated key-value list, for instance: ``org.obiba.magma.entityIdNames=Participant=Idepic,Biomarker=Biom_Id``
``org.obiba.magma.entityIdName``         Specify the default column name to be used for the entity identifier when exporting data to a file (CSV, SAS, SPSS, Stata). If empty, this name depends on the file format.
======================================== =========================================================================

Advanced Configuration File
--------------------------------

The file **OPAL_HOME/data/opal-config.xml** can be edited to match some of your server needs.

File System Root
~~~~~~~~~~~~~~~~

Opal offers a "file system" in which users may manipulate files without having a user defined in the OS running Opal. That is, all interactions with the underlying file-system go through a unique system-user: the one that runs the Opal server.

The Opal file system root is set by default to be OPAL_HOME/fs. To change it, modify the following statement:

.. code-block:: xml

  <!-- Windows example -->
  <fileSystemRoot>C:/opal-filesystem</fileSystemRoot>

Several types of file root names are recognized:

* Absolute URI. These must start with a scheme, such as 'file:', followed by a scheme dependent file name. For example:

    file:/c:/dir/somedir

* Absolute local file name. For example, /home/someuser/somedir or c:\dir\somedir. Elements in the name can be separated using any of the following characters: /, \, or the native file separator character. For example, the following file names are the same:

    c:\dir\somedir
    c:/dir/somedir


User Directories
----------------

The security framework that is used by Opal for authentication, authorization etc. is `Shiro <http://shiro.apache.org/>`_. Configuring Shiro for Opal is done via the file **OPAL_HOME/conf/shiro.ini**. See also `Shiro ini file documentation <http://cwiki.apache.org/confluence/display/SHIRO/Configuration#Configuration-INISections>`_.

.. note::

  Default configuration is a static user 'administrator' with password 'password' (or the one provided while installing Opal Debian/RPM package).

By default Opal server has several built-in user directories (in the world of Shiro, a user directory is called a realm):

* a file-based user directory (**shiro.ini** file),
* the internal Opal user directory,
* the user directory provided by Agate.

In the world of Shiro, a user directory is called a *realm*.

**File Based User Directory**

The file-based user directory configuration file **OPAL_HOME/conf/shiro.ini**.

.. note::

  It is not recommended to use this file-based user directory. It is mainly dedicated to define a default system super-user.

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
  #     cd /usr/share/opal/tools && ./shiro-hasher -p
  #   UNIX:
  #     cd <OPAL_DIST_HOME>/tools && ./shiro-hasher -p
  #   WINDOWS:
  #     cd <OPAL_DIST_HOME>/tools && shiro-hasher.bat -p
  #
  # Format is:
  # username=password[,role]*
  administrator = $shiro1$SHA-256$500000$dxucP0IgyO99rdL0Ltj1Qg==$qssS60kTC7TqE61/JFrX/OEk0jsZbYXjiGhR7/t+XNY=,admin

  [roles]
  # The 'roles' section is for simple deployments
  # when you only need a small number of statically-defined roles.
  # Format is:
  # role=permission[,permission]*
  opal-administrator = *

Passwords must be encrypted using shiro-hasher tools (included in Opal tools directory):

.. code-block:: bash

  cd /usr/share/opal/tools
  ./shiro-hasher -p

LDAP and Active Directory Authentication
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Opal can authenticate users by using an existing LDAP or Active Directory server. This is done by adding the proper configuration section in the shiro.ini file:

.. code-block:: bash

  [main]
  ldapRealm = org.apache.shiro.realm.ldap.JndiLdapRealm
  ldapRealm.contextFactory.url = ldap://ldap.hostname.or.ip:389
  ldapRealm.userDnTemplate = uid={0},ou=users,dc=mycompany,dc=com

The userDnTemplate should be modified to match your LDAP schema. The {0} will be replaced by the username provided at login. Authentication will use the user's credentials to try to bind to LDAP; if binding succeeds, the credentials are considered valid and authentication will succeed.

There is currently no support to extract a user's groups from LDAP. This will be added in a future release.

With Active Directory you can specify a mapping between AD groups and roles in Shiro. Example configuration for Active Directory authentication:

.. code-block:: bash

  [main]
  adRealm = org.apache.shiro.realm.activedirectory.ActiveDirectoryRealm
  adRealm.url = ldap://ad.hostname.or.ip:389
  adRealm.systemUsername = usernameToConnectToAD
  adRealm.systemPassword = passwordToConnectToAD
  adRealm.searchBase = "CN=Users,DC=myorg"
  adRealm.groupRolesMap = "CN=shiroGroup,CN=Users,DC=myorg":"myrole"
  #adRealm.principalSuffix =

Atlassian Crowd User Directory
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Opal can authenticate users by using an Crowd.

First, you need to enable Crowd client by uncommenting the following in OPAL_HOME/conf/custom-context.xml:

.. code-block:: xml

  <import resource="file:${OPAL_HOME}/conf/crowd/crowd-context.xml" />

Then configure your Crowd client in OPAL_HOME/conf/crowd/crowd.properties:

.. code-block:: bash

  application.name=application
  application.password=password
  application.login.url=http://crowd.example.com/crowd/console/
  crowd.server.url=http://crowd.example.com/crowd/services/
  crowd.base.url=http://crowd.example.com/crowd/
  session.isauthenticated=session.isauthenticated
  session.tokenkey=session.tokenkey
  session.validationinterval=2
  session.lastvalidation=session.lastvalidation

Other Settings
~~~~~~~~~~~~~~

Shiro's default session timeout is 1800s (half an hour). The session timeout can be set explicitly in the shiro.ini file, in the [main] section:

.. code-block:: bash

  # =======================
  # Shiro INI configuration
  # =======================

  [main]
  # Objects and their properties are defined here,
  # Such as the securityManager, Realms and anything else needed to build the SecurityManager
  # 3,600,000 milliseconds = 1 hour
  securityManager.sessionManager.globalSessionTimeout = 3600000

  # ...

The session timeout is in milliseconds and allowed values are:

* a negative value means sessions never expire.
* a non-negative value (0 or greater) means session timeout will occur as expected.


Reverse Proxy Configuration
---------------------------

Opal server can be accessed through a reverse proxy server.

**Apache**

Example of Apache directives that:

* redirects HTTP connection on port 80 to HTTPS connection on port 443,
* specifies acceptable protocols and cipher suites,
* refines organization's specific certificate and private key.

.. code-block:: text

  <VirtualHost *:80>
      ServerName opal.your-organization.org
      ProxyRequests Off
      ProxyPreserveHost On
      <Proxy *>
          Order deny,allow
          Allow from all
      </Proxy>
      RewriteEngine on
      ReWriteCond %{SERVER_PORT} !^443$
      RewriteRule ^/(.*) https://opal.your-organization.org:443/$1 [NC,R,L]
  </VirtualHost>
  <VirtualHost *:443>
      ServerName opal.your-organization.org
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
      ProxyPass / https://localhost:8443/
      ProxyPassReverse / https://localhost:8443/
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
