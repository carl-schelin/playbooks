Description: The chkraid script creates a data file for each of the raid management tools it is configured to monitor. This is used to identify raid devices that have failed to ensure a sysadmin is aware.

Depending on the operating system, the script retrieves the output from the following binaries:

* metastat - Solaris Disk Suite
* metadb - Solaris Disk Suite
* megarc - Megaraid Controller
* arcconf - Adaptec Controller
* raidctl - LSI Controller
* hpacucli - HP Controller
* hpssacli - HP Super Smart Array Controller
* sautil - HP Smart Array Controller
* omreport - Dell Open Manage utility

Various flags are set depending on the binary being checked. Note that if more than one utility is found, only the last one will be used to generate output.

* Location: [server]:/opt/intrado/bin/chkraid
* Data File: [server]:/opt/intrado/etc/[binary].output
* Comparison File: incojs01:/usr/local/admin/servers/[server]/[binary].good
* Difference File: incojs01:/usr/local/admin/servers/[server]/[binary].diff
* Validation Script: incojs01:/usr/local/admin/servers/chk[binary]
* Reporting Script: incojs01:/usr/local/admin/bin/processetc

This is a comparison script. Comparison scripts don't check for errors in that the output is diverse enough that it would take a great deal of effort to specifically identify the problem without missing another potential problem. The Data File is compared with the Comparison File using the diff utility which creates the Difference File. The output is then manually reviewed using the Validation Script or the Morning Report Dashboard for problems.

Notification: If the Difference File is greater than 0 bytes, the Reporting Script adds a line to the morning.report and config.status files. The config.status file is used to create an overall report which is located in the incojs01:/usr/local/httpd/htsecure/status directory (also https://incojs01.scc911.com/status ). The morning.report file is used by the Morning Report link in the Inventory to display the errors on a dashboard. https://incojs01.scc911.com/inventory/reports/morning.report.php?group=1&product=0

Validation Process: In the incojs01:/usr/local/admin/servers directory, run the Validation Script. This loops through the /usr/local/admin/etc/servers file, and if the Difference File is greater than 0 bytes, the diff file is displayed for review. Finally the Comparison File is replaced by the Data File so that the following days check can report an error should it occur.

Note that if the Comparison File doesn't exist, then it is the initial review. You would check the full file for any errors before committing it to the Comparison File. Ultimately the intention is for something out of the ordinary to be displayed. It may or may not be an error, just a change in status.

