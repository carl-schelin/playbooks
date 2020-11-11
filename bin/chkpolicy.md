Description: The chkpolicy script retrieves a list of installed Openview policies on a server. The function is threefold, first to confirm the necessary policies are installed, second to ensure the correct policies are on all servers of a group. For example, the FMCC servers should have the same number of policies for each server. And third, to make sure all policies that should be enabled are enabled.

Note that the Web Page lists several Openview specific items including the number of policies installed and if there are any disabled policies.

As an example, in looking at the HP-UX systems, [node1] and [node2], I see the following:

 [node1]:
 le                "[policy 1]"                enabled    0001.0002

 [node2]:
 le                "[policy 1]"                disabled   0001.0002

I'd be curious about the reasons why it's disabled on node2.

* Location: [server]:bin/chkpolicy
* Data File: [server]:var/chkpolicy.output
* Comparison File: [management server]:admin/servers/[server]/chkpolicy.good
* Difference File: [management server]:admin/servers/[server]/chkpolicy.diff
* Validation Script: [management server]:admin/servers/chkpolicy
* Reporting Script: [management server]:admin/bin/processetc
* Web Script: [management server]:admin/bin/getovfail
* Web Page: https://[management server]/reports/ovfailed.output

This is a comparison script. Comparison scripts don't check for errors in that the output is diverse enough that it would take a great deal of effort to specifically identify the problem without missing another potential problem. The Data File is compared with the Comparison File using the diff utility which creates the Difference File. The output is then manually reviewed using the Validation Script or the Morning Report Dashboard for problems.

Notification: If the Difference File is greater than 0 bytes, the Reporting Script adds a line to the morning.report and config.status files. The config.status file is used to create an overall report which is located in the [management server]:/usr/local/httpd/htsecure/status directory (also https://[management server]/status ). The morning.report file is used by the Morning Report link in the Inventory to display the errors on a dashboard. https://[inventory server]/reports/morning.report.php?group=1&product=0

Validation Process: In the [management server]:admin/servers directory, run the Validation Script. This loops through the admin/etc/servers file, and if the Difference File is greater than 0 bytes, the diff file is displayed for review. Finally the Comparison File is replaced by the Data File so that the following days check can report an error should it occur.

Note that if the Comparison File doesn't exist, then it is the initial review. You would check the full file for any errors before committing it to the Comparison File. Ultimately the intention is for something out of the ordinary to be displayed. It may or may not be an error, just a change in status.

