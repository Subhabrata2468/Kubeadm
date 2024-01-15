# Kubeam Installation on Debian (MASTER NODE)

Installing Kubeam on Debian involves setting up Kubernetes and then deploying Kubeam. 

* Prerequisites
    -  2 CPUS
    -  2 Gb RAM
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
Install Kubernetes

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

#### Step 5
Pull kubeadm images from docker

```bash
kubeadm config images pull
```

#### Step 6 
Initialize Kubernetes

```bash
sudo kubeadm init
```

#### Step 7
Set up kubeconfig
```bash
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

#### Step 8
_Install a network plugin. You can choose a CNI (Container Network Interface) plugin. Calico is a common choice_
```bash
kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml
```

#### Step 9 (Applies to only workers node)
**Then you can join any number of worker nodes by running the following on each as root:**
**NOTE- THE CODE THAT IS AVAILABLE BELOW MAY DIFFER FORM SERVER TO SERVER SO YOU HAVE TO CHANGE ACCORDINGLY BUT MUST BE DONE ONLY  ONCE**
```bash
kubeadm join 10.9.0.70:6443 --token drjha1.c34h63hpq6dya971 \
        --discovery-token-ca-cert-hash sha256:cfaf9590515c3c6bc023b1df20d476ce7d70695d768c786d77a79100c1b56da8 
```
**_Token may differ_**
### TO VERIFY IF NODES, PODS ARE WORKING OR NOT

#### Step 10
Check Nodes
```bash
kubectl get nodes
```
**_This should show the status of your nodes. If STATUS is Ready, your nodes are functioning correctly._**

#### Step 11
Check Pods
```bash
kubectl get pods --all-namespaces
```
**_Ensure that the essential pods are in the Running state, especially those in the kube-system namespace._**

#### Step 12
Check Control Plane Components
```bash
kubectl get componentstatuses
```
**_Verify that the control plane components (etcd, scheduler, controller-manager) are in the Healthy state._**

### INCASE OF ANY FAILURE

#### Step 10
Clean up node configuration
```bash
kubeadm reset
```
**_This will attempt to revert changes made by kubeadm init or kubeadm join on the node, removing Kubernetes configuration and certificates_**





## Author

- ** _Subhabrata_ **
