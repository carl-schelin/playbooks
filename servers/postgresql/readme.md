### Overview

This playbook and roles are used to provision the Postgresql server

The install_postgresql.yaml playbook builds the Postgresql server for each site

See the documentation for background and details on the process.


#### Playbook Execution

Syntax Checks

    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=bldr0' install_postgresql.yaml --syntax-check -vvv
    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=cabo0' install_postgresql.yaml --syntax-check -vvv
    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=tato0' install_postgresql.yaml --syntax-check -vvv
    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=lnmt1' install_postgresql.yaml --syntax-check -vvv

Execution

    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=bldr0' install_postgresql.yaml
    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=cabo0' install_postgresql.yaml
    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=tato0' install_postgresql.yaml
    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=lnmt1' install_postgresql.yaml

