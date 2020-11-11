Description: The chkports script uses lsof to generate a list of open ports and the applications that are using them. The intention is to review the output to see if a new port has been added to the system.

* Location: [server]:/opt/intrado/bin/chkports
* Data File: [server]:/opt/intrado/var/lsof.output - Deleted after each script run.
* Data File: [server]:/opt/intrado/etc/chkports.output
* Comparison File: incojs01:/usr/local/admin/servers/[server]/chkports.good
* Difference File: incojs01:/usr/local/admin/servers/[server]/chkports.diff
* Validation Script: incojs01:/usr/local/admin/servers/chkports
* Reporting Script: incojs01:/usr/local/admin/bin/getports

This is a comparison script. Comparison scripts don't check for errors in that the output is diverse enough that it would take a great deal of effort to specifically identify the problem without missing another potential problem. The Data File is compared with the Comparison File using the diff utility which creates the Difference File. The output is then manually reviewed using the Validation Script or the Morning Report Dashboard for problems.

Notification: If the Difference File is greater than 0 bytes, the Reporting Script adds a line to the morning.report and config.status files. The config.status file is used to create an overall report which is located in the [management server]:/usr/local/httpd/htsecure/status directory (also https://[management server]/status ). The morning.report file is used by the Morning Report link in the Inventory to display the errors on a dashboard. https://[inventory server]/reports/morning.report.php?group=1&product=0

Validation Process: In the [management server]:admin/servers directory, run the Validation Script. This loops through the admin/etc/servers file, and if the Difference File is greater than 0 bytes, the diff file is displayed for review. Finally the Comparison File is replaced by the Data File so that the following days check can report an error should it occur.

Note that if the Comparison File doesn't exist, then it is the initial review. You would check the full file for any errors before committing it to the Comparison File. Ultimately the intention is for something out of the ordinary to be displayed. It may or may not be an error, just a change in status.

