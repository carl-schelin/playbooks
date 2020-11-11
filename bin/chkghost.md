## chkghost Script

Description: The **chkghost** script creates the Data File which is then processed by the Web Script to create the Web Page report which identifies all servers with vulnerable glibc-2 libraries.

* Location: [server]:bin/chkghost
* Data File: [server]:etc/ghost.cve
* Data File: [management server]:admin/servers/[server]/chkghost.output
* Reporting Script: [management server]:admin/bin/processetc
* Web Script: [management server]:admin/bin/showghost
* Web Page: https://[management server]/reports/ghost.php

During the Reporting Script run, the chkghost.output Data File contains the glibc versions.

