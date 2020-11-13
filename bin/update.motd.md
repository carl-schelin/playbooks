Description: The update.motd script recreates both the /etc/issue and the /etc/motd file each night.

Note that the /etc/issue file is displayed to the user prior to displaying a login prompt. For this reason, a message noting if the system 
is under IDM management.

Note that the /etc/motd (or Message of the Day) file is displayed after the user has successfully logged in. The additional information located 
in the /etc/motd file is then provided.

The script first replaces the existing /etc/issue file with the approved warning about accessing the server. If the users on the server are 
managed under IDM. a short message is added to the /etc/issue file noting that for user.

The script then queries the system, parses the fingerprint file, and parses the chksys.import file to gather information which then creates 
a block of information which is displayed to users who log in. It provides the following information:

    =======================================================================
    Name: HOSTNAME                                           Status: Active
    Location: LOCATION                                   Network Zone: ZONE
    Product: PRODUCT                                       Project: PROJECT
    Service Class: SERVICE CLASS                          911 Call Path: No
    System Custodian:                                      SYSTEM CUSTODIAN
    Primary Application Custodian:                    APPLICATION CUSTODIAN

    OS Version: CentOS Linux release 8.2.2004 (Core)
    RAM: 3868932 kB
    CPU: 2x Intel(R) Xeon(R) CPU X5680 @ 3.33GHz, 1 core
    Disks(s): 40 GiB
    Interface: ens192 192.168.101.55/24 (00:50:56:b3:4b:b6)
    Interface: noprefixroute fe80::7ec5:38f6:4949:e80c/64 (00:50:56:b3:4b:b6)
    =======================================================================

In addition, for a system where the OS or underlying Hardware has reached End of Life/End of Support, a warning is displayed for 
one or both depending on the status.

If a changefreeze (file exists) is in effect, the script exits without checking. A changelog is sent only when a record is updated.

* Location: [server]:bin/update.motd
* Data File: [server]:etc/motd
* Data File: [server]:etc/fingerprint
* Data File: [server]:var/chksys.import
* Changefreeze File: [server]:etc/changefreeze

