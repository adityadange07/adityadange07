Here are the **Top 50 Kubernetes Interview Questions and Answers** tailored for **4 years of experience**, focusing on practical, in-depth, and scenario-based concepts commonly asked in real-world DevOps or SRE interviews.

---

## 🚀 Top 50 Kubernetes Interview Questions (For 4 Years Experience)

---

### ✅ **1. What is Kubernetes?**
Kubernetes (K8s) is an open-source container orchestration platform for automating deployment, scaling, and management of containerized applications.

---

### ✅ **2. What are the main components of Kubernetes architecture?**
- **Master Node** (Control Plane):
    - kube-apiserver
    - etcd
    - kube-scheduler
    - kube-controller-manager
- **Worker Node**:
    - kubelet
    - kube-proxy
    - Container Runtime (e.g., Docker, containerd)

---

### ✅ **3. What is a Pod?**
A Pod is the smallest deployable unit in Kubernetes. It encapsulates one or more containers with shared storage/network.

---

### ✅ **4. What is the difference between Pod and Container?**
- **Pod** is a wrapper around containers.
- One Pod can run multiple tightly coupled containers.

---

### ✅ **5. What is a ReplicaSet?**
A ReplicaSet ensures that a specified number of pod replicas are running at any given time.

---

### ✅ **6. What is a Deployment in Kubernetes?**
A Deployment manages ReplicaSets and provides declarative updates to Pods (rolling updates, rollbacks, etc.).

---

### ✅ **7. How do Services work in Kubernetes?**
A **Service** exposes Pods using a stable endpoint (ClusterIP, NodePort, LoadBalancer) and load balances traffic.

---

### ✅ **8. What is the role of kube-apiserver?**
It acts as the frontend to the control plane, validating and processing API requests.

---

### ✅ **9. What is etcd in Kubernetes?**
etcd is a distributed key-value store that holds all cluster state data.

---

### ✅ **10. What is the role of kubelet?**
kubelet runs on each node and ensures that containers are running in the desired state.

---

### ✅ **11. What is kube-proxy?**
It manages network communication and implements service load balancing using iptables or IPVS.

---

### ✅ **12. What is a Namespace in Kubernetes?**
Namespaces are used to logically divide cluster resources between users and teams.

---

### ✅ **13. What is the difference between ConfigMap and Secret?**
- **ConfigMap**: Stores non-sensitive configuration.
- **Secret**: Stores sensitive data (base64 encoded).

---

### ✅ **14. How to perform a rolling update in Kubernetes?**
Using Deployments:
```bash
kubectl set image deployment/myapp myapp=myimage:v2
```

---

### ✅ **15. How to rollback a deployment?**
```bash
kubectl rollout undo deployment myapp
```

---

### ✅ **16. What is a StatefulSet?**
StatefulSet is used for stateful applications and provides stable network identity and persistent storage.

---

### ✅ **17. Difference between Deployment and StatefulSet?**
| Feature | Deployment | StatefulSet |
|--------|-------------|-------------|
| Pod Names | Random | Stable |
| Storage | Shared | Persistent |
| Use Case | Stateless | Stateful |

---

### ✅ **18. What is a DaemonSet?**
A DaemonSet ensures a Pod runs on every node (e.g., log shippers, monitoring agents).

---

### ✅ **19. What are Init Containers?**
Special containers that run before app containers to perform setup tasks.

---

### ✅ **20. How does Kubernetes handle persistent storage?**
Via **Persistent Volumes (PV)** and **Persistent Volume Claims (PVC)**.

---

### ✅ **21. What are PV and PVC in Kubernetes?**
- **PV**: Abstraction over physical storage.
- **PVC**: Request for storage by a user.

---

### ✅ **22. What is a ServiceAccount?**
A ServiceAccount provides an identity for Pods to interact with the Kubernetes API.

---

### ✅ **23. What is RBAC in Kubernetes?**
Role-Based Access Control defines permissions (verbs) for users and service accounts on resources.

---

### ✅ **24. What is a NodePort service?**
Exposes a Pod on a static port on each node’s IP (range: 30000–32767).

---

### ✅ **25. What is a LoadBalancer service?**
Exposes Pods externally using a cloud provider’s load balancer.

---

### ✅ **26. How do you troubleshoot a Pod that is CrashLoopBackOff?**
- `kubectl describe pod <name>`
- `kubectl logs <name>`
- Check init containers, liveness/readiness probes, config errors

---

### ✅ **27. What is a Liveness Probe?**
Checks if the app inside a container is alive. If it fails, the container is restarted.

---

### ✅ **28. What is a Readiness Probe?**
Checks if a container is ready to receive traffic. Pod is removed from service endpoints if it fails.

---

### ✅ **29. How does Kubernetes handle scaling?**
- **Horizontal**: HPA (Horizontal Pod Autoscaler)
- **Vertical**: VPA (Vertical Pod Autoscaler)

---

### ✅ **30. What is HPA (Horizontal Pod Autoscaler)?**
Automatically scales the number of Pods based on CPU/memory or custom metrics.

---

### ✅ **31. What is Taint and Toleration?**
- **Taints**: Mark a node to repel pods.
- **Tolerations**: Allow pods to be scheduled on tainted nodes.

---

### ✅ **32. How to list all Pods in all namespaces?**
```bash
kubectl get pods --all-namespaces
```

---

### ✅ **33. What is an Ingress?**
Ingress manages external access to services, typically HTTP/S, with routing rules.

---

### ✅ **34. What is an Ingress Controller?**
A controller that implements the Ingress resource (e.g., NGINX, Traefik).

---

### ✅ **35. What is a Custom Resource Definition (CRD)?**
CRDs allow users to define their own API resources and controllers in Kubernetes.

---

### ✅ **36. What is a Helm chart?**
Helm is a package manager for Kubernetes. Charts are pre-configured Kubernetes resources.

---

### ✅ **37. How does Kubernetes perform service discovery?**
Using DNS (CoreDNS) where services are reachable via `svc-name.namespace.svc.cluster.local`.

---

### ✅ **38. What are the different kubeconfig contexts?**
Contexts in kubeconfig file define which cluster, user, and namespace to use.

---

### ✅ **39. What is a sidecar container?**
A helper container that runs alongside the main app container (e.g., for logging, proxying).

---

### ✅ **40. What is node affinity?**
Rules to influence pod scheduling to specific nodes based on labels.

---

### ✅ **41. What is the difference between soft and hard affinity/anti-affinity?**
- **Soft**: Preferred during scheduling.
- **Hard**: Required (mandatory).

---

### ✅ **42. What is a pod disruption budget (PDB)?**
Defines the minimum number of Pods that must remain available during voluntary disruptions.

---

### ✅ **43. What is the role of admission controllers?**
Intercept API requests and modify or reject them based on policies (e.g., ValidatingWebhook, MutatingWebhook).

---

### ✅ **44. How do you upgrade a Kubernetes cluster?**
Depends on environment (kubeadm, cloud provider, etc.). Backup `etcd`, upgrade control plane nodes, then worker nodes.

---

### ✅ **45. What are Finalizers in Kubernetes?**
Finalizers prevent deletion of resources until specific clean-up operations are completed.

---

### ✅ **46. How do you debug a Kubernetes network issue?**
- Check `kubectl get svc`, endpoints
- Use `kubectl exec` to ping
- Check CNI logs and iptables rules

---

### ✅ **47. What is the use of `kubectl port-forward`?**
Forwards a local port to a pod/service port without exposing it externally:
```bash
kubectl port-forward svc/myservice 8080:80
```

---

### ✅ **48. What is a Job in Kubernetes?**
Job runs a Pod until successful completion (useful for batch processing).

---

### ✅ **49. What is a CronJob?**
Runs Jobs on a defined schedule, like a UNIX cron.

---

### ✅ **50. How do you handle secret management in Kubernetes?**
- Use `Secret` objects (base64-encoded)
- Mount as volume or env variable
- Integrate with external tools (Vault, AWS Secrets Manager)

---

If you'd like:
- 📄 PDF version of these questions
- 💡 Scenario-based Kubernetes Q&A
- 🔁 Mock interview with feedback
- 📦 Helm, CI/CD, or GitOps-focused questions

Let me know what to generate next!