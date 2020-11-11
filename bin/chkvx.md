Description: The chkvx script checks the output of vxdisk and vxprint on HP-UX systems for:

* Number of 'Stale' drives.
* Number of 'Failed' drives.
* Number of 'Spares'; error if there aren't 4 spares.
* If data is found on a spare drive

* Location: [server]:bin/chkvx
* Data File: [server]:var/chkvx.output
* Validation Script: [management server]:admin/servers/chkvx
* Reporting Script: [management server]:admin/bin/processetc

