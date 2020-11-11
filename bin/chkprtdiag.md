Description: The chkprtdiag script runs the prtdiag command in order to get a status of Solaris systems. This report lists system specs plus reports if there are outages such as a fan failure. Review the output for changes in status indicating a warning or failure. The status of the lights are also displayed; color and if it's on or off.

* Location: [server]:/opt/intrado/bin/chkprtdiag
* Data File: [server]:/opt/intrado/etc/prtdiag.output
* Comparison File: incojs01:/usr/local/admin/servers/[server]/prtdiag.good
* Difference File: incojs01:/usr/local/admin/servers/[server]/prtdiag.diff
* Validation Script: incojs01:/usr/local/admin/servers/chkprtdiag
* Reporting Script: incojs01:/usr/local/admin/bin/processetc

This is a comparison script. Comparison scripts don't check for errors in that the output is diverse enough that it would take a great deal of effort to specifically identify the problem without missing another potential problem. The Data File is compared with the Comparison File using the diff utility which creates the Difference File. The output is then manually reviewed using the Validation Script or the Morning Report Dashboard for problems.

Notification: If the Difference File is greater than 0 bytes, the Reporting Script adds a line to the morning.report and config.status files. The config.status file is used to create an overall report which is located in the [management server]:/usr/local/httpd/htsecure/status directory (also https://[management server]/status ). The morning.report file is used by the Morning Report link in the Inventory to display the errors on a dashboard. https://[inventory server]/reports/morning.report.php?group=1&product=0

Validation Process: In the [management server]:admin/servers directory, run the Validation Script. This loops through the admin/etc/servers file, and if the Difference File is greater than 0 bytes, the diff file is displayed for review. Finally the Comparison File is replaced by the Data File so that the following days check can report an error should it occur.

Note that if the Comparison File doesn't exist, then it is the initial review. You would check the full file for any errors before committing it to the Comparison File. Ultimately the intention is for something out of the ordinary to be displayed. It may or may not be an error, just a change in status.

