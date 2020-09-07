Description: The upgrade.groups script uses the list of servers, groups, and members from the group.master file to ensure group membership is centrally managed. This is generally limited to very specific teams but any group can be such managed.

Currently the 'sysadmin/uxadmins' group and the 'webapps/webadmins' group has been approved. Update the group.master file on lnmt1cuomrcs1:/opt/static/intrado/etc/group.master.

The changefreeze flag is in use with this script. If the flag exists, the script exits without making any changes. Changes are documented with an email to changelog.

The script loops through the /etc/group file. The group.master file is checked for the hostname:group setup which will be used along with the members to validate and update the group. Basically it's looking for a couple of substitutions. General groups (current two) are 'sysadmins' and 'webapps' where in Centrify the same groups are 'uxadmins' and 'webadmins'. So there's a second check for that in the group.master file. If not found still, then a general 'centrify' check is made for the group.

* Check for 'group' in 'group.master'
* if not found
** if a Centrify system
*** if group == sysadmins, check for uxadmins
*** if group == webapps, check for webadmins
*** otherwise, no translation is needed, check for Centrify:group
** else not Centrify
*** check for an *:group entry; so any server should have this user list.

This lets us configure a specific system with a modified group listing. Example is incojs01 where Josh Owen is a member of the sysadmins group but shouldn't be a member of sysadmin on any other system.

incojs01:sysadmins:cschelin,kzupan,jnoyes,tcooper,escott,unixsvc,jowen

The script would make sure the sysadmins group on incojs01 matches the above configuration.

Assuming the group was somehow found in the group.master file, the existing GID and group PASSWD is extracted from /etc/group for that group along with the current list of users.

The "group:passwd:gid:grouplist" from /etc/group and group.master is compared. If different, the /etc/group group entry is updated.


* Location: [server]:/opt/intrado/bin/update.groups
* Log File: [server]:/opt/intrado/etc/update.groups.output
* Data File: [server]:/opt/intrado/etc/group.master
* Source Data: lnmt1cuomrcs1:/opt/static/intrado/etc/group.master
* Changefreeze File: [server]:/opt/intrado/etc/changefreeze

