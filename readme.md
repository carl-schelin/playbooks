### Overview ###

This directory structure consists of my playbooks. They're generally small and intended to quickly make simple 
configuration changes across multiple systems.


### Hosts File ###

The Inventory is used to create the /usr/local/admin/etc/hosts file. You can add a tag to any server and the tag 
is then used to identify the list of servers you want to update with the playbook.

`ansible-playbook -i /usr/local/admin/etc/hosts -e [variable]=[tag] [playbook].yaml -s`

As an example, for the Kubernetes servers, if I wanted to update the masters, I'd pass in `-e site=bldr0-0` and in the 
playbook I'd have `- hosts: "{{ site }}"-master`. The playbook then parses the hosts file looking for the `bldr0-0-master` 
header and returns the list of servers with that tag.

Note you can run the `searchansible` script to list all the available headers and `searchansible [tag]` which will return 
all the servers associated with that tag.


### Playbook Notes ###

kubernetes - see the Kubernetes directory for notes

satellite - Upgrades satellite repos for 6.5

snmpd - Installs a common snmpd.conf file to /etc/snmp

yumupgrade - Basically runs a 'yum upgrade -y'


### checked in playbooks ###

chrony - updated to use the correct local IP
ELK
 data
 elasticsearch
 kibana
 logstash
 master
haproxy
kubernetes
 00-osupgrade
 01-bridge
 02-swap
 03-packages
 04-clustername
 05-kubelet
 06-certificates
 07-logging
 08-permissions
 09-destroy
 13-kubeadm
 15-versionlock
 configurations
 dnstools
 postinstall
 readme.md
 scripts
logcerts
mariadb
nousers
resolver
satellite
snmp
sshd
sudoers
touchmotd
yumupgrade

### Update notes ###

There are a few places where you might want to make changes for your environment.

Under the kubernetes directory, you'll want to update the sites and what site you're trying to verify. These are my sites and what I was verifying.

For the kubernetes/06-certificates/certificates/tasks/main.yaml file, my CA is called 'companyCA.pem' Change this if yours is different. I also point to my internal repo server to check for and retrieve its CA so I can pull images. And due to a past installation, I have four 'corp' ca files. Change them as appropriate or simply remove the extra lines. I need to shift that to a variable.

Basically the same thing under logcerts/logcerts/tasks/main.yaml. I'm using companyCA.pem. Feel free  to change it if necessary.

Under the touchmotd/checkmotd script, it points to my internal email address.

