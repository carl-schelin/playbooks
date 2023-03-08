

How to install the docker repository server:

There's only the one system so the server name is in the playbook.
This also installs the web server, php, and an index.php script so you can browse to the server and see what images are installed.


	ansible-playbook -i /usr/local/admin/etc/hosts install_repository.yaml --syntax-check -vvv


	ansible-playbook -i /usr/local/admin/etc/hosts install_repository.yaml


