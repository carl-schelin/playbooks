
There are multiple configuration files here for use in the various Kubernetes clusters.

Elastic Stack configuration files are in the filebeat directory for the main download and in the bldr, tato, lnmt, and miam directories for the modified final configurations.

New Relic configuration files are in the newrelic directory for the main download and in the bldr0-0, gldn0-0, cabo0-0, hell0-0, tato0-1, alde0-0, lnmt1-2, and miam1-1 directories for the modified final configurations used when upgrading.

ResourceQuota and LimitRange configurations are in the CIL and Production directories, tato0-1, alde0-0, lnmt1-2, and miam1-1.

The configuration files here are used to set the ResourceQuota and LimitRange for namespaces. Additional configuration files will be added but for now these are what's here.

* BigIP
* ACMC
* CRP
* GIS Director
* WDLS

There is a kube-system file in the lnmt1-2 directory that was used to permit the deployment of the dnstools container in order to do testing.

Finally the metric server files are also located here in the kube-state-metrics and metrics-server yaml files.

