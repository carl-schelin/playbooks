

How to install the dns servers:


	ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=bldr0" install_dns.yaml --syntax-check -vvv
	ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=cabo0" install_dns.yaml --syntax-check -vvv
	ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=tato0" install_dns.yaml --syntax-check -vvv
	ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=lnmt1" install_dns.yaml --syntax-check -vvv
	ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=ndld1" install_dns.yaml --syntax-check -vvv


	ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=bldr0" install_dns.yaml
	ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=cabo0" install_dns.yaml
	ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=tato0" install_dns.yaml
	ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=lnmt1" install_dns.yaml
	ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=ndld1" install_dns.yaml


