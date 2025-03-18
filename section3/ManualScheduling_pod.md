How to schedule a pod manually:

```
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  nodeName: node01  # scheduling manually
  containers:
  -  image: nginx
     name: nginx
```