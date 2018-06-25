R Server Configuration
======================

R Server Admin package has two configuration files: one for the R server controller and one for the R serv itself.

Controller Configuration
---------------------------------

The file **RSERVER_HOME/conf/application.properties** allows the configuration of the R server controller. This one provides REST web services to start/stop a R server.

=============== ===================
Property        Description
=============== ===================
``server.port``	R server controller port (default is 6312).
``r.exec``	    R executable path, required to launch the R server.
=============== ===================

Rserve Configuration
--------------------

The file **RSERVER_HOME/conf/Rserv.conf** allows the configuration of the core R server. See also `the full documentation of the Rserv.conf file <http://www.rforge.net/Rserve/doc.html#conf>`_.

By default the R server has the following configuration:

* connection port is 6311,
* remote connection is disabled,
* no authentication is required.

If the R server is installed on a different machine as the Opal server, you typically will have to:

* enable remote connection,
* enable authentication.

R Session Configuration
-----------------------

When a new R session is started on server side the starting state of this session can be configured using the **RSERVER_HOME/conf/Rprofile.R**. Any R command (to be executed by the ``rserver`` user) can be put in this file.
