Description: The cleanup script cleans out old scripts, installation remnants, and retired scripts.

* Scripts were installed in /usr/local/bin with output in /usr/local/etc. It was changed to /opt/intrado when the number of scripts installed and in cron got too unwieldy. cleanup cleans out the old scripts if they still exist.
* cfg2html was originally installed in /opt/cfghtml. With the /opt/intrado creation, cfg2html is now in /opt/intrado/cfghtml. If found in the old directory, cleanup moves it to the right directory.
* cleanup removes the  /opt/ov directory but only if Openview is installed (/opt/OV/bin/ovc exists)
* cleanup removes the /opt/nbu directory but only if Netbackup is installed (/usr/openv/netbackup/bp.conf exists)
* The chkov openview.failed log file was in /var/tmp. This moves it to the correct /opt/intrado/var directory
* The Solaris patchdiag, patch management tool was installed in /usr/local/patchdiag. This removes it from the Sun servers.
* The correct motd file is installed in /etc/motd and /etc/issue
* The newuser scripts and data files are removed by the cleanup script
* If /usr/bin/ksh doesn't exist and /bin/ksh does, cleanup creates a link between /bin/ksh and /usr/bin/ksh
* cleanup ensures the unixsvc home/.ssh directory is 700/600 and owned by unixsvc
* cleanup removes old /opt/intrado/var/logfile* files after 10 days
* cleanup removes old /opt/intrado/var/intrado.log* files after 90 days
* The chkov runonce script is deleted if found (runnow as well). If the chkov script is disabled, this script won't run. This cleans it up.
* Removes retired scripts
* Removes retired script output files

* Location: [server]:/opt/intrado/bin/cleanup

