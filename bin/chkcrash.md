## chkcrash Script

Description: The **chkcrash** script checks the crash dump directories for files. Since these can take up quite a bit of space, this is intended to show files exist that need to be reviewed or removed.

* Location: [server]:/opt/intrado/bin/chkcrash
* Data File: [server]:/opt/intrado/etc/chkcrash.output
* Comparison File: incojs01:/usr/local/admin/servers/[server]/chkcrash.good
* Difference File: incojs01:/usr/local/admin/servers/[server]/chkcrash.diff
* Validation Script: incojs01:/usr/local/admin/servers/chkcrash
* Reporting Script: incojs01:/usr/local/admin/bin/processetc

