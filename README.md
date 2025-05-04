# argocd-tutorial-projects

Sure! Here's a polished and concise rewrite of your Argo CD installation guide:

---

### ArgoCD Installation: Quick Start Guide

Argo CD is a declarative, GitOps-based continuous delivery tool for managing Kubernetes applications. It ensures application configurations remain in sync by comparing the desired state in Git with the live state in your cluster.

### Cloud Native Foundation's Argo Project  
Argo CD is part of the CNCF’s Argo Project, which also includes:
- **Argo Workflow** – Automates complex workflows.
- **Argo Rollouts** – Enables progressive delivery.
- **Argo Events** – Event-driven automation.

### Installation Steps  

#### 1. Upgrade Packages & Install Prerequisites  
Before proceeding, ensure your packages are up to date.  

#### 2. Install ArgoCD  
```bash
kubectl create namespace argocd  
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml  
```

#### 3. Configure Service to NodePort  
Change the service type from **ClusterIP** to **NodePort**:
```bash
kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "NodePort"}}'  
```

#### 4. Retrieve Initial Admin Password  
```bash
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d  
```

#### 5. Deploy Demo Application  
Use the following repository to deploy a demo **nginx** application:  
[ArgoCD Tutorial Repository](https://github.com/dmancloud/argocd-tutorial)  

#### 6. Scale ReplicaSet  
Increase replicas for **nginx** deployment:  
```bash
kubectl scale --replicas=3 deployment nginx -n default  
```

#### 7. Clean Up  
Remove Argo CD and associated resources:  
```bash
kubectl delete -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml  
kubectl delete namespace argocd  
```
