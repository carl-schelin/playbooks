Description: The chksys script is a general data gathering script used to ensure the Inventory has accurate and current information about a server. The following data is gathered and imported, in order:

* Timezone (All)
* Kernel installation date (All)
* List of CPUs (All)
* Installed RAM (All)
* List of configured storage (Linux)
* System UUID (Linux, Solaris)
* Installed software and version information:
** Data Palette
** HTTPD
** Informix
** MySQLd
** Netbackup
** NewRelic
** OpNet
** Oracle
** Openview (ovc)
** Postgres
** sudo
** VMToolsd
** Wildfly
* Operating System
* Centrify; Year, Zone, and Domain
* Route Table
* Network Interfaces
* Filesystem Layout
* Resolver Information

* Location: [server]:bin/chksys
* Data File: [server]:var/chksys.import
* Reporting Script: [management server]:/usr/local/httpd/bin/import.php
* Version Script: [server]:bin/chkversion
* Version Data File: [server]:var/[software].version

