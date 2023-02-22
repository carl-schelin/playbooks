Description: The lockuser script is used to lock user accounts using system based utilities after a user has left the company.

Important Note: Make sure you don't add people who have simply moved to a different team or department.

* Location: [server]:bin/lockuser
* Data File: [server]:etc/lockuser.dat
* Output File: [server]:var/locked.output
* Output File: [server]:var/lockuser.output
* Log File: [server]:var/lockuser.log
* Validation Script: admin directory, bin/processetc

The lockuser script works as follows:

* If a system managed by Centrify, exits the script
* Extracts the user information from the lockuser.dat file
* Verifies the correct user has been found
* If the uid is <= 100, exits assuming a system account
* If the user is a Unix Admin, the script exits
* If the user is already locked, exit script
* Otherwise locks the user
* Removes the user from all groups. Exception for HP-UX, user is left in the users group

The lockuser.dat file contains a list of users:

* [hostname | *] - The hostname where the user needs to be locked. Using an asterisk will lock the user on all systems where the script runs.
* [username] - The username to be locked
* [email] - For verification to ensure the correct user is locked

The locked.output file contains a list of users that were locked.

The lockuser.output file message is that a passwd binary wasn't found in the path.

The lockuser.log file lists the date of the check and the list of groups the user was removed from.

