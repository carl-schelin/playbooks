### Overview ###

This section is for all the tasks when a new server is built plus ensure some common bits are in place

### issue and motd ###

Per the man page for /etc/issue, this file is displayed at the login prompt to all users.

Per the man page for /etc/motd, this file is displayed after a user has logged but before the shell is activated.

As such, the sshd_config file should have the following settings:

* Banner /etc/issue
* PrintMotd yes


### Exceptions ###

For Solaris servers, the /etc/profile script is run which displays the /etc/motd file after a user logs in. As such, the sshd_config file has these options:

* Banner /etc/issue
* PrintMotd no


For servers that are running Centrify, 


