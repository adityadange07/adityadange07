Here are the **Top 50 Kubernetes Interview Questions and Answers** designed for someone with **2 years of experience**. These questions are a mix of foundational concepts and practical usage—ideal for developers or DevOps engineers working with Kubernetes in day-to-day environments.

---

## 🚀 Top 50 Kubernetes Interview Questions (2 Years Experience)

---

### ✅ **1. What is Kubernetes?**
Kubernetes is an open-source container orchestration platform used to automate deployment, scaling, and management of containerized applications.

---

### ✅ **2. What are the main components of Kubernetes architecture?**
- Master Node (Control Plane)
    - API Server
    - Scheduler
    - Controller Manager
    - etcd
- Worker Nodes
    - kubelet
    - kube-proxy
    - Container runtime (Docker, containerd)

---

### ✅ **3. What is a Pod in Kubernetes?**
A Pod is the smallest and simplest unit in Kubernetes. It encapsulates one or more containers that share the same network and storage.

---

### ✅ **4. What is the role of kubelet?**
Kubelet runs on each worker node and ensures that containers are running in a Pod.

---

### ✅ **5. What is a Deployment in Kubernetes?**
Deployment is a controller that manages replica sets and allows declarative updates to Pods.

---

### ✅ **6. How do you expose a Pod to external traffic?**
Use a **Service** of type `NodePort`, `LoadBalancer`, or `Ingress`.

---

### ✅ **7. What is a ReplicaSet?**
ReplicaSet ensures a specified number of Pod replicas are running at all times.

---

### ✅ **8. Difference between Deployment and StatefulSet?**
- **Deployment**: For stateless apps.
- **StatefulSet**: For stateful apps, provides stable network ID and storage.

---

### ✅ **9. What is etcd?**
etcd is a consistent and highly available key-value store used as Kubernetes' backing store for all cluster data.

---

### ✅ **10. What is a Service in Kubernetes?**
A Service is an abstraction that defines a logical set of Pods and a policy by which to access them.

---

### ✅ **11. Types of Kubernetes Services?**
- ClusterIP (default)
- NodePort
- LoadBalancer
- ExternalName

---

### ✅ **12. What is a Namespace?**
Namespaces provide a way to divide cluster resources between multiple users (multi-tenancy).

---

### ✅ **13. How do you scale Pods in Kubernetes?**
```bash
kubectl scale deployment <name> --replicas=<number>
```

---

### ✅ **14. What is a ConfigMap?**
ConfigMap is used to inject configuration data into Pods as environment variables or volume files.

---

### ✅ **15. What is a Secret in Kubernetes?**
Secret is used to store sensitive information like passwords, tokens, or keys.

---

### ✅ **16. What is the role of Scheduler in Kubernetes?**
It assigns Pods to available nodes based on resource requirements and constraints.

---

### ✅ **17. What is the difference between `kubectl apply` and `kubectl create`?**
- `create`: Creates resources from scratch.
- `apply`: Creates or updates resources declaratively.

---

### ✅ **18. How to perform a rolling update in Kubernetes?**
```bash
kubectl rollout restart deployment <name>
```

---

### ✅ **19. How to rollback a Deployment?**
```bash
kubectl rollout undo deployment <name>
```

---

### ✅ **20. What is a DaemonSet?**
Ensures that a Pod runs on all (or some) nodes. Common for log collectors or monitoring agents.

---

### ✅ **21. What is a Job in Kubernetes?**
A Job creates one or more Pods and ensures they run to completion.

---

### ✅ **22. What is a CronJob?**
A CronJob is used to run Jobs on a time-based schedule (like cron).

---

### ✅ **23. What is Ingress in Kubernetes?**
Ingress is an API object that manages external access to services, usually HTTP.

---

### ✅ **24. What is a Node in Kubernetes?**
A Node is a physical or virtual machine on which Kubernetes runs and hosts Pods.

---

### ✅ **25. How does Kubernetes handle high availability?**
- Multiple master nodes (HA setup)
- ReplicaSets for Pods
- Services with load balancing

---

### ✅ **26. What is `kubectl`?**
`kubectl` is the command-line tool to interact with the Kubernetes API.

---

### ✅ **27. How to get logs from a Pod?**
```bash
kubectl logs <pod-name>
```

---

### ✅ **28. How to access a Pod's shell?**
```bash
kubectl exec -it <pod-name> -- /bin/bash
```

---

### ✅ **29. What is Taint and Toleration?**
- **Taints**: Prevent Pods from scheduling on a node.
- **Tolerations**: Allow Pods to be scheduled on tainted nodes.

---

### ✅ **30. What is Node Affinity?**
Used to constrain which nodes your Pod is eligible to be scheduled on based on labels.

---

### ✅ **31. What is Horizontal Pod Autoscaler (HPA)?**
HPA automatically scales Pods based on CPU/memory usage or custom metrics.

---

### ✅ **32. What are Labels and Selectors?**
- **Labels**: Key-value pairs attached to objects.
- **Selectors**: Used to filter resources by labels.

---

### ✅ **33. How to update a running container image?**
```bash
kubectl set image deployment <name> <container>=<image>
```

---

### ✅ **34. How to delete all resources in a namespace?**
```bash
kubectl delete all --all -n <namespace>
```

---

### ✅ **35. What is `kube-proxy`?**
It maintains network rules and enables communication to/from Pods.

---

### ✅ **36. How do you monitor a Kubernetes cluster?**
- Prometheus + Grafana
- Kubernetes Metrics Server
- kubectl top nodes/pods

---

### ✅ **37. How does Kubernetes handle persistent storage?**
Via **PersistentVolumes (PV)** and **PersistentVolumeClaims (PVC)**.

---

### ✅ **38. What is a Volume in Kubernetes?**
Volumes are used to store data that outlives the Pod's container lifecycle.

---

### ✅ **39. How do you connect external storage to Kubernetes?**
Use StorageClasses with dynamic provisioning (e.g., AWS EBS, GCE PD).

---

### ✅ **40. How does service discovery work in Kubernetes?**
Kube-DNS/CoreDNS resolves service names to cluster IPs.

---

### ✅ **41. What is a Stateful Application in Kubernetes?**
Apps that require stable network IDs, persistent storage (e.g., databases) use StatefulSets.

---

### ✅ **42. What is the difference between Ephemeral and Persistent storage?**
- **Ephemeral**: Data is lost when the container stops.
- **Persistent**: Data is retained via PVs and PVCs.

---

### ✅ **43. What are Init Containers?**
Special containers that run before the main container starts; used for setup tasks.

---

### ✅ **44. What is an Admission Controller?**
Intercepts requests to the Kubernetes API server before persistence and execution.

---

### ✅ **45. What are Resource Quotas and Limits?**
They restrict the amount of CPU and memory resources a namespace or container can consume.

---

### ✅ **46. What are the common issues in Pods not starting?**
- ImagePull errors
- Insufficient resources
- Config errors
- Taints and tolerations mismatched

---

### ✅ **47. How does Kubernetes perform load balancing?**
Via Services (ClusterIP/NodePort) using round-robin across available Pods.

---

### ✅ **48. What is a ServiceAccount in Kubernetes?**
Used by Pods to authenticate with the Kubernetes API.

---

### ✅ **49. How to run Kubernetes locally?**
Using tools like:
- Minikube
- Kind (Kubernetes in Docker)
- k3s

---

### ✅ **50. What is the difference between Docker Swarm and Kubernetes?**
| Feature | Docker Swarm | Kubernetes |
|--------|---------------|------------|
| Setup | Simpler | Complex |
| Features | Basic | Rich |
| Scaling | Manual | Auto |
| Ecosystem | Smaller | Large community |

---

Let me know if you want:
- A **PDF version** of these 50 questions
- **Mock interview set** combining **Kubernetes + Docker + CI/CD**
- 30 **scenario-based Kubernetes questions** for real-world experience
- Kubernetes questions for **5+ years experience or architect roles**

Just say the word!