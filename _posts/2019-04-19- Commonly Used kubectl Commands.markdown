---
layout: post
title:  "Commonly Used kubectl Commands"
date:   2019-04-19 11:43:53 +0900
tags: Docker Kubernetes
categories: Linux 
---

Add more later.

 - Get (all | deployment | pod | service) running on the cluster.
```bash
kubectl get all
kbuectl get deploy
kubectl get po
kubectl get svc
```

 - View Config
```bash
kubectl config view
```

 - Scale Replicaset
 ```bash
kubectl scale deployment hello-node --replicas=0 -n=kube-system
```

 - Rollout Update / Rollback
```bash
kubectl set image deployment/hello-node hello-node=hello-node:v4
kubectl rollout undo deployments hello-node
```

 - Tail -f log of a pod
```bash
kubectl logs -f <pod name>
```

 - execute a command in a pod.
```bash
kubectl exec <pod name> — sh -c ‘ls-al'
kubectl exec -it <POD 이름> <명령>
kubectl exec -it jenkins-5566cc5fdc-9cgsp hostname
kubectl exec -it jenkins-5566cc5fdc-9cgsp -- /bin/bash
```

 - Create configMap
```bash
kubectl create configmap <configmap name> —from-file=<file name>
```

 - Create Secret 만들기
```bash
kubectl create secret generic <secret name> —from-literal=<Content>
kubectl create secret generic <secret name> —from-literal=password=changeme
```

