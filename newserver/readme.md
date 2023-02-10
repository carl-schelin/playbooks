### Overview ###

This section is for all the tasks when a new server is built plus ensure some common bits are in place

Once the servers are initialized, then we can work on specific server builds.

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


### Overview

This playbook and roles are used to initialize all the two guests on a site.

See the documentation for background and details on the process.


#### Playbook Execution

Note that the vault is used for snmp credentials

Syntax Checks

    ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e 'pattern=bldr0' initialize.yaml --syntax-check -vvv
    ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e 'pattern=cabo0' initialize.yaml --syntax-check -vvv
    ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e 'pattern=tato0' initialize.yaml --syntax-check -vvv
    ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e 'pattern=lnmt1' initialize.yaml --syntax-check -vvv
    ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e 'pattern=ndld1' initialize.yaml --syntax-check -vvv

Execution

    ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e 'pattern=bldr0' initialize.yaml
    ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e 'pattern=cabo0' initialize.yaml
    ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e 'pattern=tato0' initialize.yaml
    ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e 'pattern=lnmt1' initialize.yaml
    ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e 'pattern=ndld1' initialize.yaml

    ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e 'pattern=bldr0' -e patch=true initialize.yaml
    ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e 'pattern=cabo0' -e patch=true initialize.yaml
    ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e 'pattern=tato0' -e patch=true initialize.yaml
    ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e 'pattern=lnmt1' -e patch=true initialize.yaml
    ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e 'pattern=ndld1' -e patch=true initialize.yaml


Note passing -e patch=true to the above playbooks and the guests will be patched and rebooted upon completion. It will take some time of course so be ready.


### Secondary HAProxy

Variables required:

  - read_only
  - snmp.ipa_1
  - snmp.ipa_2
  - snmp_trap
  - dns_primary.ipa

Templates required:

  - snmp.conf.j2

