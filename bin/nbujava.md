Description: The nbujava script checks to see if a changefreeze is in effect and bails if true. Then on Linux systems only, checks to see if VRTSnbjava, a Netbackup Java web page, is installed and removes it if so. Then sends a changelog and restarts vxpbx_exchanged.

Note that this is being done to satisfy a Vulnerability Scan issue regarding Java being installed by Netbackup.

* Location: [server]:bin/nbujava
* Flag File: [server]:etc/changefreeze

