# Why
Using [odo](https://docs.openshift.com/container-platform/4.2/cli_reference/openshift_developer_cli/understanding-odo.html) on OpenShift causes PV/C's to be created upon doing an `oc push` for an app component. on IBM Cloud, the smallest provisionable storage volume is 20GB which is certainly `TOO BIG` for the source code for any application. This solution solves this problem by creating a new NFS provisioner and storageclass in the cluster that is backed by a single block PVC of some large size (>20GB potentially) and then allowing much smaller PV/Cs to be created using the new storageclass. `odo` defaults to a 1GB volume (which is prob way to big, too, but I can't change that). 

I'd be great if `odo` exposed some configuration capabilities that allows us to specify the storageclass to use for it's needs but it does not. So, in order to get this to work correctly, you'll need to make this new storageclass the default for the cluster. That's not ideal but it's the only option if we cannot configure `odo` to better use our preferred storageclass. 

# Deployment

1. Backing PVC
2. RBAC
3. SCC
4. `oc adm policy add-scc-to-user nfs-provisioner -z nfs-provisioner`
5. Deployment
6. StorageClass


Set StorageClass to default for `odo` to pick up and use
