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



