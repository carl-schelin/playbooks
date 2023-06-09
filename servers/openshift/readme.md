
Syntax Checks

    ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e 'pattern=bldr0' install_openshift.yaml --syntax-check -vvv
    ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e 'pattern=cabo0' install_openshift.yaml --syntax-check -vvv
    ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e 'pattern=tato0' install_openshift.yaml --syntax-check -vvv
    ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e 'pattern=lnmt1' install_openshift.yaml --syntax-check -vvv
    ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e 'pattern=ndld1' install_openshift.yaml --syntax-check -vvv

Execution

    ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e 'pattern=bldr0' install_openshift.yaml
    ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e 'pattern=cabo0' install_openshift.yaml
    ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e 'pattern=tato0' install_openshift.yaml
    ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e 'pattern=lnmt1' install_openshift.yaml
    ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e 'pattern=ndld1' install_openshift.yaml

