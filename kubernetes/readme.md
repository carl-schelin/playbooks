### Overview ###

This is the playbook subdirectory for Kubernetes work.


### Sections ###

The playbooks are created to be run in order vs trying to figure out which ones to run.

Playbooks 01-07 were used to initially set up the Kubernetes servers for the 1.14.7 installations.

Playbook 08 is a security update, making sure files and directories are correct.

Playbook 09 is used to tear down a kubernetes cluster that was created by kubeadm. Deletes all directories, etc.

Playbook 10-11 is used to upgrade the cluster to 1.15.7. It replaces the versionlock settings and upgrades all the packages.

Playbook 12 is used to activate the new 6.5 satellite repo, update, and then restart docker. This should be part of Playbook 10-11 as it was done after the upgrade.

