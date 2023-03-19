### Overview ###

This directory structure consists of my playbooks. I'm basically creating or updating playbooks to build my homelab 
environment.


### Hosts File ###

The Inventory (see the other repository) is used to create the /usr/local/admin/etc/hosts file (the ansible.php script). 
You can add a tag to any server and the tag is then used to identify the list of servers you want to update with the playbook.

`ansible-playbook -i /usr/local/admin/etc/hosts -e pattern=[pattern] [playbook].yaml -s`

I am using patterns and tags for some of the playbooks. Check each yaml and readme.md file for details.

For example, for the Kubernetes servers, if I wanted to update the control plane, I'd pass in `-e 'pattern=bldr0:&control' and 
in the playbook I'd have `- hosts: "{{ pattern }}"`. The playbook then parses the hosts file looking for hosts that have 
the 'bldr0' tag and the 'control' tag. Don't forget you can use the not (!) to exclude servers from the final host listing.

Note you can run the `searchansible` script (part of the tool server repository) to list all the available tag headers and 
`searchansible [tag]` which will return all the servers associated with that tag.


### Playbook Notes ###

There are essentially four directories in this repository.

* newserver - These playbooks build the VMs or install standardized configurations such as firewall settings.
* servers - These playbooks build specific servers such as NFS server, HAProxy load balancers for Kubernetes, DNS, and so on.
* utilities - These playbooks do some more general configurations that may not need to be run in the newserver playbooks or things that would be run more often to ensure configurations are up to date such as the Unixsuite scripts.
* vars - This directory contains the site specific data files that list configurations, IP addresses, and other bits used by the other playbooks.


### Update notes ###

A key bit if information here is that I don't store my site specific configurations with this repository. I have a separate 
playbooks_configs repository that's local to my site. I currently use Jenkins to merge the two repos together and then sync 
them with the final working location. I am trying to create dummy files so you know what files to create and manage. This is 
specific to my environment though so your mileage may vary.


