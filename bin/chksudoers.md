Description: The chksudoers script processes all entries in the sudoers file, comparing entries to the group and passwd files to identify users who are members of any group that has a sudoers configuration associated with it and to identify users who have privileged access. This includes gathering information from Centrify.

Important! The script has a dependencies on the output of chkusers (chkusers.dat).

* Location: [server]:/opt/intrado/bin/chksudoers 
* Data File: [server]:/opt/intrado/etc/chksudoers.output
* Data File: [server]:/opt/intrado/etc/chksudoers.dat
* Comparison File: incojs01:/usr/local/admin/servers/[server]/chksudoers.good
* Difference File: incojs01:/usr/local/admin/servers/[server]/chksudoers.diff
* Validation Script: incojs01:/usr/local/admin/servers/chksudoers
* Reporting Script: incojs01:/usr/local/admin/bin/processetc

This is a comparison script. Comparison scripts don't check for errors in that the output is diverse enough that it would take a great deal of effort to specifically identify the problem without missing another potential problem. The Data File is compared with the Comparison File using the diff utility which creates the Difference File. The output is then manually reviewed using the Validation Script or the Morning Report Dashboard for problems.

Notification: If the Difference File is greater than 0 bytes, the Reporting Script adds a line to the morning.report and config.status files. The config.status file is used to create an overall report which is located in the incojs01:/usr/local/httpd/htsecure/status directory (also https://incojs01.scc911.com/status ). The morning.report file is used by the Morning Report link in the Inventory to display the errors on a dashboard. https://incojs01.scc911.com/inventory/reports/morning.report.php?group=1&product=0

Validation Process: In the incojs01:/usr/local/admin/servers directory, run the Validation Script. This loops through the /usr/local/admin/etc/servers file, and if the Difference File is greater than 0 bytes, the diff file is displayed for review. Finally the Comparison File is replaced by the Data File so that the following days check can report an error should it occur.

Note that if the Comparison File doesn't exist, then it is the initial review. You would check the full file for any errors before committing it to the Comparison File. Ultimately the intention is for something out of the ordinary to be displayed. It may or may not be an error, just a change in status.

Pseudocode:

# Set script variables
# Determine the location of the sudoers file.
# Remove data file if it exists
# Process sudoers looking for users who are members of the TMPROOT alias (since deprecated and deleted)
## Loop through the sudoers file looking for User_Alias
## Check to see if any of the users are members of TMPROOT
### Set status; yes if a member, no otherwise
## Grab whether the user is active (not locked) and get user details for report
# Process the sudoers file looking for Cmnd_Alias with root privileges 
## Loop through the sudoers file looking for Cmnd_Alias with su - or su
## Capture the name of the Cmnd_Alias that has root privs in a regex string
# Process the sudoers file parsing out the names of all groups for who has root privs
## Loop through sudoers capturing all group names
### Loop through the userlist for each group
### If the group is a member of a Cmnd_Alias with root privs, identify the user as having root privs
### Loop through the passwd file getting user GIDs
### If a user is a default member of group with a Cmnd_Alias with root privs, identify the user has having root privs
# Last step is to sort | uniq the file.

