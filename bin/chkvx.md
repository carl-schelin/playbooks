Description: The chkvx script checks the output of vxdisk and vxprint on HP-UX systems for:

* Number of 'Stale' drives.
* Number of 'Failed' drives.
* Number of 'Spares'; error if there aren't 4 spares.
* If data is found on a spare drive

* Location: [server]:/opt/intrado/bin/chkvx
* Data File: [server]:/opt/intrado/etc/chkvx.output
* Validation Script: incojs01:/usr/local/admin/servers/chkvx
* Reporting Script: incojs01:/usr/local/admin/bin/processetc

