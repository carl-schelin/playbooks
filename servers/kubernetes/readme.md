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

Run the following commands to run the playbook


        ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=bldr0" kubernetes.yaml --tags=bridge
        ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=cabo0" kubernetes.yaml --tags=bridge
        ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=tato0" kubernetes.yaml --tags=bridge
        ansible-playbook -i /usr/local/admin/etc/hosts -e "pattern=lnmt1" kubernetes.yaml --tags=bridge




