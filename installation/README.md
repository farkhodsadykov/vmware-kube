# Kubernetes Cluster Install on Ubuntu
## Dependents Packages 
```
test -e /usr/bin/python || (apt -y update && apt install -y python-minimal)
ufw disable
cp /etc/fstab /root/fstab
sed -i /"swap"/d /etc/fstab
swapoff -a
apt-get install linux-generic
sudo apt-get install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu xenial stable"
sudo apt-get update
apt-get install docker-ce=17.12.1~ce-0~ubuntu
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" > /etc/apt/sources.list.d/kubernetes.list
sudo apt-get update
apt-get install kubelet kubeadm kubectl -y 
systemctl start kubelet
```

# Master Cluster
```
apt-get install -y vim wget telnet dnsutils elinks
kubeadm init /etc/kubernetes/admin.conf
mkdir -p $HOME/.kube
chmod 0755 $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
kubectl apply -f https://cloud.weave.works/k8s/net?k8s-version=$(kubectl version | base64 | tr -d '\n')
```

## Nodes run following command 
```
kubeadm token create --print-join-command
```


# Check server 
```
kubectl get nodes
```

