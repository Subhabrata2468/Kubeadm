# Kubeam Installation on Debian (BOTH MASTER NODE & WORKER NODE)

Installing Kubeadm on Debian involves setting up Kubernetes and then deploying Kubeam. 

* Prerequisites
    -  2 CPUS
    -  2 Gb RAM
    -  Network Connectivity
    -  Disable swap

`
#### Step 1
Turn off the swap

```bash
sudo swapoff -a
```

#### Step 2
...

```bash
sudo ufw allow 6443
```

### TO VERIFY IF NODES, PODS ARE WORKING OR NOT

#### Step 10
Check Nodes in master node 
```bash
kubectl get nodes
```
**_This should show the status of your nodes. If STATUS is Ready, your nodes are functioning correctly._**






## Author

- ** _Subhabrata_ **
