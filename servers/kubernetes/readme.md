### Overview

This is the playbook subdirectory for Kubernetes work.


### Sections

The kubernetes.yaml file can be run with tags= if you need to run a specific play.


#### Clustername



#### Kubelet




#### Certificates




#### Logging



#### Permissions

This is a security update, making sure all files and directories are correct.


#### Kubeadm

At this step, you'll log in to the control nodes and run kubeadm in order to install kubernetes.


#### Versionlock

This play ensures that during upgrades, you don't accidentally upgrade the Kubernetes componants.


### Postinstall

This play should generally be extracted out to perform the above tasks.



### Plays

There are multiple tasks that can be run against the Kubernetes control and worker nodes.

There are three patterns:

  pattern=bldr0:&kubernetes - this one touches all kubernetes nodes for the site
  pattern=bldr0:&control - this one touches just the control plane nodes for the site
  pattern=bldr0:&worker - this one touches just the worker nodes for the site

In addition there are multiple tasks that can be run. I should split these into unique installations but for now, make sure you use the correct pattern when running the playbook.


Add the cluster name to the control nodes
        ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=bldr0:&control" kubernetes.yaml --tags=clustername
        ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=cabo0:&control" kubernetes.yaml --tags=clustername
        ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=tato0:&control" kubernetes.yaml --tags=clustername
        ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=lnmt1:&control" kubernetes.yaml --tags=clustername

Add the cluster name to the control nodes
        ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=bldr0:&control" kubernetes.yaml --tags=clustername
        ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=cabo0:&control" kubernetes.yaml --tags=clustername
        ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=tato0:&control" kubernetes.yaml --tags=clustername
        ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=lnmt1:&control" kubernetes.yaml --tags=clustername



Update the permissions of files
        ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=bldr0:&kubernetes" kubernetes.yaml --tags=permissions
        ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=cabo0:&kubernetes" kubernetes.yaml --tags=permissions
        ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=tato0:&kubernetes" kubernetes.yaml --tags=permissions
        ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=lnmt1:&kubernetes" kubernetes.yaml --tags=permissions







  roles:
    - { role: kubelet,      tags: ["kubelet"]      }
    - { role: certificates, tags: ["certificates"] }
    - { role: logging,      tags: ["logging"]      }
    - { role: permissions,  tags: ["permissions"]  }
    - { role: kubeadm,      tags: ["kubeadm"]      }
    - { role: versionlock,  tags: ["versionlock"]  }
    - { role: postinstall,  tags: ["postinstall"]  }










