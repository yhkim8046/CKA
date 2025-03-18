Q:Do any taints exist on node01 node?
A: kubectl describe node node01 | grep -i taints

Q: Create a taint on node01 with key of spray, value of mortein and effect of NoSchedule
A: kubectl taint nodes node01 spray=mortein:NoSchedule --overwrite=true


Q: Dry run for creating a pod
A: kubectl run mosquito --image=nginx --dry-run=client -o yaml > pod.yaml


Q: Create another pod named bee with the nginx image, which has a toleration set to the taint mortein.
A: 

Step 1: kubectl run bee --image=nginx --dry-run=client -o yaml > bee.yaml
Step 2: Edit file to add toleration
```
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: bee
  name: bee
spec:
  containers:
  - image: nginx
    name: bee
    resources: {}
  tolerations:
  - key: "spray"
    operator: "Equal"
    value: "mortein"
    effect: "NoSchedule"   
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}
```
 
link: https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/



Q: Remove the taint on controlplane, which currently has the taint effect of NoSchedule.
A: kubectl taint nodes controlplane node-role.kubernetes.io/control-plane:NoSchedule-
node/controlplane untainted

Q: Update the deployment by running kubectl edit deployment blue and add the nodeaffinity section as follows:
- Name: blue
- Replicas: 3
- Image: nginx
- NodeAffinity: requiredDuringSchedulingIgnoredDuringExecution
- Key: color
- value: blue

A: 

---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: blue
spec:
  replicas: 3
  selector:
    matchLabels:
      run: nginx
  template:
    metadata:
      labels:
        run: nginx
    spec:
      containers:
      - image: nginx
        imagePullPolicy: Always
        name: nginx
      affinity:
        nodeAffinity:
          requiredDuringSchedulingIgnoredDuringExecution:
            nodeSelectorTerms:
            - matchExpressions:
              - key: color
                operator: In
                values:
                - blue
