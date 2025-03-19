Finding static pods: 

kubectl get pods --all-namespaces 
Then, find pods with controlplane 
ex) kube-apiserver-controlplane


Files locations: 
/etc/kubernetes/manifestss
---
Q: Create a static pod named static-busybox that uses the busybox image and the command sleep 1000

Name: static-busybox
Image: busybox

A:
```
kubectl run --restart=Never --image=busybox static-busybox --dry-run=client -o yaml --command -- sleep 1000 > /etc/kubernetes/manifests/static-busybox.yaml
```

Editing static-pod
kubectl run --restart=Never --image=busybox:1.28.4 static-busybox --dry-run=client -o yaml --command -- sleep 1000 > /etc/kubernetes/manifests/static-busybox.yaml