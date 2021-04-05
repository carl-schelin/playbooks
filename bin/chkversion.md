Description: The chkversion script attempts to determine the version of known software on the server and writes to a software specific version file. This information is used by the chksys data import script to build the installed software for the Inventory.

Software currently checked and target file:

* HTTPD - httpd.version
* Informix - informix.version
* MySQLd - mysqld.version
* Open Manage - omsa.version
* OpNet - opnet.version - Only notes that it's installed.
* Oracle - oracle.version - This is a list of all schema's that are running on the system.
* Postgres - postgres.version
* Sudo - sudo.version
* VMtoolsd - vmtoolsd.version
* Wildfly - wildfly.version - Only notes that it's installed.

* Location: [server]:bin/chkversion
* Data File: [server]:var/[software].version
* Reporting Script: [server]:bin/chksys

Note that I worked with SCM several years back to create a deployed software version file for products. At this time, I'm not importing that information but it is planned.

