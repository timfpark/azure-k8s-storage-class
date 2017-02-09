# Azure Kubernetes Storage Class

azure-disk.yaml contains a sample storage class for use with a Kubernetes cluster running
on Azure.

To use:

1. Spin up a kubernetes ACS cluster.  I recommend using the instructions with the Azure path on the [Deis Workflow site](https://deis.com/docs/workflow/quickstart/).
Follow them at least through the installation and initialization of `helm`.
2. Create a storage account on Azure that this K8s storage class will create persistent volumes in.
3. Create a top level container called 'vhds' in this storage acount (where persistent volumes will be stored).
4. Edit azure-disk.yaml to provide a name (eg. 'fast'), data center location (eg. 'eastus'), and storage account name (eg. 'acspremium').
5. Register this Storage Class with your Kubernetes cluster using `kubectl create -f azure-disk.yaml`.

You can then use this storage class with deployments.  For example, to deploy Redis on the cluster with premium storage disks with helm:

`# helm install --name redis --namespace redis --set persistence.storageClass=fast --set persistence.size=4Gi stable/redis`
