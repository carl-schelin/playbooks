## chkbackups Script

Description: System backups are a critical part of the server infrastructure. While the team can get reports from the Backup Team when there are problems with backups, they won't know about systems that they weren't told about.

The **chkbackups** script verifies that the Netbackup agent is installed and then runs a command against the agent and the media server to retrieve a report of the last time a backup occurred.

* Location: [server]:bin/chkbackups
* Data File: [server]:var/backups.output
* Reporting Script: [management server]:admin/bin/processetc
* Web Page Script: [management server]:admin/bin/showbackups
* Web Page: https://[management server]/reports/backups.html
* No error is recorded with this script.

The Web Page provides a snapshot of the current status of backups.

The Report by column:

* List of all servers
* An @ if a /usr/openv/netbackup/bp.conf file was found, the assumption being backups are expected to run
* The network zone. Note that no backups occur in the DMZ.
* The first SERVERS entry. This must be the FQDN of the backup server. The report does trim it to be the hostname though.
* The date of the last backup from the backups.output file
* The remainder columns provide additional detail about the backup.

Notes:

* The **chkservers** script will check the status of netbackup, using the **backups.output** file to report if a backup has not occurred or has occurred prior to the 7 days ago in case a server is a once a week, full backup server vs a daily backup server.
* The **chkservers** script validates the bp.conf configuration, checking for FQDN, the correct media servers, and the expected CLIENT_NAME.

