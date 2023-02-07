# k8s-supportconfig-plugin

Kubernetes plugin log collector for supportconfig part of the [supportutils](https://github.com/openSUSE/supportutils) package.

NOTE: The instructions have been tested on openSUSE and SUSE systems.

## Overview
This script purpose is to include [Rancher's log collector](https://github.com/rancherlabs/support-tools/tree/master/collection/rancher/v2.x/logs-collector) when supportconfig is executed so that as much as kubernetes data can be gathered

I made a contribution upstream recently to Rancher's log collector script which added the support for Kubeadm clusters using the switch `-r kubeadm`, on top of the already existent collections for Rancher environments.

The script auto-detects the environemnt and treis to collect logs for control planes (masters) and workers (agents) components and collect info such api-resource, nodes, metrics, certificates state and many more...

Rancher collector script can be installed on any cluster nodes by running:

`sudo curl -Ls rnch.io/rancher2_logs -o /usr/local/sbin/rancher2_logs_collector.sh`

## Installation Instructions

1) Get `kubernetes` plugin and copy it in `/usr/lib/supportconfig/plugins`

2) Fetch and install rancher's collector script: 

   `sudo curl -Ls rnch.io/rancher2_logs -o /usr/local/sbin/rancher2_logs_collector.sh`

   Alternatevely, copy it in the correct location `/usr/local/sbin/rancher2_logs_collector.sh`

3) Set the correct plugin permission:

   `chmod 755 /usr/lib/supportconfig/plugins/kubernetes`

Once installed the plugin will be available in the list of supportconfig modules (pkubernetes):

`sudo supportconfig -F`

`APPARMOR AUDIT AUTOFS BOOT BTRFS DAEMONS CIMOM CRASH CRON DHCP DISK DNS DOCKER DRBD EMAIL ENV ETC HA HAPROXY HISTORY IB ISCSI LDAP LVM MEM MOD MPIO NET NFS NTP NVME OCFS2 OFILES PODMAN PRINT PROC SAR SLERT SLP SMT SMART SMB SRAID SSH SSSD SYSCONFIG SYSFS TRANSACTIONAL TUNED UDEV UFILES UP WEB X LIVEPATCH aFSLIST aLOGS aMINDISK aMAXYAST aRPMV aSLP aLOCAL_ONLY pkubernetes`

In order to only collect the plugin's (k8s) logs, run:

`sudo supportconfig -i pkubernetes`

All new supportconfigs will include the `kubernetes.txt` file with all of the kubernetes data.

More messages about the collection, debug and errors are shown in `plugin-kubernetes.txt`
