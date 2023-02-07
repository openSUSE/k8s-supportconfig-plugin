# k8s-supportconfig-plugin

Kubernetes plugin log collector for supportconfig part of the [supportutils](https://github.com/openSUSE/supportutils) suite

## Overview
This script purpose is to include [Rancher's log collector](https://github.com/rancherlabs/support-tools/tree/master/collection/rancher/v2.x/logs-collector) while supportconfig is executed so that as much as kubernetes data can be gathered

I made a contribution upstream recently which added the support for Kubeadm clusters in the rancher's collector using the switch `-r kubeadm` as well as collection from Rancher environments.

The script auto-detects the environemnt and treid to collect logs for control planes (masters) and workers (agents) components and collect info such api-resource, nodes, metrics, certificates state and many more...

Rancher collector script can be installed on any cluster nodes by running:

`sudo curl -Ls rnch.io/rancher2_logs -o /usr/local/sbin/rancher2_logs_collector.sh`

## Installation Instructions

Download the Plugin Script and send kubernetes.gz to the customer

Copy `kubernetes` plugin in `/usr/lib/supportconfig/plugins`

Fetch and install rancher's collector script: 

`sudo curl -Ls rnch.io/rancher2_logs -o /usr/local/sbin/rancher2_logs_collector.sh`

Alternatevely, copy it in the correct location /usr/local/sbin/rancher2_logs_collector.sh

Set the correct plugin permission:

`chmod 755 /usr/lib/supportconfig/plugins/kubernetes`

Once installed the plugin will be available in the list of supportconfig modules (pkubernetes):

`sudo supportconfig -F`

`APPARMOR AUDIT AUTOFS BOOT BTRFS DAEMONS CIMOM CRASH CRON DHCP DISK DNS DOCKER DRBD EMAIL ENV ETC HA HAPROXY HISTORY IB ISCSI LDAP LVM MEM MOD MPIO NET NFS NTP NVME OCFS2 OFILES PODMAN PRINT PROC SAR SLERT SLP SMT SMART SMB SRAID SSH SSSD SYSCONFIG SYSFS TRANSACTIONAL TUNED UDEV UFILES UP WEB X LIVEPATCH aFSLIST aLOGS aMINDISK aMAXYAST aRPMV aSLP aLOCAL_ONLY pkubernetes`

In order to only collect the plugin's (k8s) logs, run:

`sudo supportconfig -i pkubernetes`

All new supportconfigs will include the `kubernetes.txt` file with all of the kubernetes data.

More messages about the collection, debug and errors are shown in `plugin-kubernetes.txt`
