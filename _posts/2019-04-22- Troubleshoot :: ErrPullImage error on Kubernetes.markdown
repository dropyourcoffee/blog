---
layout: post
title:  "Troubleshoot :: ErrPullImage error on Kubernetes"
date:   2019-04-22 11:43:53 +0900
tags: Docker Kubernetes
categories: Linux 
---

When generally managing containerized apps at work, container images are maintained on private docker registry.

According to a [blog I found](https://gardener.cloud/050-tutorials/content/howto/missing-registry-permission/), Pod with a status of either 'ErrPullImage' or 'ImagePullBackOff' are caused by two reasons :

 - Specifying the wrong container image
 - Trying to use private images without providing registry credentials.


Renaming wrong container image is pretty straight forward.
if absence of the registry credentials is the case, I need to add a secret to pass.

In order to create a new secret,
```bash
kubectl create secret docker-registry dockersecret --docker-server=https://index.docker.io/v1/ --docker-username=<username> --docker-password=<password> --docker-email=<emailj>
```

New added secret can be confirmed by,
```bash
kubectl get secret docker-registry --output=yaml
# OR
kubectl get secret docker-registry --output="jsonpath={.data.\.dockerconfigjson}" | base64 -d
```

Describe the secret file in YAML file in `.spec.template.spec.containers.imagePullSecrets`
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: A_POD
spec:
  containers:
  - name: container-name
    image: <registry URL>/<image Name>:<image Tag>
  imagePullSecrets:
  - name: docker-registry
```