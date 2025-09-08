### **📌 CKA Exam Essential `kubectl` Commands (README.md)**

## 📌 Key Points for CKA Exam
- **Speed is crucial!** Use `kubectl` to generate YAML files and modify them instead of writing from scratch.
- **Troubleshooting is a must!** Be able to check pod status, logs, and debug common issues.
- **`etcd` backup & restore frequently appears in the exam.**
- **Understand different Service types:** `NodePort`, `LoadBalancer`, `ClusterIP`.
- **RBAC configurations may be tested!** Learn `Role` and `RoleBinding`.

## **1️⃣ Pod Management**
### ✅ **Create a Pod**
```bash
kubectl run redis --image=redis:alpine --labels="tier=db"
```
- **Pod Name:** `redis`
- **Image:** `redis:alpine`
- **Label:** `tier=db`

### ✅ **List All Pods**
```bash
kubectl get pods --show-labels
```

### ✅ **Describe a Pod**
```bash
kubectl describe pod redis
```

### ✅ **Delete a Pod**
```bash
kubectl delete pod redis
```

---

## **2️⃣ Deployment & ReplicaSet**
### ✅ **Create a Deployment**
```bash
kubectl create deployment nginx-deploy --image=nginx --replicas=3
```
- **Deployment Name:** `nginx-deploy`
- **Image:** `nginx`
- **Replicas:** `3`

### ✅ **Generate Deployment YAML and Modify**
```bash
kubectl create deployment my-app --image=nginx --dry-run=client -o yaml > my-app.yaml
kubectl apply -f my-app.yaml
```

### ✅ **Scale a Deployment**
```bash
kubectl scale deployment nginx-deploy --replicas=5
```

### ✅ **Update Deployment Image**
```bash
kubectl set image deployment/nginx-deploy nginx=nginx:1.19
```

---

## **3️⃣ Service Configuration**
### ✅ **Expose a Deployment as a NodePort Service**
```bash
kubectl expose deployment nginx-deploy --port=80 --target-port=80 --type=NodePort
```
- **Check the assigned NodePort**
```bash
kubectl get services
```
📌 **Access using:** `http://<Node-IP>:<NodePort>`

### ✅ **Expose a Deployment as a LoadBalancer (Cloud Only)**
```bash
kubectl expose deployment nginx-deploy --port=80 --target-port=80 --type=LoadBalancer
```

---

## **4️⃣ Troubleshooting & Debugging**
### ✅ **Check Pod Status**
```bash
kubectl get pods
```

### ✅ **Describe a Pod to check errors**
```bash
kubectl describe pod <pod-name>
```

### ✅ **Check Logs of a Pod**
```bash
kubectl logs <pod-name>
```

### ✅ **Access Pod Container Shell**
```bash
kubectl exec -it <pod-name> -- /bin/sh
```

### ✅ **View Events Sorted by Time**
```bash
kubectl get events --sort-by=.metadata.creationTimestamp
```



