Here are the **Top 50 Kubernetes Interview Questions and Answers** curated specifically for someone with **5 years of experience**, focusing on both practical and advanced concepts used in real-world production environments.

---

## 🚀 Top 50 Kubernetes Interview Questions (5 Years Experience)

---

### ✅ **1. What is Kubernetes and why is it used?**
Kubernetes (K8s) is an open-source container orchestration platform that automates deployment, scaling, and management of containerized applications.

---

### ✅ **2. What are the main components of Kubernetes architecture?**
- **Master Node**: API Server, Controller Manager, Scheduler, etcd
- **Worker Node**: Kubelet, Kube Proxy, Container Runtime

---

### ✅ **3. What is a Pod in Kubernetes?**
A pod is the smallest deployable unit in Kubernetes. It encapsulates one or more containers that share storage/network.

---

### ✅ **4. What is a ReplicaSet?**
A ReplicaSet ensures a specified number of pod replicas are running at any time.

---

### ✅ **5. What is a Deployment in Kubernetes?**
A Deployment provides declarative updates for pods and ReplicaSets.

---

### ✅ **6. Difference between ReplicaSet and Deployment?**
- **ReplicaSet**: Maintains pod count
- **Deployment**: Manages ReplicaSet, supports rolling updates & rollbacks

---

### ✅ **7. What is a Namespace?**
Namespaces are virtual clusters within a Kubernetes cluster, used for environment isolation (dev/test/prod).

---

### ✅ **8. What is etcd in Kubernetes?**
etcd is a consistent and highly available key-value store used for all cluster data.

---

### ✅ **9. What is a Service in Kubernetes?**
A Service exposes a set of pods as a network service and provides load balancing.

---

### ✅ **10. Types of Services in Kubernetes?**
1. ClusterIP (default)
2. NodePort
3. LoadBalancer
4. ExternalName

---

### ✅ **11. What is a StatefulSet?**
Manages stateful applications; each pod gets a persistent identity and stable storage.

---

### ✅ **12. Difference between StatefulSet and Deployment?**
- **StatefulSet**: Unique pod identity, ordered deployment
- **Deployment**: Stateless pods, generic scaling

---

### ✅ **13. What is a DaemonSet?**
Ensures that a pod runs on all (or selected) nodes in the cluster (e.g., log collector).

---

### ✅ **14. What is a Job in Kubernetes?**
A Job creates pods to run tasks until completion (used for batch processing).

---

### ✅ **15. What is a CronJob?**
Schedules Jobs to run periodically on a given time schedule.

---

### ✅ **16. What is a ConfigMap?**
Stores non-confidential key-value pairs for configuration purposes.

---

### ✅ **17. What is a Secret?**
Stores sensitive information like passwords, tokens, and SSH keys.

---

### ✅ **18. How does Kubernetes do service discovery?**
Using environment variables or DNS (CoreDNS) within the cluster.

---

### ✅ **19. What is kubelet?**
An agent that runs on each worker node, ensuring containers are running as expected.

---

### ✅ **20. What is kube-proxy?**
Handles network routing and load balancing to services across pods.

---

### ✅ **21. How does Kubernetes handle load balancing?**
- Internal via kube-proxy
- External via Ingress Controllers or LoadBalancer service type

---

### ✅ **22. What is Ingress in Kubernetes?**
Ingress manages external access to services, typically via HTTP/HTTPS, and supports routing, TLS, etc.

---

### ✅ **23. What is a PersistentVolume (PV) and PersistentVolumeClaim (PVC)?**
- **PV**: Actual storage resource
- **PVC**: Request for storage by a pod

---

### ✅ **24. Explain Init Containers.**
Init containers run before app containers and are used for setup tasks.

---

### ✅ **25. What is a Sidecar container pattern?**
A sidecar is an auxiliary container that extends or enhances the primary container’s functionalities (e.g., logging agent).

---

### ✅ **26. How do you perform a rolling update in Kubernetes?**
Using `kubectl apply -f deployment.yaml` or updating the Deployment object, which triggers a controlled rollout.

---

### ✅ **27. How to rollback a failed deployment?**
```bash
kubectl rollout undo deployment my-deployment
```

---

### ✅ **28. What are taints and tolerations?**
Taints repel pods from nodes, and tolerations allow pods to be scheduled on tainted nodes.

---

### ✅ **29. What are Node Affinity and Anti-Affinity?**
They control pod placement based on labels of nodes (affinity) or not co-locating pods (anti-affinity).

---

### ✅ **30. What is Horizontal Pod Autoscaler (HPA)?**
Automatically scales the number of pods based on metrics like CPU or custom metrics.

---

### ✅ **31. What is Vertical Pod Autoscaler (VPA)?**
Adjusts CPU/memory resource requests/limits for pods automatically.

---

### ✅ **32. What is Cluster Autoscaler?**
Scales the number of nodes in a cluster based on pending pods or unused nodes.

---

### ✅ **33. What is Helm in Kubernetes?**
Helm is a package manager for Kubernetes. It uses **charts** to define, install, and upgrade complex Kubernetes applications.

---

### ✅ **34. What is a Helm Chart?**
A Helm Chart is a package of pre-configured Kubernetes resources.

---

### ✅ **35. How does Kubernetes ensure high availability?**
- Multi-master setup
- Pod replication
- Health checks and self-healing
- Node autoscaling

---

### ✅ **36. How does Kubernetes perform health checks?**
- **Liveness Probe**: Checks if app is alive
- **Readiness Probe**: Checks if app is ready to receive traffic
- **Startup Probe**: Checks if app has started

---

### ✅ **37. How is RBAC implemented in Kubernetes?**
RBAC (Role-Based Access Control) defines access policies via **Roles**, **RoleBindings**, **ClusterRoles**, and **ClusterRoleBindings**.

---

### ✅ **38. How to debug a CrashLoopBackOff error?**
- Check logs: `kubectl logs pod-name`
- Describe pod: `kubectl describe pod pod-name`
- Use `kubectl exec` for live debugging

---

### ✅ **39. What is a ResourceQuota?**
Limits resource usage (CPU, memory, number of objects) in a namespace.

---

### ✅ **40. What is a LimitRange?**
Sets default/min/max resource requests and limits per container in a namespace.

---

### ✅ **41. How do you scale a Deployment manually?**
```bash
kubectl scale deployment my-app --replicas=5
```

---

### ✅ **42. What is the difference between request and limit in pod resources?**
- **Request**: Guaranteed minimum
- **Limit**: Maximum allowed

---

### ✅ **43. What is a ServiceAccount in Kubernetes?**
ServiceAccount provides identity to a pod to interact with the Kubernetes API.

---

### ✅ **44. How does Kubernetes handle secrets securely?**
Secrets are base64-encoded and can be encrypted at rest. Use RBAC and avoid storing secrets in image.

---

### ✅ **45. What is the role of the Kubernetes Scheduler?**
Assigns pods to appropriate nodes based on resource requirements, constraints, taints/tolerations, etc.

---

### ✅ **46. What is a Custom Resource Definition (CRD)?**
CRDs let you define custom resources to extend Kubernetes functionality.

---

### ✅ **47. What is a Kubernetes Operator?**
Operators extend Kubernetes by automating application-specific operations using CRDs and controllers.

---

### ✅ **48. How to back up and restore etcd in Kubernetes?**
Use `etcdctl`:
```bash
etcdctl snapshot save snapshot.db  
etcdctl snapshot restore snapshot.db
```

---

### ✅ **49. How to perform zero-downtime deployment in Kubernetes?**
Use rolling updates with readiness probes, keep previous ReplicaSet running until new pods are ready.

---

### ✅ **50. How do you monitor a Kubernetes cluster?**
- **Prometheus + Grafana**
- **ELK/EFK Stack**
- **Kube-state-metrics**
- **Jaeger/Zipkin for tracing**

---

Would you like a **PDF version**, or shall I continue with **advanced scenario-based Kubernetes questions**, or maybe dive into **Helm**, **K8s + DevOps**, or **K8s + AWS (EKS)** interview sets?