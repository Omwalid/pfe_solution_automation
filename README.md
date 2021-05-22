# pfe_solution_automation
scripts to install free5gmano + terraform file to provision 2 VMs in Azure

## steps : 
1- get_right_kernel_version → master and worker → reboot <br/>
2- prepare_node → master and worker <br/>
3- <br/>
master : <br/>
<pre>
   kubeadm init --pod-network-cidr=10.244.0.0/16 <br/> 
   as regular user : <br/>
     mkdir -p $HOME/.kube <br/>
     sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config <br/>
     sudo chown $(id -u):$(id -g) $HOME/.kube/config <br/>
     kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml <br/>
     kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/k8s-manifests/kube-flannel-legacy.yml  <br/>  
     kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/k8s-manifests/kube-flannel-rbac.yml <br/>
     kubectl taint nodes --all node-role.kubernetes.io/master- <br/>
</pre>

worker: <br/>
<pre>
     kubeadm join …. <br/>
     vi .kube/config → we copy config from master <br/>
 </pre>

PS : make sure worker is ready, and all pods are up (coredn, flannel …) <br/> 

4- <br/>
master : intall_kube5gnfvo <br/>
worker : setup_ovs_worker <br/>

5- deploy_kube5gnfvo <br/>

6- install_kafka <br/>

7- deploy free5gmano : voir free5gmano github (with kubernetes) <br/>

8- install_free5gmano_cli <br/>

9- Apply a NSSI <br/>
<pre>
     cd && git clone https://github.com/free5gmano/simpleexampleplugin.git <br/>
     vi simpleexampleplugin/config.yaml → configure hosts <br/>
     configure host and port in free5gmano-cli/nm/settings.py
</pre>

10- apply nssi → github <br/>
