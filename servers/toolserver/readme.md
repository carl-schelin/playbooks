This server is the main entry point to the environment. In general it'll have an apache server for the inventory and status management applications, plus php.

Basically this playbook is run from a central site or server (or laptop) and used to create accounts and prepare for the installation of the playbooks that build the servers for the environment.


#### Playbook Execution

Note that the vault is used for snmp credentials

Syntax Checks

    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=bldr0' install_tool.yaml --syntax-check -vvv
    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=cabo0' install_tool.yaml --syntax-check -vvv
    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=tato0' install_tool.yaml --syntax-check -vvv
    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=lnmt1' install_tool.yaml --syntax-check -vvv
    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=ndld1' install_tool.yaml --syntax-check -vvv

Execution for most tool servers:

    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=bldr0' install_tool.yaml --tags tools
    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=cabo0' install_tool.yaml --tags tools
    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=tato0' install_tool.yaml --tags tools
    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=lnmt1' install_tool.yaml --tags tools
    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=ndld1' install_tool.yaml --tags tools

    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=bldr0' install_tool.yaml --tags kubernetes
    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=cabo0' install_tool.yaml --tags kubernetes
    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=tato0' install_tool.yaml --tags kubernetes
    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=lnmt1' install_tool.yaml --tags kubernetes
    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=ndld1' install_tool.yaml --tags kubernetes

    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=bldr0' install_tool.yaml --tags httpd
    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=cabo0' install_tool.yaml --tags httpd
    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=tato0' install_tool.yaml --tags httpd
    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=lnmt1' install_tool.yaml --tags httpd
    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=ndld1' install_tool.yaml --tags httpd


When installing an openshift cluster (okd4 or ocp4) only in boulder, run the following tags as well or simply run without tags to fully install:

    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=bldr0' install_tool.yaml --tags dhcp
    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=bldr0' install_tool.yaml --tags tftp

As pxe installs some files into the tftproot directory structure, it should be run last.
    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=bldr0' install_tool.yaml --tags pxe

Note passing -e patch=true to the above playbooks and the guests will be patched and rebooted upon completion. It will take some time of course so be ready.

