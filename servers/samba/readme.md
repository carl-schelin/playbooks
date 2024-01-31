### Installation

This set of playbooks are used to provision the samba server which is used by folks in the house to back up their data.


### Samba

Samba is the tool that lets us share drives with users. There are three servers currently that run samba. Backups, Movies, and Television.


#### Configuration

It's likely that we don't need to password protect this information as there are no credentials here and it may be moved at a later date. It does have user information.

```
---
samba:
  - workgroup: "BATTLENET"
    description: "Samba Server Version %v"
    allow: "192.168.1."
    logfile: "/var/log/samba/log.%m"
    maxlog: "50"
    security: "user"
    passdb: "tdbsam"
    printers: "no"


movies:
  - name: "movies"
    description: "Media - Movies, Books, Games"
    browseable: yes
    path: /media
    writable: yes
    guest: no


television:
  - name: "television"
    description: "TV Shows"
    browseable: "yes"
    path: "/media"
    writable: "yes"
    guest: "yes"


backups:
  - name: "cschelin"
    description: "Carl's Backup Directories"
    security: "cschelin"
    browseable: "yes"
    path: "/samba/cschelin"
    writable: "yes"
  - name: "jainsley"
    description: "Jeanne's Backup Directories"
    security: "jainsley"
    browseable: "yes"
    path: "/samba/jainsley"
    writable: "yes"
  - name: "lscott"
    description: "Lisa Scott's Backup Directories"
    security: "lscott"
    browseable: "yes"
    path: "/samba/lscott"
    writable: "yes"
```


### Monit

The monit tool is used to monitor services on a server and runs a script should the service go away. As it's a script, it can do anything including notifying the management and/or monitoring team.

#### Configuration

The problem with monit is the account name and password is hard coded into the software. I recommend ensuring the configuration is read-only.

 ---
 monit:
   name: "[account]"
   password: "[password] "


### Commands


This block is the command used to verify the playbook is working as expected.

	ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e "pattern=bldr0" install_samba.yaml --syntax-check -vvv
	ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e "pattern=cabo0" install_samba.yaml --syntax-check -vvv
	ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e "pattern=tato0" install_samba.yaml --syntax-check -vvv
	ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e "pattern=lnmt1" install_samba.yaml --syntax-check -vvv
	ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e "pattern=ndld1" install_samba.yaml --syntax-check -vvv


This is the list of commands you'd use to install samba.

	ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e "pattern=bldr0" install_samba.yaml
	ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e "pattern=cabo0" install_samba.yaml
	ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e "pattern=tato0" install_samba.yaml
	ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e "pattern=lnmt1" install_samba.yaml
	ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e "pattern=ndld1" install_samba.yaml

There are two tags here that lets you install Samba. Pass in --tag [samba|monit] to restrict to an install or refresh of a configuration

