



        ansible-playbook -i ../../inventory/development -e 'pattern=bldr0' ping_check.yaml --syntax-check -vvv
        ansible-playbook -i ../../inventory/development -e 'pattern=cabo0' ping_check.yaml --syntax-check -vvv
        ansible-playbook -i ../../inventory/development -e 'pattern=tato0' ping_check.yaml --syntax-check -vvv
        ansible-playbook -i ../../inventory/development -e 'pattern=lnmt1' ping_check.yaml --syntax-check -vvv
        ansible-playbook -i ../../inventory/development -e 'pattern=ndld1' ping_check.yaml --syntax-check -vvv

        ansible-playbook -i ../../inventory/development -e 'pattern=bldr0' ping_check.yaml
        ansible-playbook -i ../../inventory/development -e 'pattern=cabo0' ping_check.yaml
        ansible-playbook -i ../../inventory/development -e 'pattern=tato0' ping_check.yaml
        ansible-playbook -i ../../inventory/development -e 'pattern=lnmt1' ping_check.yaml
        ansible-playbook -i ../../inventory/development -e 'pattern=ndld1' ping_check.yaml



