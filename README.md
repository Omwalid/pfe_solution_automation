# pfe_solution_automation
scripts to install free5gmano + terraform file to provision 2 VMs in Azure

## steps : 
1- get_right_kernel_version → master and worker → reboot
2- prepare_node → master and worker 
3- 
master :
kubeadm init --pod-network-cidr=10.244.0.0/16 
as regular user :
  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config
kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/k8s-manifests/kube-flannel-legacy.yml    
kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/k8s-manifests/kube-flannel-rbac.yml
kubectl taint nodes --all node-role.kubernetes.io/master-
worker:
kubeadm join ….
vi .kube/config → we copy config from master

PS : make sure worker is ready, and all pods are up (coredn, flannel …) 

4- 
master :
intall_kube5gnfvo
worker :
setup_ovs_worker

5- deploy_kube5gnfvo
6- install_kafka
7- deploy free5gmano : voir free5gmano github (with kubernetes)
8- install_free5gmano_cli
9- Apply a NSSI
cd && git clone https://github.com/free5gmano/simpleexampleplugin.git
vi simpleexampleplugin/config.yaml → configure hosts
configure host and port in free5gmano-cli/nm/settings.py
10- apply nssi → github
