# Set up a Highly Available Kubernetes Cluster using kubeadm
Follow this documentation to set up a highly available Kubernetes cluster using __Ubuntu 16.04 LTS__.

This documentation guides you in setting up a cluster with two master nodes, one worker node and a load balancer node using HAProxy.

## Vagrant Environment
|Role|FQDN|IP|OS|RAM|CPU|
|----|----|----|----|----|----|
|Load Balancer|loadbalancer.example.com|172.16.16.100|Ubuntu 16.04|1G|1|
|Master|kmaster1.example.com|172.16.16.101|Ubuntu 16.04|2G|2|
|Master|kmaster2.example.com|172.16.16.102|Ubuntu 16.04|2G|2|
|Worker|kworker1.example.com|172.16.16.201|Ubuntu 16.04|1G|1|

> * Password for the **root** account on all these virtual machines is **kubeadmin**
> * Perform all the commands as root user unless otherwise specified

## Pre-requisites
If you want to try this in a virtualized environment on your workstation
* Virtualbox installed
* Vagrant installed
* Host machine has atleast 8 cores
* Host machine has atleast 8G memory

## Bring up all the virtual machines
```
vagrant up
```

## Set up load balancer node
##### Install Haproxy
```
apt update && apt install -y haproxy
```
##### Configure haproxy
Append the below lines to **/etc/haproxy/haproxy.cfg**
```
frontend kubernetes-frontend
    bind 172.16.16.100:6443
    mode tcp
    option tcplog
    default_backend kubernetes-backend

backend kubernetes-backend
    mode tcp
    option tcp-check
    balance roundrobin
    server kmaster1 172.16.16.101:6443 check fall 3 rise 2
    server kmaster2 172.16.16.102:6443 check fall 3 rise 2
```
##### Restart haproxy service
```
systemctl restart haproxy
```

## On all kubernetes nodes (kmaster1, kmaster2, kworker1)
##### Disable Firewall
```
ufw disable
```
##### Disable swap
```
swapoff -a; sed -i '/swap/d' /etc/fstab
```
##### Update sysctl settings for Kubernetes networking
```
cat >>/etc/sysctl.d/kubernetes.conf<<EOF
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
EOF
sysctl --system
```
##### Install docker engine
```
{
  apt install -y apt-transport-https ca-certificates curl gnupg-agent software-properties-common
  curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -
  add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
  apt update && apt install -y docker-ce=5:19.03.10~3-0~ubuntu-focal containerd.io
}
```
### Kubernetes Setup
##### Add Apt repository
```
{
  curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
  echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" > /etc/apt/sources.list.d/kubernetes.list
}
```
##### Install Kubernetes components
```
apt update && apt install -y kubeadm=1.19.2-00 kubelet=1.19.2-00 kubectl=1.19.2-00
```

## Skip the above steps & excute the bootstap script: 
```
./bootstrap.sh 
```

## On any one of the Kubernetes master node (Eg: kmaster1)
##### Initialize Kubernetes Cluster
```
kubeadm init --control-plane-endpoint="172.16.16.100:6443" --upload-certs --apiserver-advertise-address=172.16.16.101 --pod-network-cidr=192.168.0.0/16
```
Copy the commands to join other master nodes and worker nodes.
##### Deploy Calico network
```
kubectl --kubeconfig=/etc/kubernetes/admin.conf create -f https://docs.projectcalico.org/v3.15/manifests/calico.yaml
```

## Join other nodes to the cluster (kmaster2 & kworker1)
> Use the respective kubeadm join commands you copied from the output of kubeadm init command on the first master.

> IMPORTANT: You also need to pass --apiserver-advertise-address to the join command when you join the other master node.

## Downloading kube config to your local machine
On your host machine
```
mkdir ~/.kube
scp root@172.16.16.101:/etc/kubernetes/admin.conf ~/.kube/config
```
Password for root account is kubeadmin (if you used my Vagrant setup)

## Verifying the cluster
```
kubectl cluster-info
kubectl get nodes
kubectl get cs
```

## Node Status
```
root@kmaster1:~ # kubectl  get nodes
NAME       STATUS   ROLES                  AGE     VERSION
kmaster1   Ready    control-plane,master   86m     v1.21.0
kmaster2   Ready    control-plane,master   84m     v1.21.0
kmaster3   Ready    control-plane,master   83m     v1.21.0
kworker1   Ready    <none>                 5m23s   v1.21.0
kworker2   Ready    <none>                 5m19s   v1.21.0
root@kmaster1:~ #

```

## Control Plan Pod Status
```
root@kmaster1:~ # kubectl  get pod -n kube-system
NAME                                       READY   STATUS    RESTARTS   AGE
calico-kube-controllers-7676785684-tlddr   1/1     Running   0          83m
calico-node-47hlt                          1/1     Running   0          83m
calico-node-dnr5m                          1/1     Running   0          6m42s
calico-node-n8thh                          1/1     Running   0          83m
calico-node-vrcl4                          1/1     Running   0          6m38s
calico-node-zjhlk                          1/1     Running   0          83m
coredns-558bd4d5db-425sr                   1/1     Running   0          87m
coredns-558bd4d5db-ldrr4                   1/1     Running   0          87m
etcd-kmaster1                              1/1     Running   0          88m
etcd-kmaster2                              1/1     Running   0          85m
etcd-kmaster3                              1/1     Running   0          84m
kube-apiserver-kmaster1                    1/1     Running   0          88m
kube-apiserver-kmaster2                    1/1     Running   0          85m
kube-apiserver-kmaster3                    1/1     Running   0          84m
kube-controller-manager-kmaster1           1/1     Running   2          88m
kube-controller-manager-kmaster2           1/1     Running   1          85m
kube-controller-manager-kmaster3           1/1     Running   0          84m
kube-proxy-6s74b                           1/1     Running   0          85m
kube-proxy-gtthd                           1/1     Running   0          87m
kube-proxy-jnxlh                           1/1     Running   0          6m38s
kube-proxy-qvbcd                           1/1     Running   0          84m
kube-proxy-wf7bd                           1/1     Running   0          6m42s
kube-scheduler-kmaster1                    1/1     Running   2          88m
kube-scheduler-kmaster2                    1/1     Running   1          85m
kube-scheduler-kmaster3                    1/1     Running   0          84m
root@kmaster1:~ #
```

## Deployment of App
```
kubectl apply -f 01-helloworld.yaml 
```
```
root@kmaster1:~ # kubectl  get deploy,pods
NAME                                       READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/python-webapp-deployment   3/3     3            3           33s

NAME                                            READY   STATUS    RESTARTS   AGE
pod/python-webapp-deployment-5679955cb7-h5zl2   1/1     Running   0          33s
pod/python-webapp-deployment-5679955cb7-llg27   1/1     Running   0          33s
pod/python-webapp-deployment-5679955cb7-z76ng   1/1     Running   0          33s
root@kmaster1:~ #

```

## Expose the Service & Check the App Status
```
root@kmaster1:~/k8s-ckad-philips-03-Oct-2022# kubectl  get svc
NAME                TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)           AGE
kubernetes          ClusterIP   10.96.0.1      <none>        443/TCP           92m
python-webapp-svc   NodePort    10.108.48.16   <none>        31007:31007/TCP   74s
root@kmaster1:~/k8s-ckad-philips-03-Oct-2022#
```
```
root@kmaster1:~# kubectl  get pods -o wide
NAME                                        READY   STATUS    RESTARTS   AGE     IP               NODE       NOMINATED NODE   READINESS GATES
python-webapp-deployment-5679955cb7-h5zl2   1/1     Running   0          3m17s   192.168.77.131   kworker2   <none>           <none>
python-webapp-deployment-5679955cb7-llg27   1/1     Running   0          3m17s   192.168.77.130   kworker2   <none>           <none>
python-webapp-deployment-5679955cb7-z76ng   1/1     Running   0          3m17s   192.168.41.130   kworker1   <none>           <none>
root@kmaster1:~#

root@kmaster1:~# curl 172.16.16.101:31007/info
<h2> Hey Python Web Server</h2><b> Hostname: </b> python-webapp-deployment-5679955cb7-llg27<br/><b> IP Address: </b> 192.168.77.130<br/>
root@kmaster1:~# curl 172.16.16.101:31007/info
<h2> Hey Python Web Server</h2><b> Hostname: </b> python-webapp-deployment-5679955cb7-h5zl2<br/><b> IP Address: </b> 192.168.77.131<br/>
root@kmaster1:~# curl 172.16.16.101:31007/info
<h2> Hey Python Web Server</h2><b> Hostname: </b> python-webapp-deployment-5679955cb7-z76ng<br/><b> IP Address: </b> 192.168.41.130<br/>
root@kmaster1:~#

```



Have Fun!!

