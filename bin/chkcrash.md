## chkcrash Script

Description: The **chkcrash** script checks the crash dump directories for files. Since these can take up quite a bit of space, this is intended to show files exist that need to be reviewed or removed.

* Location: [server]:bin/chkcrash
* Data File: [server]:var/chkcrash.output
* Comparison File: [management server]:admin/servers/[server]/chkcrash.good
* Difference File: [management server]:admin/servers/[server]/chkcrash.diff
* Validation Script: [management server]:admin/servers/chkcrash
* Reporting Script: [management server]:admin/bin/processetc

