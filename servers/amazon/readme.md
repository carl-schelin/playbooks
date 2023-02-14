### Overview

This playbook installs the standard amazon server used to access the amazon aws environment generally with terraform.


# Process

    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=bldr0' install_amazon.yaml --syntax-check -vvv


### Process

    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=bldr0' install_amazon.yaml

