Q: We have deployed a number of PODs. They are labelled with tier, env and bu. How many PODs exist in the dev environment (env)?


A: 
```
kubectl get pods --selector env=dev --no-headers | wc -l
```


Q: Identify the POD which is part of the prod environment, the finance BU and of frontend tier?

A: 
```
kubectl get all --selector env=prod,bu=finance,tier=frontend
```