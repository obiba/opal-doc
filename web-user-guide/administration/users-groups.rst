Users and Groups
================

Opal has its own user directory, accessible from the users and groups administration page.

Users
-----

There two types of user in Opal, depending on the way they are authenticated:

- by password: this is the most standard way, allowing a physical user to connect to the web interface,
- by certificate: this is convenient when an application needs to connect to Opal server. This only works when connecting to Opal through **https**; Opal identifies the user by comparing the received certificate with the registered one and encrypts in return the communication with this certificate. Only a remote client having the corresponding private key (not known by Opal) will be able to decrypt the response. For more information see Client-authenticated TLS handshake documentation. In order to have this handshake to work, the SSL headers must not be altered by proxies, firewall or load balancers that could be between the client application and the Opal server.

Groups
------

A group is just a group of users, i.e. no group can be created without users.

Operations
----------

Add User with Password
~~~~~~~~~~~~~~~~~~~~~~

At least 6 characters are required for the user password. After a user has been added, a personal folder is added in the home folder of the Opal's :ref:`file-system`.

Add User with Certificate
~~~~~~~~~~~~~~~~~~~~~~~~~

The user `X.509 <https://en.wikipedia.org/wiki/X.509>`_ certificate (or public key) must be provided in `PEM <https://en.wikipedia.org/wiki/Privacy-enhanced_Electronic_Mail>`_ format.

Edit User
~~~~~~~~~

Change password or X.509 certificate or group membership.

Remove User
~~~~~~~~~~~~

Remove a user and all the permissions that could have been granted to this user. The home folder of this user (located at the path /home/<user
name> in Opal's file system is untouched).


Disable User
~~~~~~~~~~~~

User and its associated permissions are still available but user cannot login anymore.


Remove Group
~~~~~~~~~~~~

Removing a group consist of excluding associated users from this group.