### Overview

This set of playbooks is used to prepare a KVM host, either Ubuntu or Red Hat, with libvirt and the libvirt provider for ansible and terraform so the host is ready for the terraform scripts which build the guests.

### Binary Files

Of course none of the binary files are located in git. You'll need to chase them down and make the available somehow.

I have my binary files located on my bldr0cuomdev1:/opt/static/playbooks/libvirt/ directory structure.

In the static directories, create the following subdirectories.

* createlvm/files
* provider/files
* terraform/files

In the createlvm/files directory, the following images need to be available:

* bionic-server-cloudimg-amd64.img - Canonical cloud-init image
* CentOS-7-x86_64-GenericCloud-2009.qcow2 - CentOS cloud image
* CentOS-8-GenericCloud-8.3.2011-20201204.2.x86_64.qcow2 - CentOS cloud Image
* debian-10-openstack-amd64.qcow2 - Debian cloud image

(Images can be found here)[https://docs.openstack.org/image-guide/obtain-images.html]

Then copy the above images as listed below and adjust the sizes as noted. (These files are also needed.)

* centos7_300g.qcow2
* centos8_20g.qcow2
* centos8_50g.qcow2
* centos8_75g.qcow2
* centos8_300g.qcow2
* debian10_20g.qcow2
* ubuntu18_20g.img - While not currently used, I am copying this file out.

In the provider/files directory, you need the following file:

* terraform-provider-libvirt

(Binary can be found here)[https://github.com/dmacvicar/terraform-provider-libvirt]

In the terraform/files directory, you need the following file:

* terraform

(Binary can be found here)[https://www.terraform.io/downloads.html]


