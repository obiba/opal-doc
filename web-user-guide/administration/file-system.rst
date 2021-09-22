.. _file-system:

File System
===========

Opal has its own file system accessible from the Dashboard, a project and the Files administration page.

File Browser
------------

The file browser consists of two parts: folder shortcuts on the left and directory/file listing on the right. The default location is the current user's home folder.

Operations
----------

An administrator can perform the following operations on all folders whereas a user with limited privileges can only perform them in the user's home directory.

Add Folder
~~~~~~~~~~

Adds a new sub-folder in the current location.

Upload
~~~~~~

Uploads a file in the current location.

Download
~~~~~~~~

Downloads the selected files and folders to the user's computer. If there are more than one file or directory selected, a ZIP containing all of them is downloaded to the user's computer.

.. note::
 A zip file can be password protected to secure the downloaded data.

Delete
~~~~~~~~~~~~

Deletes the selected files and folders from the current location.

SFTP
~~~~

Users can securely access Opal's file system using SFTP with any third-party tools such as FileZilla or the Firefox add-on FireFTP. Information required to configure FileZilla:

- Host: IP or the host name where the Opal server is running
- Protocol: SFTP
- Port: 8022 (In case of a firewall, this port must be accessible to the client)
- Logon Type: Normal (requires a valid username and password)
