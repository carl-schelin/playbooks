### Overview

This role is used to prepare the nodes that make up a kubernetes cluster.


### Preparation

The kubernetes.yaml file is used to prepare the new servers. You can certainly run it complete as it will work as expected. Or you can pass along tags to only run specific roles in case there was an error or if you're not sure.

There are four sites that will have kubernetes clusters. bldr0 (dev), cabo0 (qa), tato (stage), and lnmt (production).


### Roles

bridge: The Bridge and Overlay kernel modules are activated and the persistent files are copied into the /etc/modprobe.d directory. In addition, once the bridge module is activated, three bridge kernel tuning settings are activated plus ip forwarding.

swap: Swap is removed fully from /etc/fstab and from the /etc/default/grub file then the file is rebuilt.

firewall: Since we're using the Calico networking package, it takes care of access so the firewall is not needed. This playbook simply disables the firewall on all nodes.

packages: The packages role installs the yum_versionlock module so we can prevent upgrades when patching servers. The kubernetes.repo, crio.repo, and crio stable.repo is installed. Any existing versionlock entries are removed and new ones for the selected version is applied. Once all that is prepared, kubeadm, kubectl, kubelet, crio, the kubernetes-cni binaries, plus all the docker files are installed. Finally kubelet is enabled and crio is enabled and activated. For kubeadm, kubelet should only be enabled as it doesn't have the configuration file yet. That's created as part of the kubeadm process.

Once the packages playbook has completed, it's time to build the cluster.


### kubeadm

Speaking of kubeadm, once done, you'll log into each of the nodes starting with the control plane and run the kubeadm command as follows.

kubeadm init --control-plane-endpoint "LOAD_BALANCER_DNS:LOAD_BALANCER_PORT" --upload-certs

Where LOAD_BALANCER_DNS is the vip used to balance traffic to the cluster (use the haproxy playbooks). And LOAD_BALANCER_PORT is 6443.

Assuming all goes well, you'll receive two sets of commands. One will be used to provision the remaining two control nodes. The second one will attach workers to the cluster.

For the control plane, you'll need to build each one sequentially as running two at once may cause the second one to time out and fail and you'll need to run it again.

For the workers, you can run them all at the same time.


### Cluster

Once done, on any of the control plane nodes, you'll need to create a ~/.kube directory and then you  can copy the /etc/kubernetes/admin.conf file into the .kube directory renaming it to config. At that point, you can run the kubectl get nodes to get a status of the cluster.


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

