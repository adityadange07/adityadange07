Here are the **Top 50 Kubernetes Interview Questions and Answers** tailored for **3 years of experience**. These questions focus on both foundational and practical Kubernetes knowledge you'll need in real-world projects and DevOps interviews.

---

## 🚀 **Top 50 Kubernetes Interview Questions (3 Years Experience)**

---

### ✅ **1. What is Kubernetes?**
Kubernetes is an open-source container orchestration platform for automating deployment, scaling, and management of containerized applications.

---

### ✅ **2. What are the main components of Kubernetes architecture?**
1. **Master Node (Control Plane)**: API Server, Scheduler, Controller Manager, etcd
2. **Worker Node**: Kubelet, Kube-proxy, Container Runtime

---

### ✅ **3. What is a Pod in Kubernetes?**
A Pod is the smallest deployable unit in Kubernetes. It can contain one or more containers that share storage, network, and specs.

---

### ✅ **4. What is a Node in Kubernetes?**
A node is a physical or virtual machine on which Kubernetes runs your workloads (Pods).

---

### ✅ **5. What is the role of etcd?**
`etcd` is a distributed key-value store that stores all cluster data.

---

### ✅ **6. What is a ReplicaSet?**
A ReplicaSet ensures that a specified number of Pod replicas are running at any given time.

---

### ✅ **7. What is a Deployment in Kubernetes?**
Deployment provides declarative updates to Pods and ReplicaSets. It supports rolling updates and rollbacks.

---

### ✅ **8. What is a Namespace?**
A Namespace is a virtual cluster within a Kubernetes cluster. It helps separate and organize resources.

---

### ✅ **9. What is a Service in Kubernetes?**
A Service exposes a set of Pods as a network service (ClusterIP, NodePort, LoadBalancer, etc.).

---

### ✅ **10. What is the difference between NodePort and LoadBalancer service types?**
- **NodePort**: Exposes service on a static port on each node
- **LoadBalancer**: Integrates with cloud provider’s load balancer (external access)

---

### ✅ **11. What is Kubelet?**
Kubelet is an agent that runs on each node and ensures containers are running in a Pod.

---

### ✅ **12. What is Kube-proxy?**
It maintains network rules on nodes to allow communication to/from Pods.

---

### ✅ **13. What is a ConfigMap?**
Used to inject configuration data into Pods via environment variables or volumes.

---

### ✅ **14. What is a Secret in Kubernetes?**
A Secret is an object that stores sensitive information like passwords, tokens, and keys.

---

### ✅ **15. What is the use of Liveness and Readiness probes?**
- **Liveness Probe**: Checks if app is alive
- **Readiness Probe**: Checks if app is ready to serve traffic

---

### ✅ **16. What is the default scheduling algorithm in Kubernetes?**
It schedules Pods based on resource requests, node selectors, affinity/anti-affinity, taints/tolerations, etc.

---

### ✅ **17. What is a StatefulSet?**
Manages the deployment and scaling of stateful applications (e.g., databases). It gives each Pod a unique identity.

---

### ✅ **18. What is a DaemonSet?**
Ensures a Pod runs on all (or selected) nodes.

---

### ✅ **19. What is a Job in Kubernetes?**
A Job creates one or more Pods and ensures that a specified number of them successfully terminate.

---

### ✅ **20. What is a CronJob?**
Schedules jobs to run periodically on a given schedule.

---

### ✅ **21. How do you perform a rolling update in Kubernetes?**
Using `kubectl rollout` commands or updating Deployment configuration:
```bash
kubectl rollout restart deployment <deployment-name>
```

---

### ✅ **22. How do you rollback a deployment?**
```bash
kubectl rollout undo deployment <deployment-name>
```

---

### ✅ **23. What is a ServiceAccount in Kubernetes?**
An account used by Pods to communicate with the Kubernetes API.

---

### ✅ **24. What are Taints and Tolerations?**
- **Taints**: Mark a node to repel Pods
- **Tolerations**: Allow Pods to be scheduled on tainted nodes

---

### ✅ **25. What is node affinity?**
A rule to schedule Pods based on node labels (preferred or required).

---

### ✅ **26. What is the difference between horizontal and vertical Pod autoscaling?**
- **Horizontal**: Scales number of Pod replicas
- **Vertical**: Changes resource requests/limits of Pods

---

### ✅ **27. What is HPA (Horizontal Pod Autoscaler)?**
Automatically scales the number of Pods based on metrics like CPU or custom metrics.

---

### ✅ **28. How to expose a deployment externally?**
By using:
- `kubectl expose`
- Service of type NodePort or LoadBalancer
- Ingress controller

---

### ✅ **29. What is Ingress in Kubernetes?**
Ingress exposes HTTP/HTTPS routes from outside the cluster to services within the cluster.

---

### ✅ **30. What is the use of annotations and labels?**
- **Labels**: Used for grouping and selecting objects
- **Annotations**: Used for storing metadata

---

### ✅ **31. How do you debug a Pod?**
- `kubectl logs <pod>`
- `kubectl exec -it <pod> -- /bin/sh`
- `kubectl describe pod <pod>`

---

### ✅ **32. What is Helm in Kubernetes?**
Helm is a package manager for Kubernetes. Helm Charts are used to define, install, and upgrade complex Kubernetes applications.

---

### ✅ **33. What is a Helm chart?**
A Helm chart is a collection of YAML templates for Kubernetes resources.

---

### ✅ **34. What is a PersistentVolume (PV) and PersistentVolumeClaim (PVC)?**
- **PV**: Provisioned storage in the cluster
- **PVC**: Request for storage by a user

---

### ✅ **35. What are the storage classes in Kubernetes?**
Defines how storage is dynamically provisioned (e.g., `standard`, `fast`, `ssd`).

---

### ✅ **36. How do you perform a health check on Pods?**
By defining:
- `livenessProbe`
- `readinessProbe`
- `startupProbe` (K8s 1.16+)

---

### ✅ **37. How to restrict access to Kubernetes resources?**
Use **RBAC** (Role-Based Access Control):
- Role / ClusterRole
- RoleBinding / ClusterRoleBinding

---

### ✅ **38. How to scale a deployment manually?**
```bash
kubectl scale deployment <name> --replicas=5
```

---

### ✅ **39. How does Kubernetes handle self-healing?**
- Restarts failed containers
- Replaces and reschedules Pods on dead nodes
- Kills unresponsive Pods

---

### ✅ **40. How does Kubernetes manage secrets securely?**
Secrets are base64-encoded and stored in etcd. Best practices:
- Use RBAC
- Use external secret managers (Vault, AWS Secrets Manager)

---

### ✅ **41. What is kubeconfig?**
A configuration file used to access Kubernetes clusters via `kubectl`.

---

### ✅ **42. How do you view cluster resource usage?**
```bash
kubectl top nodes  
kubectl top pods
```
(Requires metrics-server)

---

### ✅ **43. What is the difference between soft and hard limits in resource requests?**
- **Request**: Minimum guaranteed resources
- **Limit**: Maximum allowed usage

---

### ✅ **44. How do you clean up unused resources in Kubernetes?**
Use:
```bash
kubectl delete <resource> <name>
```
Or use `--prune`, label selectors, or scripts.

---

### ✅ **45. How to view all services in a namespace?**
```bash
kubectl get svc -n <namespace>
```

---

### ✅ **46. What happens when a node goes down in Kubernetes?**
- The node is marked "NotReady"
- Pods are rescheduled on other nodes (if replicas exist)

---

### ✅ **47. How do you implement blue-green deployment in Kubernetes?**
- Use two deployments (v1 and v2)
- Switch service from v1 to v2 manually or via Ingress

---

### ✅ **48. What is a sidecar container?**
A container that runs alongside the main container in a Pod to provide supporting functionality (e.g., logging, proxy).

---

### ✅ **49. How do you install Kubernetes locally?**
Using tools like:
- Minikube
- Kind (Kubernetes in Docker)
- k3s (lightweight)

---

### ✅ **50. How do you monitor Kubernetes clusters?**
- Prometheus + Grafana
- Metrics-server
- EFK/ELK Stack
- Kubernetes Dashboard

---

Let me know if you’d like:
- A **PDF** version
- Top **50 Kubernetes advanced** questions
- Questions focused on **K8s + Docker + DevOps**
- Scenario-based questions for real-world **Kubernetes projects**

Also happy to help with Helm, CI/CD, AWS with K8s (EKS), and more!