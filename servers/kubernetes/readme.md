### Overview

This is the playbook subdirectory for Kubernetes work.


### Sections

    - { role: bridge,       tags: ["bridge"]       }
    - { role: swap,         tags: ["swap"]         }
    - { role: packages,     tags: ["packages"]     }
    - { role: clustername,  tags: ["clustername"]  }
    - { role: kubelet,      tags: ["kubelet"]      }
    - { role: certificates, tags: ["certificates"] }
    - { role: logging,      tags: ["logging"]      }
    - { role: permissions,  tags: ["permissions"]  }
    - { role: kubeadm,      tags: ["kubeadm"]      }
    - { role: versionlock,  tags: ["versionlock"]  }
    - { role: postinstall,  tags: ["postinstall"]  }


The kubernetes.yaml file can be run with tags= if you need to run a specific play.

#### Bridge

Purpose:

The core-dns container in Kubernetes has a bug in that if a container shares a worker with core-dns, name resolution fails.
Since there are generally a pair of core-dns containers, the resolution lookup can succeed which throws off troubleshooting.
The solution is to enable the three bridge kernel rules and enable the bridge module.

#### Swap

Kubernetes requires that swap be disabled on all nodes. This playbook removes swap from the system including as an option in the kernel.

#### Packages



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

Configure the firewall on the control nodes
        ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=bldr0:&kubernetes" kubernetes.yaml --tags=firewall
        ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=cabo0:&kubernetes" kubernetes.yaml --tags=firewall
        ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=tato0:&kubernetes" kubernetes.yaml --tags=firewall
        ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=lnmt1:&kubernetes" kubernetes.yaml --tags=firewall

Install the kubeadm, kubectl, and kubelet binaries
        ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=bldr0:&control" kubernetes.yaml --tags=packages
        ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=cabo0:&control" kubernetes.yaml --tags=packages
        ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=tato0:&control" kubernetes.yaml --tags=packages
        ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=lnmt1:&control" kubernetes.yaml --tags=packages

Add the cluster name to the cluster
        ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=bldr0:&control" kubernetes.yaml --tags=clustername
        ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=cabo0:&control" kubernetes.yaml --tags=clustername
        ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=tato0:&control" kubernetes.yaml --tags=clustername
        ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=lnmt1:&control" kubernetes.yaml --tags=clustername







  roles:
    - { role: kubelet,      tags: ["kubelet"]      }
    - { role: certificates, tags: ["certificates"] }
    - { role: logging,      tags: ["logging"]      }
    - { role: permissions,  tags: ["permissions"]  }
    - { role: kubeadm,      tags: ["kubeadm"]      }
    - { role: versionlock,  tags: ["versionlock"]  }
    - { role: postinstall,  tags: ["postinstall"]  }










