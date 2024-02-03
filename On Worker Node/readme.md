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

#### Step 3
Installing apt-transport-https

```bash
sudo apt-get update && sudo apt-get install -y apt-transport-https
```

Download the Kubernetes GPG key
```bash
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | gpg --dearmor -o /usr/share/keyrings/kubernetes-archive-keyring.gpg
```

Add the Kubernetes repository using signed-by option
```bash
echo "deb [signed-by=/usr/share/keyrings/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
```

Update the package list
```bash
sudo apt-get update
```

Installing kubeadm,kubelet,kubectl
Can change the version according to your requirements 
```bash
sudo apt-get install -y kubelet=1.23.0-00 kubeadm=1.23.0-00 kubectl=1.23.0-00
```

#### Step 4
Turn off the swap

```bash
sudo swapoff -a
```
To turn off swap permanently
```bash
sudo sed -i '/ swap / s/^/#/' /etc/fstab
```

#### Step 5 (Applies to only workers node)
**NOTE -_ The only Token that come from master node only_**
```bash
kubeadm join 10.9.0.70:6443 --token drjha1.c34h63hpq6dya971 \
        --discovery-token-ca-cert-hash sha256:cfaf9590515c3c6bc023b1df20d476ce7d70695d768c786d77a79100c1b56da8 
```

#### Step 6 (Applies to only master node)
For verifying that both the master and worker nodes are working fine (cmd must be written in master node)
```bash
kubectl get nodes
```


## Author

- ** _Subhabrata_ **
