### Overview

This is the playbook subdirectory for Kubernetes work.


### Sections


#### Bridge

Purpose:

The core-dns container in Kubernetes has a bug in that if a container shares a worker with core-dns, name resolution fails.
Since there are generally a pair of core-dns containers, the resolution lookup can succeed which throws off troubleshooting.
The solution is to enable the three bridge kernel rules and enable the bridge module.








The playbooks are created to be run in order vs trying to figure out which ones to run.

Playbooks 01-07 were used to initially set up the Kubernetes servers for the 1.14.7 installations.

Playbook 08 is a security update, making sure files and directories are correct.

Playbook 09 is used to tear down a kubernetes cluster that was created by kubeadm. Deletes all directories, etc.

Playbooks 10-11 is used to upgrade the cluster binaries to 1.15.7. After the upgrade, log in to the first master and as root upgrade the server to 1.15.7. Then run playbook 11 which restarts both kubelet and docker

  * Removes the 1.14.7 versionlock
  * Adds the 1.15.7 versionlock
  * Upgrades kubelet, kubectl, and kubeadm
