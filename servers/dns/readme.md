### Installation

This set of playbooks installs the various tools needed to provision a dns server


### monit

monit is a tool that monitors services on a server. If the service shuts down for some reason, monit runs a script that is customizable, essentially to restart the service but as it's a script, it can be used for any purpose such as notifying the team of the outage.

#### Configuration

This is the monit/defaults/main.yaml configuration that is password protected in vault. Unfortunately it's hard coded in the software so you can't really change it. I recommend changing the settings so that access is read-only.

 ---
 monit:
   name: "[account]"
   password: "[password]"


### Ansible commands

The following command are used to install a dns server or configure guests. This installs bind and monit which monitors the service and restarts it should it fail for some reason.


	ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e "pattern=bldr0" install_dns.yaml --syntax-check -vvv
	ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e "pattern=cabo0" install_dns.yaml --syntax-check -vvv
	ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e "pattern=tato0" install_dns.yaml --syntax-check -vvv
	ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e "pattern=lnmt1" install_dns.yaml --syntax-check -vvv
	ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e "pattern=ndld1" install_dns.yaml --syntax-check -vvv


	ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e "pattern=bldr0" install_dns.yaml
	ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e "pattern=cabo0" install_dns.yaml
	ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e "pattern=tato0" install_dns.yaml
	ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e "pattern=lnmt1" install_dns.yaml
	ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e "pattern=ndld1" install_dns.yaml


	ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=bldr0" install_guests.yaml --syntax-check -vvv
	ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=cabo0" install_guests.yaml --syntax-check -vvv
	ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=tato0" install_guests.yaml --syntax-check -vvv
	ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=lnmt1" install_guests.yaml --syntax-check -vvv
	ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=ndld1" install_guests.yaml --syntax-check -vvv


	ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=bldr0" install_guests.yaml
	ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=cabo0" install_guests.yaml
	ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=tato0" install_guests.yaml
	ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=lnmt1" install_guests.yaml
	ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=ndld1" install_guests.yaml


You can pass a --tag [dns|monit] to only install/refresh one aspect of a dns server

