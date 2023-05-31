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

Execution

    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=bldr0' install_tool.yaml
    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=cabo0' install_tool.yaml
    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=tato0' install_tool.yaml
    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=lnmt1' install_tool.yaml
    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=ndld1' install_tool.yaml

    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=bldr0' -e patch=true install_tool.yaml
    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=cabo0' -e patch=true install_tool.yaml
    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=tato0' -e patch=true install_tool.yaml
    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=lnmt1' -e patch=true install_tool.yaml
    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=ndld1' -e patch=true install_tool.yaml


Note passing -e patch=true to the above playbooks and the guests will be patched and rebooted upon completion. It will take some time of course so be ready.


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

    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=bldr0' install_tool.yaml --tags dhcp
    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=cabo0' install_tool.yaml --tags dhcp
    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=tato0' install_tool.yaml --tags dhcp
    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=lnmt1' install_tool.yaml --tags dhcp
    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=ndld1' install_tool.yaml --tags dhcp

Others are pxe, httpd, and tftp

