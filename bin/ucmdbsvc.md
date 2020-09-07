Description: The ucmdbsvc script ensures the ucmdbsvc account has a .ssh directory in the account home directory, the directory has appropriate permissions, and installs the appropriate authorized_keys file which is created from the ucmdbsvc.id_rsa.pub file, which was provided by the Monitoring team.

The ucmdb account is used by the Monitoring Team to sudo run several commands as listed in order to populate their UCMDB tool:

* /bin/netstat
* /usr/sbin/lsof
* /usr/sbin/ifconfig
* /usr/sbin/dmidecode

* Location: [server]:/opt/intrado/bin/ucmdbsvc
* Data File: [server]:/opt/intrado/etc/ucmdbsvc.id_rsa.pub

