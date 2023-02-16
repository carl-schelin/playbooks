### Overview ###

This playbook and roles are used to install jenkins. This is only in Production so only one line is needed

For now this just ensures the ports are open so we can access jenkins


#### Playbook Execution

Syntax Checks

    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=lnmt1' install_jenkins.yaml --syntax-check -vvv

Execution

    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=lnmt1' install_jenkins.yaml


