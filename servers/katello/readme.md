### Overview

I'm defining the process based on the Foreman documentation to ensure a Katello server is created as designed.


### Prerequisites

Per the documentation, and our needs, the server should have 4 CPUs, 12 Gigs of RAM, and up to 500 Gigs of Disk Space.

### Presteps

Once the server has been provisioned and set up, you'll need to follow the documentation as listed below. Each of the steps are mirrored by one of the Ansible Playbooks.

First you'll need to install the necessary packages. This is done using the **install_initialize.yaml** playbook.

    ansible-playbook -i /usr/local/admin/etc/hosts --pattern='lnmt1cuomkat1' install_initialize.yaml

This playbook installs and configures the firewall, installs the necessary repository configurations, and finally installs katello.

**Important:** Do not install Foreman. Katello is a plugin but it needs to be the scenario selected when you do the installation or it's broken and you must start over.


### Installing Katello

This is the tricky part. Due to the amount of time it takes, it's been timing out trying to Ansiblize the installation. For now, log in to the target server and simply run the following command:

    foreman-install --scenario katello

This will take several minutes to get things set up. Let it run.


### Configuring Katello

Now we're at the meat of the installation. Here you'll configure the Organization, Site Locations, Lifecycle Environments, add Repository Credentials, create Products, Repositories, Content Views, and finally Activation Keys.

For the Credentials, you'll need to retrieve them from the pertinent sites and place them into the credentials role under the files directory.

* https://www.centos.org/keys/RPM-GPG-KEY-CentOS-7
* https://dl.fedoraproject.org/pub/epel/RPM-GPG-KEY-EPEL-7
* https://www.centos.org/keys/RPM-GPG-KEY-CentOS-Official
* https://dl.fedoraproject.org/pub/epel/RPM-GPG-KEY-EPEL-8
* https://artifacts.elastic.co/GPG-KEY-elasticsearch
* https://packages.cloud.google.com/yum/doc/yum-key.gpg
* https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg

Run the following playbook to complete all the steps. You can also run them individually by adding a --tag and following with the role you want to run.

* --tag configure
* --tag credentials
* --tag products
* --tag repositories
* --tag contentviews

Check the various tasks to ensure they're installing what you want to install. Currently the following repositories are configured and have associated products created. Simply review the tasks and ensure they match what you want to install. Of course you can add things later, no worries there.

* CentOS 7 Base, Updates, Extras, and Plus
* CentOS 8 BaseOS, AppStream, PowerTools, Extras, and Plus
* EPEL 7
* EPEL 8 and EPEL 8 Modular
* Kubernetes
* Elasticsearch

You **must** create a [role]/defaults/main.yaml ansible-vault file that looks like this. You will get the katello_password from the output of the foreman-install command so copy that down:

    # ansible-vault create main.yaml
    ---
    katello_password: "password"
    katello_url: "url of the katello server"
    katello_organization: "organization"

If you're ready and it's all set, run the following playbook.

    ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e pattern='lnmt1cuomkat1' install_katello.yaml


Another issue is the Ansible options don't have a "Promote" task. Part of the point of Content Views is to be able to promote Content Views between environments. This means either a shell command playbook or manually promoting the Content View.

As you can't create an Activation Key without a Content View, you'll need to ensure they're all Published and then at least promote a core or starting Content View to all environments. Once that's done, you can create Activation Keys and then add servers to Katello.


### Activation Keys

Once the initial Content Views have been promoted, you can now create Activation Keys

    ansible-playbook -i /usr/local/admin/etc/hosts --ask-vault-pass -e pattern='lnmt1cuomkat1' install_activation.yaml

At this point, the Katello server is configured and ready to add servers to it.


### Managing Content Views

The ultimate goal here is to regularly create a Content View in order for all environments to be consistent in their patch bundles. This section describes the process for creating additional content views.

