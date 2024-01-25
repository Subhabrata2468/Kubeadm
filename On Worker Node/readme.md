# Kubeadm Installation on Debian (WORKER NODE)

Installing Kubeadm on Debian involves setting up Kubernetes and then deploying Kubeam. 

* Prerequisites
    -  1 or 2 CPUS
    -  1 or 2 Gb RAM
    -  Network Connectivity
    -  Disable swap


#### Step 1 
Install Docker

```bash
sudo apt-get update
```
```bash
sudo apt-get install -y docker.io
```
#### Step 2
Turn off the swap

```bash
sudo swapoff -a
```

#### Step 3
Enable ,start and to see status of Docker

```bash
sudo systemctl enable docker
```
```bash
sudo systemctl start docker
```
```bash
sudo systemctl status docker
```

#### Step 4
Install Kubernetes _DO 3 to 4 times for safety_

```bash
sudo apt-get update && sudo apt-get install -y apt-transport-https
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
echo "deb http://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
```
```bash
sudo apt-get update
```
```bash
sudo apt-get install -y kubelet kubeadm kubectl
```

#### Step 5 (Applies to only workers node)
**NOTE -_ The only Token that come from master node only_**
```bash
kubeadm join 10.9.0.70:6443 --token drjha1.c34h63hpq6dya971 \
        --discovery-token-ca-cert-hash sha256:cfaf9590515c3c6bc023b1df20d476ce7d70695d768c786d77a79100c1b56da8 
```

#### Step 6 (Applies to only master node)
For verifying that both the master and worker nodes are working fine
```bash
kubectl get nodes
```


## Author

- ** _Subhabrata_ **
