### Update the hosts file
```
vim /etc/hosts
    172.16.7.235	kmaster1
    172.16.7.236	kworker1
    172.16.7.237	kworker2
```

### Add GPG key
```
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.30/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
```


### Update the source file
```
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.30/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
```

### Update the all packages
```
apt update -y
```

### Install Kubernetes Tools
```
apt install kubeadm kubelet kubectl -y
```


### Check the kubeadm version
```
kubeadm version
```

### Check the Kubectl version
```
kubectl version
```

### Check theu Kubelet version
```
kubelet --version
```

### Disable the swap space. Also remove the swap entry from '/etc/fstab'
```
swapoff -a
```


### Load the required modules
```
vim /etc/modules-load.d/k8s.conf
    overlay
    br_netfilter
```


### Reload the modules
```
modprobe overlay
modprobe br_netfilter
```


### Check the module status
```
lsmod | grep over
lsmod | grep br_netfilter
```


### Enable the ip forwarding
```
vim /etc/sysctl.d/10-k8s.conf
    net.bridge.bridge-nf-call-ip6tables = 1
    net.bridge.bridge-nf-call-iptables = 1
    net.ipv4.ip_forward = 1
```

### Reload this configuration
```
sysctl --system
```

### Check the docker driver. If  "Cgroup Driver: systemd", then it's okay.
```
docker info | grep -i driver
```


###  If "Cgroup Driver: cgroup" then change it by below cmd
```
vim /etc/default/kubelet
    KUBELET_EXTRA_ARGS="--cgroup-driver=cgroupfs"
```

### Reload the daemons
```
systemctl daemon-reload
```


### Restart the kubelet service
```
systemctl restart kubelet.service
```

### Remove the '/etc/containerd/config.toml'
```
rm -rf /etc/containerd/config.toml
```


### Restart the containerd service
```
systemctl restart containerd.service
```


### Initialize the kubeadm by using pod cidr
```
kubeadm init --pod-network-cidr=10.244.0.0/16
```

**_Please preserve the outputs in a text file for further use_**


### Update the bashrc file for to connect the cluster by kubectl command
```
export KUBECONFIG=/etc/kubernetes/admin.conf
```

### To enable the tab completion for kubectl
```
kubectl completion bash | sudo tee /etc/bash_completion.d/kubectl > /dev/null
```


### Download and apply the flannel for network plugins.
```
wget https://github.com/flannel-io/flannel/releases/latest/download/kube-flannel.yml
```

### We can update this file if we initiate the kubeadm with different prefix. Run the kube-flannel file
```
kubectl create -f kube-flannel.yml
```

### Download the tigra operator and calico plugins.
```Actionscript
wget https://docs.projectcalico.org/manifests/tigera-operator.yaml
wget https://docs.projectcalico.org/manifests/custom-resources.yaml
```

### Lights up the tigra operator
```Actionscript
kubectl create -f tigera-operator.yaml
```

### Update the calico custom resource file on CIDR section and lights up
```Actionscript
kubectl create -f calico-custom-resources.yaml
```

### Check the all pods
```
kubectl get pods -A -o wide
```

### Create a token if you forget the current token
```
kubeadm token create --print-join-command
```