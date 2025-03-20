Q: Recognise where the pods are set
A: kubectl get pods -o wide  

Q:What is the latest version available for an upgrade with the current version of the kubeadm tool installed?
A: kubeadm upgrade plan

Q:We will be upgrading the controlplane node first. Drain the controlplane node of workloads and mark it UnSchedulable

A: kubectl drain controlplane --ignore-daemonsets




### Upgrade the controlplane components to exact version v1.32.0

1. Open the file that defines the kubernetes apt repository  
$ vim /etc/apt/sources.list.d/kubernetes.list

2. Update the version in the URL 
$ deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.32/deb/ /

3. Save the file and exit from the text editor and update 
$ apt update 
$ apt-cache madison kubeadm 

4. upgrade kubeadm for kubernetes
$ apt-get install kubeadm=1.32.0-1.1

$ kubeadm upgrade plan v1.32.0
$ kubeadm upgrade apply v1.32.0

5. upgrade the kubelet version
$ apt-get install kubelet=1.32.0-1.1

6. refresh the systemd configurartion and apply chages to the kubelet service: 
$ systemctl daemon-reload
$ systemctl restart kubelet

---

Q: Mark the controlplane node as "Schedulable" again
A: $ kubectl uncordon controlplane