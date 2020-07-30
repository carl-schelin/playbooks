## chkserver Script

Description: The **chkserver** script checks numerous parts of the system to ensure the server is properly configured and ready to go into production. 
The output can be parsed to review errors either on system or by using the **chkstatus** script located on the admin server.

* Location: [server]:/opt/intrado/bin/chkserver
* Config File: [server]:/opt/intrado/.config
* Data Input: lnmt1cuomrcs1:/opt/static/intrado/etc/chkserver.merge
* Data Input: [server]:/opt/intrado/etc/chkserver.input
* Merge Script: incojs01:/export/home/unixsvc/chkserver/process
* Data Output: [server]:/opt/intrado/etc/chkserver.output
* Supporting Script: incojs01:/usr/local/admin/bin/chkstatus
* Extract Script: incojs01:/usr/local/httpd/bin/login.report.php
* Validation Script: [server]:/opt/intrado/bin/profile
* Central Validation Script: incojs01:/opt/intrado/bin/profile - Note that you would pass a servername to the script and it would load the profile info from the /usr/local/admin/servers/[servername]/chkserver.output file.
* Email List: [server]:/opt/intrado/etc/intrado.email
* Priority Management Dashboard: https://incojs01.scc911.com/inventory/manage/errors.php
* Overall chkserver Dashboard: https://incojs01.scc911.com/inventory/manage/manage.php
* Group Input: [server]:/opt/intrado/etc/group.master
* Backup Input: [server]:/opt/intrado/etc/backups.output
* Exclude File: [server]:/opt/intrado/etc/chkserver.exclude
* Privileged File: [server]:/opt/intrado/etc/chksuders.output
* Privileged Management File: [server]:/opt/intrado/etc/chksudo.dat
* Route Table: [server]:/opt/intrado/etc/routeable.output
* Security Data: [server]:/opt/intrado/etc/chksecurity.output
* Exclude File: [server]:/opt/intrado/etc/chkserver.exclude
* Openview Completed File: [server]:/opt/intrado/etc/chkopenview.completed
* Openview Blocked File: [server]:/opt/intrado/etc/chkopenview.block

The .config file contains the configuration used by this script. You also have the ability to disable checks within the .config file.

The chkserver.input file is used by chkserver to validate a server configuration.

* The chkserver.merge file is a manually edited configuration file where you can add extra bits such as missing servers or information that isn't part of RSDP just yet.
* Extract Script pulls server configuration information from RSDP in the Inventory and writes to STDOUT
* The Merge Script combines the output of the Extract Script with the chkserver.merge file to create a final chkserver.input file.
* The chkserver.exclude file is used to overwrite default configuration checks. For example, standard swap is == RAM up to 8G. Kubernetes workers are configured to 0G swap. To skip the error for 0G, a [server]:Swap:0 line is added. If it's not 0, it errors though.

The chkserver script checks two aspects of the server configuration.

* The chkserver.input file is processed to verify the server configuration
* The script also checks the default server configuration

The following are the list of chkserver.input keywords:

Server:Keyword:Value[0]:Value[1]:...

* Server - the server hostname to be checked or * if the rule is applied to all servers.
* Keyword. The following keywords are available:
  * Centrify
    * Centrify is installed on the server.
  * CPU
    * Value[0] is the expected number of CPUs for the system.
  * Cron
    * The Value[0] account is allowed to use cron.
  * Datapalette
    * Datapalette is installed on the server.
  * Disk - Not processed.
  * Enabled - Linux only
    * Value[0] service is enabled.
  * Group
    * Value[0] is a valid group on the system.
  * Hostname
    * Value[0] is the hostname of the system.
  * InterfaceMonitored
    * Value[0] Interface identified as the Management Interface.
  * IP
    * Value[0] IP is assigned to an interface on the system.
  * IPAddressMonitored
    * Value[0] is the IP address that is monitored.
  * Location
    * Value[0] is the West 5 character Data Center designation
  * Memory
    * Value[0] is the expected amount of RAM for the system
  * MonitoringServer
    * Value[0] is the name of the Openview monitoring server
  * Netbackup
    * Netbackup is installed on the server.
  * NetworkZone
    * Value[0] is the network zone (Corp, E911, DMZ, Lab).
  * Openview
    * Openview is installed on the server.
  * OpNet
    * OpNet is installed on the server.
  * Running
    * Value[0] service is running.
  * Service
    * Value[0] service account is an account on the system.
    * Password expires.
    * Account expires.
    * nginx verify log permissions
    * nginx verify sudoers rules
  * Sudoers
    * Value[0] group is in the sudoers file.
    * sudoers file exists.

The following checks are run against all servers:

  * check_active_employees()
    * Checks all valid user email addresses against the intrado.email data file and returns an error if missing. Valid == Not Locked and Not a Service Account.
  * check_apa()
    * Comparison check of chkapa.review and chkapa.valid
  * check_artifactory()
    * Checks to see if servers are pingable
    * Checks to see if server ports are accessible
  * check_centrify()
    * Is Centrify installed?
    * Is Centrify running?
    * Is the server connected to a domain?
  * check_cfg2html()
    * Is it installed?
    * Did it run?
  * check_config_addresses()
    * Linux Only
    * Ensures the onboot value == yes
    * Ensures the IP is in /etc/hosts
    * Checks Value[1] to see if it is routeable
    * Checks Value[1] to see if it's in /etc/sysconfig/network
  * check_config_centrify()
    * Verifies that Centrify is installed
  * check_config_cpus()
    * Does the number of CPUs match Value[0]
  * check_config_cron()
    * Does Value[1] have permission to use cron
  * check_config_datapalette()
    * Verifies that Data Palette is installed
  * check_config_disable()
    * Checks chkserver.exclude for the service as enabled and exits the function if it does
    * Verifies that service Value[2] is disabled
  * check_config_enabled()
    * Verifies that service Value[2] is enabled
  * check_config_group()
    * Verifies that Value[1] group is a valid group
  * check_config_memory()
    * Verifies the amount of RAM that's supposed to be in the system. On VMs, there is a bit of overhead so large amounts of RAM return slightly less RAM. Add the correct amount to the Merge file.
  * check_config_netbackup()
    * Verifies that NetBackup is installed
  * check_config_openview()
Verifies that Openview is installed
  * check_config_opnet()
Verifies that OpNet is installed
  * check_config_running()
Verifies that Value[1] service is running
  * check_config_service()
    * Verifies that a specific service account exist
    * Checks to make sure the account doesn't expire
    * Checks to make sure the account password doesn't expire
    * If an nginx service account
      * Checks the log rotation configuration
      * Checks the log permissions
      * Checks the log rights
  * check_config_sudoers()
    * Checks the sudoers file to make sure Valid[1] is a defined group
  * check_crash()
    * Are there crash dump files?
  * check_datapalette()
    * Is it installed?
    * Is it running?
    * Are the Nerve Centers pingable?
    * Are the Nerve Centers accessible via their designated port?
  * check_default_gateway()
    * Linux only
    * Reports if the default gateway is not in the network file
  * check_default_passwords()
    * Is root's password still set to default?
    * Is unixsvc's password still set to default?
    * Are any sysadmin's password still set to default?
  * check_defunct_processes()
    * Report if more than zero defunct processes.
  * check_disk_space()
    * Has a file system exceeded 85%?
    * Has a file system exceeded 95%?
  * check_disk_suite()
    * Is metadb showing any errors?
    * Is metastat showing any errors?
  * check_eeprom()
    * Is the auto-boot? flag set to false?
  * check_email()
    * Are the email servers pingable?
    * Are the email servers accessible via their designated port?
  * check_floppy() (not checked)
    * Does /dev/fd exist?
  * check_group_membership()
    * Is a standard group installed? A group name for a department has a standard name such as webapps or sysadmin.
    * Is a non-standard group installed? A group name that has been created for a department but which isn't standard (webadmin instead webapps for example).
    * Report if a standard group user doesn't have access to the server. Example: kstratford is a DBA but doesn't have an account on a server will report an error.
    * Report if a standard group user exists but isn't a member of the standard group. Example: kstratford is a DBA and has a login but isn't a member of the dbadmins standard group will be reported as an error.
    * Report if a user is a member of a standard group who shouldn't be in the group. Example: dlivingston was a DBA and is still a member of the dbadmins standard group will be reported as an error.
  * check_guid()
    * Comparison of chkguid.review and chkguid.valid.
  * check_hostname()
    * Checks to make sure hostname is in /etc/hosts.
  * check_interfaces()
    * Report if a FAILED interface is found.
  * check_intrado()
    * Report if the intrado script hasn't run.
    * Report if the intrado script isn't active in root's cron.
  * check_ksh()
    * Report if /usr/bin/ksh doesn't exist.
  * check_kubernetes()
    * Verify that etcd is healthy.
    * Verify that the apiserver is healthy.
    * Verify that a node is healthy.
    * Verify the status of all running pods.
  * check_logs()
    * Reports if there are no log entries for the day.
  * check_lsof() (not checked)
    * Returns the number of deleted processes. Intended to identify systems where log files were deleted but no properly rolled but deleted is pretty common so disabled for the moment.
  * check_management()
    * Is a management server pingable?
    * Is a management server accessible via their designated port?
  * check_netbackup()
    * If Netbackup version 6, verify the /etc/hosts.allow file is properly configured.
    * Is the correct route in place for the netbackup server?
    * Is the netbackup server pingable?
    * Is the netbackup server accessible via their designated port?
    * Verifies that vnetd is running on the correct port.
    * Verifies that bpcd is running on the correct port.
    * Verifies that the first SERVER line in the bp.conf file is correct.
    * Verifies that the correct media servers are in the bp.conf file.
    * Verifies that the correct CLIENT_NAME is in the bp.conf file. Note that if the backups.output file is > 0 bytes, this check is bypassed.
    * Reports if the last backup was more than 7 days prior.
  * check_nrpe()
    * Reports if the nrpe agent is not running.
  * check_oomkiller()
    * Reports if there are any oom-killer messages in the log file.
  * check_openview()
    * Reports if the chkov agent validation script is not active in root's cron.
    * Reports if the chkov agent script will not restart the agent in the event of an error.
    * Reports the status of the openview agent.
    * Is the correct route in place for the openview server?
    * Is the openview server pingable?
    * Is the openview server accessible via their designated port?
    * Can the bbcutil ping the openview server?
    * Are certificates installed?
    * Is the agent buffering?
    * Validates the openview configuration.
    * Are policies installed?
    * If permitted, sends a validation message to the openview servers
      * A chkopenview.completed file prevents the message. Removing this will have the test message sent the next time chkopenview is run
      * A chkopenview.block file will prevent the message even if the chkopenview.completed file is deleted.
  * check_opnet()
    * Is OpNet Installed?
    * Is OpNet Running?
    * Is OpNet configured to start on boot?
    * Is the OpNet server pingable?
    * Is the OpNet server accessible via their designated port?
  * check_packages()
    * Comparison check of chkpackages.review and chkpackages.valid
  * check_passwd()
    * Comparison check of chkpwck.review and chkpwck.valid
  * check_privileted_access()
    * Is any privileged user authorized?
    * Has privileged access expired for a user?
  * check_redhat_subscription()
    * Is the Satellite server pingable?
    * Is the Satellite server accessible via their designated ports?
    * Is Subscription Manager installed?
    * Status of the subscription.
    * Is the Katello Certificate installed?
    * Is the Katello agent installed?
  * check_removeips()
    * Is RemoveIPS set to yes?
  * check_resolver()
    * Check the nsswitch.conf file to see if DNS is enabled.
    * Is the nameserver pingable?
    * Are management servers resolvable through each nameserver?
    * Verify that the system IPs are correctly in DNS.
    * Verify that the system hostnames are correctly in DNS.
    * Report if there are more than 3 nameserver entries.
  * check_routetable()
    * Report if any route table mismatches.
    * HP-UX check that the number of static routes matches the actual static routes
    * HP-UX check that there aren't overlaps in the static routes file
  * check_rrdtool()
    * Reports if rrdtool isn't running
  * check_scanners()
    * Report if an InfoSec scanner IP isn't in the routing table
  * check_security()
    * Report if remote root access is permitted.
  * check_selinux()
    * Report the status of SELinux
  * check_services()
    * Comparison generation
  * check_sudoers()
    * Report if sudoers doesn't have the correct hostname
    * Report if sudoers group doesn't exist.
    * Report if sudoers file doesn't exist.
  * check_suid()
    * Comparison check between chksuid.review and chksuid.valid
  * check_swap()
    * Linux Only. Reports if swap space is not = to RAM up to 8G and not 8G if RAM > 8G.
  * check_techops()
    * Reports if /opt/techops exists.
    * Reports if /opt/techops70 exists.
  * check_time()
    * Verifies management route is in place for the time server
    * Is the time server pingable?
    * Is the time server accessible on their designated port?
    * Is the time server IP in the config file
    * Report if unable to reach a time server
    * Report if errors have occurred trying to reach a time server
    * Report if the drift directory doesn't exist.
    * Report if the drift file doesn't exist.
  * check_vmware_agent()
    * Is the VMWare agent installed?
    * Is the VMWare agent running?
    * Is the ctrl-alt-del setting enabled?
  * check_vpn_route()
    * Verify the vpn route is going through the management interface
  * check_vxprint_vxdisk()
    * Checks for failed disks
    * Checks for suspicious disks
    * Checks for spares with data

