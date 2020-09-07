Description: The simplejson script is used to install the python simplejson binaries onto the Red Hat 5 servers where the binaries are missing.

Ansible requires json in order to properly function. There are full packages that are normally available and installed however the simplejson packages were only available on newer point releases of RHEL5.

Note that if there is a changefreeze, the changefreeze file is created and this script will exit.

Changes will also send out a changelog email.

* Location: [server]:/opt/intrado/bin/simplejson
* Data File: [server]:/opt/intrado/etc/changefreeze
* Data File: [server]:/opt/intrado/etc/python-simplejson-2.0.9-8.el5.i386.rpm
* Data File: [server]:/opt/intrado/etc/python-simplejson-2.0.9-8.el5.x86_64.rpm

