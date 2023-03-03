### Overview

This playbook and roles are used to provision the NFS server

The install_nfs.yaml playbook builds the NFS server for each site

See the documentation for background and details on the process.


#### Playbook Execution

Syntax Checks

    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=bldr0' install_nfs.yaml --syntax-check -vvv
    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=cabo0' install_nfs.yaml --syntax-check -vvv
    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=tato0' install_nfs.yaml --syntax-check -vvv
    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=lnmt1' install_nfs.yaml --syntax-check -vvv

Execution

    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=bldr0' install_nfs.yaml
    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=cabo0' install_nfs.yaml
    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=tato0' install_nfs.yaml
    ansible-playbook -i /usr/local/admin/etc/hosts -e 'pattern=lnmt1' install_nfs.yaml

### DNS

Variables required:

    - nfs_dir.root_dir
    - nfs_dir.mount_location
    - nfs_dir.share_mount_location
    - nfs.subnet_range
    - storage_nfs1

Templates required:

  - exports.j2

