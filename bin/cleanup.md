Description: The cleanup script cleans out old scripts, installation remnants, and retired scripts.

* The Solaris patchdiag, patch management tool was installed in /usr/local/patchdiag. This removes it from the Sun servers.
* The correct motd file is installed in /etc/motd and /etc/issue
* The /tmp/newuser scripts and data files are removed by the cleanup script
* If /usr/bin/ksh doesn't exist and /bin/ksh does, cleanup creates a link between /bin/ksh and /usr/bin/ksh
* cleanup ensures the unixsvc home/.ssh directory is 700/600 and owned by unixsvc
* cleanup removes old var/logfile* files after 10 days
* cleanup removes old var/unixsuite.log* files after 90 days
* The suitecheck runonce script is deleted if found (runnow as well just in case). If the suitecheck script is disabled, this script won't run. This cleans it up.

* Location: [server]:bin/cleanup

