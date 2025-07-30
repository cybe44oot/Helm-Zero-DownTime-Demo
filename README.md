# 🛡️ Zero Downtime Helm Upgrade Demo

This mini Helm project demonstrates how to deploy a Kubernetes application (NGINX) using Helm with **zero downtime** during upgrades. It focuses on:

- ✅ Readiness & Liveness Probes  
- ✅ Rolling Update strategy  
- ✅ Safe upgrade behavior using Kubernetes best practices  

> ⚠️ This project **does not include a Service** object — it's focused purely on Deployment behavior.

---

## 📁 Project Structure

helm-zero-downtime-demo/

├── Chart.yaml

├── values.yaml

└── templates/
  
  └── deployment.yaml


  # 🚀 How to Deploy

  ## 1- install the chart :

  ``` yaml

helm install demo ./helm-zero-downtime-demo
```
  ## 2- Verify pods are running:
```yaml
kubectl get pods -l app=zero-downtime-demo
```
#  How to Upgrade Without Downtime:
## 1- Open values.yaml and update the image tag:

from 1.25 to 1.26 for example

```yaml
tag: "1.26"
```
## 2- run the upgrade :

```yaml
helm upgrade demo ./helm-zero-downtime-demo
```

During this upgrade:

New pods will be created.

New pods must pass the readiness probe before traffic goes to them.

Old pods are only removed after new ones are ready.

Liveness probe ensures unhealthy pods are restarted automatically.

✅ This ensures zero downtime for your app during the upgrade.

