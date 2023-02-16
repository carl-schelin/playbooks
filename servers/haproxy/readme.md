




        ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e 'pattern=bldr0' install_haproxy.yaml
        ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e 'pattern=cabo0' install_haproxy.yaml
        ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e 'pattern=tato0' install_haproxy.yaml
        ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e 'pattern=lnmt1' install_haproxy.yaml


