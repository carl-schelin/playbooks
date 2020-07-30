## chkghost Script

Description: The **chkghost** script creates the Data File which is then processed by the Web Script to create the Web Page report which identifies all servers with vulnerable glibc-2 libraries.

* Location: [server]:/opt/intrado/bin/chkghost
* Data File: [server]:/opt/intrado/etc/ghost.cve
* Data File: incojs01:/usr/local/admin/servers/[server]/chkghost.output
* Reporting Script: incojs01:/usr/local/admin/bin/processetc
* Web Script: incojs01:/usr/local/admin/bin/showghost
* Web Page: [https://incojs01.scc911.com/reports/ghost.php](https://incojs01.scc911.com/reports/ghost.php)

During the Reporting Script run, the chkghost.output Data File contains the glibc versions.

