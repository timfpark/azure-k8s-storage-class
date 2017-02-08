# Azure Kubernetes Storage Class

azure-disk.yaml contains a sample storage class for use with a Kubernetes cluster running
on Azure.

To use:

1. Create a storage account on Azure that this K8s storage class will create persistent volumes in.
2. Edit azure-disk.yaml to provide a name (eg. 'fast'), data center location (eg. 'eastus'), and storage account name (eg. 'acspremium').
3. Register this Storage Class with your Kubernetes cluster using `kubectl create -f azure-disk.yaml`.

You can then use this storage class with deployments.  For example, to deploy Redis on the cluster with premium storage disks with helm:

`# helm install --name redis --namespace redis --set persistence.storageClass=fast --set persistence.size=4Gi stable/redis`
