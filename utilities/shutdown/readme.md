### Overview

Simply playbook to shutdown servers.


        ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=bldr0' shutdown.yaml --syntax-check -vvv
        ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=cabo0' shutdown.yaml --syntax-check -vvv
        ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=tato0' shutdown.yaml --syntax-check -vvv
        ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=lnmt1' shutdown.yaml --syntax-check -vvv
        ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=ndld1' shutdown.yaml --syntax-check -vvv

        ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=bldr0' shutdown.yaml
        ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=cabo0' shutdown.yaml
        ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=tato0' shutdown.yaml
        ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=lnmt1' shutdown.yaml
        ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=ndld1' shutdown.yaml

