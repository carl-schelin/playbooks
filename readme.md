### Overview ###

This directory structure consists of my playbooks. A lot of them are fairly small playbooks where I'm working 
on some specific task. Some of them are larger ones such as the Kubernetes ones.


### Hosts File ###

The Inventory (see the other repository) is used to create the /usr/local/admin/etc/hosts file (the ansible.php script). 
You can add a tag to any server and the tag is then used to identify the list of servers you want to update with the playbook.

`ansible-playbook -i /usr/local/admin/etc/hosts -e pattern=[pattern] [playbook].yaml -s`

I am using patterns and tags for some of the playbooks. Check each yaml file for details.

For example, for the Kubernetes servers, if I wanted to update the masters, I'd pass in `-e 'pattern=boulder:&master' and 
in the playbook I'd have `- hosts: "{{ pattern }}"`. The playbook then parses the hosts file looking for hosts that have 
the 'boulder' tag and the 'master' tag. Don't forget you can use the not (!) to exclude servers from the final host listing.

Note you can run the `searchansible` script (part of the unixsuite repository) to list all the available tag headers and 
`searchansible [tag]` which will return all the servers associated with that tag.


### Playbook Notes ###

While there are a list here, it may not be totally current as things move around, are added, and may be deleted.

kubernetes - see the Kubernetes directory for notes

satellite - Upgrades satellite repos for 6.5

snmpd - Installs a common snmpd.conf file to /etc/snmp

yumupgrade - Basically runs a 'yum upgrade -y'


### checked in playbooks ###

* chrony - updated to use the correct local IP
* ELK
**   data
**   elasticsearch
**   kibana
**   logstash
**   master
* haproxy
* kubernetes
**   00-osupgrade
**   01-bridge
**   02-swap
**   03-packages
**   04-clustername
**   05-kubelet
**   06-certificates
**   07-logging
**   08-permissions
**   09-destroy
**   13-kubeadm
**   15-versionlock
**   configurations
**   dnstools
**   postinstall
**   readme.md
**   scripts
* logcerts
* mariadb
* nousers
* resolver
* satellite
* snmp
* sshd
* sudoers
* touchmotd
* yumupgrade

### Update notes ###

A key bit if information here is that I don't store my site specific configurations with this repository. I have a separate 
playbooks_configs repository that's local to my site. I currently use Jenkins to merge the two repos together and then sync 
them with the final working location.

