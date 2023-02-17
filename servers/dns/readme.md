

How to install the dns servers:


	ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e "pattern=bldr0" install_dns.yaml --syntax-check -vvv
	ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e "pattern=cabo0" install_dns.yaml --syntax-check -vvv
	ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e "pattern=tato0" install_dns.yaml --syntax-check -vvv
	ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e "pattern=lnmt1" install_dns.yaml --syntax-check -vvv
	ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e "pattern=ndld1" install_dns.yaml --syntax-check -vvv


	ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e "pattern=bldr0" install_dns.yaml
	ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e "pattern=cabo0" install_dns.yaml
	ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e "pattern=tato0" install_dns.yaml
	ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e "pattern=lnmt1" install_dns.yaml
	ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e "pattern=ndld1" install_dns.yaml


