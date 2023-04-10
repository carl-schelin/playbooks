### Overview

These roles are used to prepare the nodes that make up a kubernetes cluster.


### Preparation

The kubernetes.yaml file is used to prepare the new servers. You can certainly run it complete as it should work as expected. Or you can pass along tags to only run specific roles in case there was an error or if you're not sure.

I will note that the packages role has needed to be stopped and run three times. Otherwise it appears to hang up when creating a versionlock and when installing kubelet.

There are four sites that will have kubernetes clusters. bldr0 (dev), cabo0 (qa), tato (stage), and lnmt (production).


### Roles

bridge: The Bridge and Overlay kernel modules are activated and the persistent files are copied into the /etc/modprobe.d directory. In addition there are four kernel settings related to the bridge module. The sysctl file is supplied but in order to set it during the playbook run, the bridge module must be activated as the bridge module creates the appropriate directory off of /proc.

swap: Swap is removed fully from /etc/fstab and from the /etc/default/grub file then the file is rebuilt and applied to /boot/grub.

firewall: Since we're using the Calico networking package, it takes care of access so the firewall is not needed. This playbook simply disables the firewall on all nodes.

packages: The packages role installs the yum_versionlock module so we can prevent upgrades when patching servers. The kubernetes.repo, crio.repo, and crio stable.repo is installed. Any existing versionlock entries are removed and new ones for the selected version is applied. Once all that is prepared, kubeadm, kubectl, kubelet, crio, the kubernetes-cni binaries, plus all the docker files are installed. Finally kubelet is enabled and crio is enabled and activated. For kubeadm, kubelet should only be enabled as it doesn't have the configuration file yet and will error if started. That's created as part of the kubeadm process.

Once the packages playbook has completed, it's time to build the cluster.


### kubeadm

Speaking of kubeadm, once done, you'll log into the first control plane node and in the service account home directory will be the kubeadm-config.yaml file. You'll run the below command which will initialize the cluster.

    kubeadm init --config kubeadm-config.yaml --upload-certs

Assuming all goes well, you'll receive two sets of commands. One will be used to provision the remaining two control nodes. The second one will attach workers to the cluster.

For the control plane, you'll need to build each one sequentially as running two at once may cause the second one to time out and fail and you'll need to run it again.

For the workers, you can run them all at the same time.


### Cluster

Once done, on any of the control plane nodes, you'll need to create a ~/.kube directory and then you can copy the /etc/kubernetes/admin.conf file into the .kube directory renaming it to config. At that point, you can run the kubectl get nodes to get a status of the cluster.


### Plays

If you're going to run it straight, then one of the following plays can be run.

        ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=bldr0:&kubernetes" kubernetes.yaml
        ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=cabo0:&kubernetes" kubernetes.yaml
        ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=tato0:&kubernetes" kubernetes.yaml
        ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=lnmt1:&kubernetes" kubernetes.yaml

If you want to run tasks one at a time, the following tags are available.

Configure the bridge and kernel tuning settings:

        ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=bldr0:&kubernetes" kubernetes.yaml --tags=bridge
        ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=cabo0:&kubernetes" kubernetes.yaml --tags=bridge
        ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=tato0:&kubernetes" kubernetes.yaml --tags=bridge
        ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=lnmt1:&kubernetes" kubernetes.yaml --tags=bridge

Disable swap on all nodes.

        ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=bldr0:&kubernetes" kubernetes.yaml --tags=swap
        ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=cabo0:&kubernetes" kubernetes.yaml --tags=swap
        ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=tato0:&kubernetes" kubernetes.yaml --tags=swap
        ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=lnmt1:&kubernetes" kubernetes.yaml --tags=swap

Disable the firewall on all nodes

        ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=bldr0:&kubernetes" kubernetes.yaml --tags=firewall
        ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=cabo0:&kubernetes" kubernetes.yaml --tags=firewall
        ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=tato0:&kubernetes" kubernetes.yaml --tags=firewall
        ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=lnmt1:&kubernetes" kubernetes.yaml --tags=firewall

Install the kubeadm, kubectl, and kubelet binaries, also crio and activate them.

        ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=bldr0:&kubernetes" kubernetes.yaml --tags=packages
        ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=cabo0:&kubernetes" kubernetes.yaml --tags=packages
        ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=tato0:&kubernetes" kubernetes.yaml --tags=packages
        ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=lnmt1:&kubernetes" kubernetes.yaml --tags=packages

