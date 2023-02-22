Description: The modifysudo script is used to add sudo rules to permit NOPASSWD access to all servers via Ansible.

The script:

* If a changefreeze is in effect, exits the script
* Ensures the ansgrp exists
* Ensures root is a member of the group
* Ensures unixsvc has the correct rule to permit execution of Ansible Playbooks
* If the 'towersvc' service account exists, adds the correct rule for Ansible Tower
* Removes the Temporary File when done

* Location: [server]:bin/modifysudo
* Flag File: [server]:etc/changefreeze
* Temporary File: [server]:var/sudoers.unixsvc

