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
``org.obiba.opal.http.port``                The port to use for listening for HTTP connections. Default value is ``8080``, -1 to disable.
``org.obiba.opal.https.port``               The port to use for listening for HTTPS connections. Default value is ``8443``, -1 to disable.
``org.obiba.opal.maxIdleTime``              The maximum time a single read/write HTTP operation can take in millis (default is ``30000``). See `idleTimeout Jetty configuration <http://www.eclipse.org/jetty/documentation/current/configuring-connectors.html>`_.
``org.obiba.opal.ssl.excludedProtocols``    Specify the SSL/TLS protocols to be excluded. Usually SSLv3 will be excluded. Use commas for separating multiple protocol names. Default is no protocol is excluded (for legacy reason). See `JSSE Provider documentation <http://docs.oracle.com/javase/8/docs/technotes/guides/security/SunProviders.html#SunJSSEProvider>`_.
``org.obiba.opal.ssl.includedCipherSuites`` Specify which Cipher Suites to be included. Use commas for separating multiple cipher suites names. Default is all that is available. See `JSSE Provider documentation <http://docs.oracle.com/javase/8/docs/technotes/guides/security/SunProviders.html#SunJSSEProvider>`_.
``org.obiba.opal.server.context-path``      The context path when server is accessed at a subdirectory (for instance in ``http://example.org/opal`` the context path is ``/opal``). Default is empty.
=========================================== =========================================================================

The HTTPS server requires a certificate. If none can be found Opal creates a default one to ensure that HTTPS is always available. It should be configured afterward, following the procedure described in HTTPS Configuration.

SSH Server Configuration
~~~~~~~~~~~~~~~~~~~~~~~~

Opal is accessible using SSH clients: SFTP is available through SSH connections. The SSH connection port can be configured.

=========================== =========================================================================
Property                    Description
=========================== =========================================================================
``org.obiba.opal.ssh.port`` The port to use for listening for SSH connections. Default value is ``8022``.
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
``org.obiba.opal.smtp.auth``     A flag to indicated if authentication against SMTP server is required. Allowed values are: true/false. Default is ``false`` (usually not required when server is in the same intranet).
``org.obiba.opal.smtp.username`` The SMTP user name to be authenticate (if authentication is activated).
``org.obiba.opal.smtp.password`` The SMTP user password (if authentication is activated).
================================ =========================================================================

.. _appsconf:

Apps Configuration
~~~~~~~~~~~~~~~~~~

External applications can be discovered or can self-register. The following settings the apps management defaults.

======================================= =========================================================================
Property                                Description
======================================= =========================================================================
``apps.registration.token``             Apps self-registration default token. Default is empty (self-registration not allowed). When configured from :ref:`apps` administration page, this value is overridden.
``apps.registration.include``           White list rule to accept an app self-registration: (java) regular expression applied to app's server address. If not defined (default) all apps are filtered-in.
``apps.registration.exclude``           Black list rule to accept an app self-registration: (java) regular expression applied to app's server address. If not defined (default) no app is filtered-out.
``apps.discovery.interval``             Apps discovery scheduling in milliseconds. Default is ``10000``.
``apps.discovery.rock.hosts``           Comma separated list of `Rock <https://rockdoc.obiba.org>`_ R server URLs to discover on start up. Default is ``localhost:8085``. See also :ref:`rconf`.
======================================= =========================================================================

.. _rconf:

R Server Configuration
~~~~~~~~~~~~~~~~~~~~~~

Opal is able to perform R queries by talking with a running R server. See the :ref:`rserver` documentation. The properties for connecting to the default `Rock <https://rockdoc.obiba.org>`_ R server(s) are the following:

============================================== =========================================================================
Property                                       Description
============================================== =========================================================================
``rock.default.administrator.username``        Rock administrator user name. Default is ``administrator``.
``rock.default.administrator.password``        Rock administrator user password. Default is ``password``.
``rock.default.manager.username``              Rock manager user name.
``rock.default.manager.password``              Rock manager user password.
``rock.default.user.username``                 Rock regular user name.
``rock.default.user.password``                 Rock regular user password.
``org.obiba.opal.r.endpoint``                  Enable/disable the plain R web service. When disabled, even the system administrator cannot interact directly with a plain R session. Use of the DataSHIELD web service is recommended instead. Default is ``true`` (enabled).
``org.obiba.opal.r.sessionTimeout``            Time in minutes after which an inactive R session will be automatically terminated (default is 4 hours).
``org.obiba.opal.r.sessionTimeout.R``          Time in minutes after which an inactive R session with **R context** will be automatically terminated (default is to fallback to ``org.obiba.opal.r.sessionTimeout``).
``org.obiba.opal.r.sessionTimeout.DataSHIELD`` Time in minutes after which an inactive R session with **DataSHIELD context** will be automatically terminated (default is to fallback to ``org.obiba.opal.r.sessionTimeout``).
``org.obiba.opal.r.sessionTimeout.Import``     Time in minutes after which an inactive R session with **Import context** will be automatically terminated (default is to fallback to ``org.obiba.opal.r.sessionTimeout``).
``org.obiba.opal.r.sessionTimeout.Export``     Time in minutes after which an inactive R session with **Export context** will be automatically terminated (default is to fallback to ``org.obiba.opal.r.sessionTimeout``).
``org.obiba.opal.r.sessionTimeout.SQL``        Time in minutes after which an inactive R session with **SQL context** will be automatically terminated (default is to fallback to ``org.obiba.opal.r.sessionTimeout``).
``org.obiba.opal.r.sessionTimeout.Analyse``    Time in minutes after which an inactive R session with **Analyse context** will be automatically terminated (default is to fallback to ``org.obiba.opal.r.sessionTimeout``).
``org.obiba.opal.r.sessionTimeout.View``       Time in minutes after which an inactive R session with **View context** will be automatically terminated (default is to fallback to ``org.obiba.opal.r.sessionTimeout``).
``org.obiba.opal.r.repos``                     The list of CRAN repositories from which R packages can be downloaded, comma separated. Default value is ``https://cloud.r-project.org,https://cran.obiba.org``.
============================================== =========================================================================

DataSHIELD Configuration
~~~~~~~~~~~~~~~~~~~~~~~~

Some minimal default DataSHIELD infrastructure settings can be defined.

======================================= =========================================================================
Property                                Description
======================================= =========================================================================
``datashield.r.parser``                 DataSHIELD R parser version: ``v1`` or ``v2`` See `DataSHIELD4J library documentation <https://github.com/obiba/datashield4j>`_. Default is the latest.
======================================= =========================================================================


Login Policy Configuration
~~~~~~~~~~~~~~~~~~~~~~~~~~

To prevent brute force password guessing, a user can be temporarily banned after too many login failures.

===================================================== =========================================================================
Property                                              Description
===================================================== =========================================================================
``org.obiba.opal.security.login.maxRetry``            Number of failed login attempts before being banned (default is ``3``).
``org.obiba.opal.security.login.retryTime``           Time span in which the maximum of retry count should happen before starting a ban period, in seconds (default is ``300``). No time limit if not positive.
``org.obiba.opal.security.login.banTime``             Ban time after max retry, within the retry time span, was reached, in seconds (default is ``300``). No ban if not positive.
``org.obiba.opal.security.login.pat.expiresIn``       Time in days after which a personal access token is automatically removed. Default is ``-1`` (i.e. tokens never expire).
``org.obiba.opal.security.login.pat.activityTimeout`` Time in days since last access after which a personal access token is marked as being inactive. This state can be reverted by user. Default is ``60`` (2 months).
===================================================== =========================================================================

Agate Server Configuration
~~~~~~~~~~~~~~~~~~~~~~~~~~

Opal user lookup can include the Agate's user realm. Default configuration enables connection to a Agate server.

================================ =========================================================================
Property                         Description
================================ =========================================================================
``org.obiba.realm.url``          Address to connect to Agate server. Default is https://localhost:8444. To disable Agate connection, specify an empty value for this property.
``org.obiba.realm.publicUrl``    Public address to create a link from Opal's user profile page to the Agate's one where personal information, password and two-factor authentication can be managed. Default is empty.
``org.obiba.realm.service.name`` Application name of this Opal instance in Agate. Default is ``opal``.
``org.obiba.realm.service.key``  Application key of this Opal instance in Agate. Default is ``changeit``.
================================ =========================================================================

System Identifiers Generation Configuration
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

When importing data and selecting a identifiers mapping, if an imported identifier does not exist for the selected mapping and the strategy that was chosen is
to generate a system identifier, then the following default settings apply for system identifiers generation:

======================================= =========================================================================
Property                                Description
======================================= =========================================================================
``org.obiba.opal.identifiers.length``   Length of the numerical part of the identifier (i.e. not including the prefix length). Default is ``10``.
``org.obiba.opal.identifiers.zeros``    Allow leading zeros in the numerical part of the identifiers. Default is ``false``.
``org.obiba.opal.identifiers.prefix``   Character prefix to be applied. Default is none.
``org.obiba.opal.identifiers.checksum`` Add a checksum digit so that the generated identifier can be validated regarding the Luhn algorithm. Default is ``false``.
======================================= =========================================================================

Cross Site Resource Forgery (CSRF)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

`CSRF <https://owasp.org/www-community/attacks/csrf>`_ attacks can be mitigated by a built-in interceptor. Default behavior allows connections (http or https) from ``localhost`` and ``127.0.0.1``. Requests from pages served by Opal should be allowed as well (https only), unless network settings or proxies modify or do not report the referer URL.

======================================= =========================================================================
Property                                Description
======================================= =========================================================================
``csrf.allowed``                        Comma separated list of client ``host:port`` explicitly allowed to connect to Opal server. Use ``*`` as a wildcard. Default is empty.
======================================= =========================================================================

.. _misc-config:

Miscelaneous Configuration
~~~~~~~~~~~~~~~~~~~~~~~~~~

Advanced settings.

======================================================== =========================================================================
Property                                                 Description
======================================================== =========================================================================
``org.obiba.opal.keys.entityType``                       Type of entities to store in the identifiers table.
``org.obiba.opal.keys.tableReference``                   Fully-qualified name of the identifiers table
``org.obiba.opal.taxonomies``                            Comma separated list of URIs to taxonomy files in YAML format. Note that file URI schema is supported (allows to read locally defined taxonomy).
``org.obiba.opal.plugins.site``                          The URL to the plugins repository (default is https://plugins.obiba.org). A plugin repository is not just a list of files, meta-data information about plugins are expected to be provided by a plugins.json file.
``org.obiba.opal.maxFormContentSize``                    Maximum body size of a HTTP(S) form post request. Default value is ``200000`` bytes.
``org.obiba.opal.ws.messageSizeLimit``                   Limit of the Protobuf message size. Default value is ``524288000`` bytes (500MB).
``org.obiba.magma.entityIdNames``                        Specify the column name per entity type to be used for the entity identifier when exporting data to a file (CSV, SAS, SPSS, Stata). If empty for the considered entity type, the default column name will apply. The format to be used is a comma-separated key-value list, for instance: ``org.obiba.magma.entityIdNames=Participant=Idepic,Biomarker=Biom_Id``
``org.obiba.magma.entityIdName``                         Specify the default column name to be used for the entity identifier when exporting data to a file (CSV, SAS, SPSS, Stata). If empty, this name depends on the file format.
``org.obiba.magma.readDataPointsCount``                  Maximum number of data points (number of rows per number of variables) when batches of values are read from a table. Default value is ``100000``.
``org.obiba.opal.security.multiProfile``                 Allow user to login from different realms with the same username. Note that the user is always logged in one realm at a time (no addition of the privileges). Default value is ``true``.
``org.obiba.opal.security.ssl.allowInvalidCertificates`` When connecting to MongoDB using SSL and when remote certificate is self-signed, the certificate check can be deactivated (not recommended, default is ``false``).
``org.obiba.opal.jdbc.maxPoolSize``                      Maximum size of the pool of JDBC connections, for each SQL database. Default value is ``100``.
``productionMode``                                       When set to ``false`` the CSRF check is disabled and plugin jars conflict checks are skipped. Default value is ``true``.
======================================================== =========================================================================

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

.. _user-dirs:

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
  admin = *

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

Logging
-------

The runtime messages can be configured in the **OPAL_HOME/conf/logback.xml** file. See `Logback documentation <https://logback.qos.ch/documentation.html>`_.

By default, Logback is configured to output files in the **OPAL_HOME/logs** folder. The log files are:

* ``opal.log``, contains the Opal application main log messages,
* ``rest.log``, contains the web services specific log messages,
* ``datashield.log``, contains the DataSHIELD activity log messages,
* ``sql.log``, contains the SQL API specific log messages.

These log files can be downloaded from the web interface (**Administration > Java Virtual Machine > Logs** or **Administration > DataSHIELD > Logs**) or using the `opalr R package <https://www.obiba.org/opalr/>`_.

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

For performance, you can also activate Apache's compression module (requires ``deflate`` module) with the following settings (note the json content type setting) in file */etc/apache2/mods-available/deflate.conf*:

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

Recommended security headers are (to be added to the ``apache2.conf`` file, requires ``headers`` module):

.. code-block:: text

  # Security Headers, see https://securityheaders.com/
  Header set Strict-Transport-Security "max-age=63072000"
  Header set X-Frame-Options DENY
  Header set X-XSS-Protection 1;mode=block
  Header set X-Content-Type-Options nosniff
  Header set Content-Security-Policy "frame-ancestors 'none'"
  Header set Referrer-Policy "same-origin"
  Header set Permissions-Policy "fullscreen=(self)"
  Header onsuccess edit Set-Cookie ^(.+)$ "$1;HttpOnly;Secure;SameSite=Strict"

Proxy Configuration
-------------------

Outbound connections may go through a proxy, depending on the host institution's network setup. It is possible to declare the proxy settings by modifying the ``JAVA_OPTS`` environment variable. As an example:

.. code-block:: sh

    # without authentication
    JAVA_OPTS=-Dhttp.proxyHost=127.0.0.1 -Dhttp.proxyPort=3020 -Xms1G -Xmx8G

    # or with authentication
    JAVA_OPTS=-Dhttp.proxyHost=127.0.0.1 -Dhttp.proxyPort=3020 -Dhttp.proxyUser=opal -Dhttp.proxyPassword=xxxxxx -Xms1G -Xmx8G
