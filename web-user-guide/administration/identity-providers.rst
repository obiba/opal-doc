.. _oidc:

Identity Providers
==================

Definition
----------

`Identity Providers <https://en.wikipedia.org/wiki/Identity_provider>`_ are user registries that can be used to signin users into Opal. The
`OpenID Connect <https://en.wikipedia.org/wiki/OpenID_Connect>`_ protocol is used to perform the authentication delegation: Opal has no access
to user credentials, only basic user information is retrieved. An example of open source identity provider is `Keycloak <https://www.keycloak.org/>`_.

The only requirement is that the Identity Provider server exposes an OpenID Connect configuration discovery entry point. Usually it takes the form of:
`https://auth.example.org/.well-known/openid-configuration` (see `Google Accounts <https://accounts.google.com/.well-known/openid-configuration>`_ or
`ORCID <https://orcid.org/.well-known/openid-configuration>`_ examples).

Personal Access Tokens
----------------------

Because of the redirect of the user to the original OpenID Connect server login page, this authentication realm is not suitable for scripting/command line tools such as R, Python etc. The solution for a user defined in that kind of realm is to create one or more personal API access tokens (see :ref:`my-profile`) to perform authentication in scripting clients.

Operations
----------

Add ID Provider
~~~~~~~~~~~~~~~

Open a form dialog to specify the connection details to the ID provider.

There are some required fields:

* An ID provider must be identified by a *Name*,
* The Opal application has been registered in the this provider: these are the *Client ID* and *Client Secret* fields.
* The *Discovery URI* must follow the `OpenID Connect configuration discovery specifications <https://openid.net/specs/openid-connect-discovery-1_0.html#ProviderConfig>`_.

The optional fields are:

* *Label* is a human-readable name that will be displayed in the provider's signin button in the login page. If missing, the name of the ID provider will be used.
* *Account Login* address allows the user to go to it's personal profile page in the ID provider interface (to chenge its password for instance) from the Opal login page.
* *Groups* are the group that are to be automatically applied to any users signing in through this ID provider.
* *Scope* is the scope value(s) to be sent to the ID provider to initiate the OpenID Connect dialog. This is provider dependent but usually ``openid`` is enough.
* *Username Mapping* is an optional field name in the `UserInfo <https://openid.net/specs/openid-connect-core-1_0.html#UserInfo>`_ object which value will represent the Opal user name.
* *Groups Mapping by Claim value* is an optional field name in the `UserInfo <https://openid.net/specs/openid-connect-core-1_0.html#UserInfo>`_ object (that is returned by the ID provider) that contains the group names to which the user belongs. These will be automatically applied to the user's profile. Such field is `not one of the standard claims <https://openid.net/specs/openid-connect-core-1_0.html#StandardClaims>`_ and needs to be explicitly set. The expected value type associated to this claim is either an array of strings, or a string which group names are separated by spaces (or commas). In the case of Agate, the groups claim name is ``groups``.
* *Groups Mapping by Javascript* is an optional Javascript code chunk that will process the `UserInfo <https://openid.net/specs/openid-connect-core-1_0.html#UserInfo>`_ object to extract a group name or an array of group names to which the Opal user will belong.

More advanced options are:

* *Nonce* to validate ID token with `Nonce <https://openid.net/specs/openid-connect-core-1_0.html#IDToken>`_. Uncheck this option when Agate is used as a ID provider.
* *Connect Timeout* is the maximum time to wait before a connection is established, in milliseconds. Zero implies no timeout (default).
* *Read Timeout* is the maximum time to wait before a response is received, in milliseconds. Zero implies no timeout (default).
* *Public URL*, in case Opal is accessible from different public URLs, it is possible to specify which one is to be used for this ID provider. When not specified, the system's public URL applies. Note that this ID provider will be only visible when Opal base URL matches this public URL.

.. note::

  To register Opal as a client of the OIDC provider it will be necessary to provide its callback URL which is: ``https://opal.example.org/auth/callback/``.

Remove
~~~~~~

Remove the ID provider. This does not affect the user profiles that may have been created through this provider and this does not remove the permissions
specific to this provider that may have been applied.

Edit
~~~~

Open the ID provider form dialog. Name cannot be changed (see *Duplicate* operation instead).

Enable
~~~~~~

On creation an ID provider is disabled, which means that the corresponding Signin button is not shown in the login page.

Duplicate
~~~~~~~~~

Open an ID provider form dialog prefilled with the original provider's values (except for the name).
