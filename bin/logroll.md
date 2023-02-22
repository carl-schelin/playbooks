Description: The logroll script is HP-UX and OSF1 specific and rolls the logs as noted.

* syslog.log - rolled on Sundays
* rsyncd.log - rolled on Sundays. Files older than 30 days are deleted.
* messages - rolled on Tuesdays.

* Location: [server]:bin/logroll
* HP-UX Log File: [server]:/var/adm/syslog/syslog.log
* HP-UX Log File: [server]:/var/adm/syslog/rsyncd.log
* OSF1 Log File: [server]:/var/cluster/members/{memb}/adm/messages

