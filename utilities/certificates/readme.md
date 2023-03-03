### Overview

This playbook updates all VMs with the package signing keys so they can install packages.


### Process

The playbook first checks to see if it's a CentOS 7 or 8 box and installs the neccessary main key and EPEL key.

Next we'll install keys for the specific application for the system.

The Admin suite located on the tool servers creates a fingerprint file that is on every server in the /opt/unixsuite/etc directory.

The playbook checks for a specific key based on the application.

For example; ",elk,' for Elastic Search servers (data, kibana, logstash, and master).

For Kubernetes; ",kubernetes," for control and worker servers.

Other servers will be added as new keys are required.


### Commands

        ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=bldr0:&elk' certificates.yaml --syntax-check -vvv
        ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=cabo0:&elk' certificates.yaml --syntax-check -vvv
        ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=tato0:&elk' certificates.yaml --syntax-check -vvv
        ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=lnmt1:&elk' certificates.yaml --syntax-check -vvv


        ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=bldr0:&elk' certificates.yaml
        ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=cabo0:&elk' certificates.yaml
        ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=tato0:&elk' certificates.yaml
        ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=lnmt1:&elk' certificates.yaml


