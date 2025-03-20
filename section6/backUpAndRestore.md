Q: What is the version of ETCD running on the cluster?
A: kubectl -n kube-system describe pod etcd-controlplane | grep Image:

Q: At what address can you reach the ETCD cluster from the controlplane node?
A: kubectl -n kube-system describe pod etcd-controlplane | grep '\--listen-client-urls'

Q: The master node in our cluster is planned for a regular maintenance reboot tonight. While we do not anticipate anything to go wrong, we are required to take the necessary backups. Take a snapshot of the ETCD database using the built-in snapshot functionality.
A: ETCDCTL_API=3 etcdctl --endpoints=https://[127.0.0.1]:2379 \
> --cacert=/etc/kubernetes/pki/etcd/ca.crt \
--cert=/etc/kubernetes/pki/etcd/server.crt \
--key=/etc/kubernetes/pki/etcd/server.key \
> snapshot save /opt/snapshot-pre-boot.db
Snapshot saved at /opt/snapshot-pre-boot.db


---
### 2
Q: Before proceeding to the next question, explore the student-node and the clusters it has access to.

$ hostname
$ kubectl version --client
$ kubectl config get-contexts
$ kubectl get nodes

$ kubectl get pods -n kube-system |grep etcd