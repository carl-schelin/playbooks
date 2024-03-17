### Overview ###

This playbook and roles are used to install nagios. This service is only in Production so only one line is needed

For now this just ensures the http port is open so we can access nagios


#### Playbook Execution

Syntax Checks

    ansible-playbook -i /usr/local/admin/etc/hosts install_nagios.yaml --syntax-check -vvv

Execution

    ansible-playbook -i /usr/local/admin/etc/hosts install_nagios.yaml


