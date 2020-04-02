# Deployment

1. Backing PVC
2. RBAC
3. SCC
4. `oc adm policy add-scc-to-user nfs-provisioner -z nfs-provisioner`
5. Deployment
6. StorageClass


Set StorageClass to default for `odo` to pick up and use
