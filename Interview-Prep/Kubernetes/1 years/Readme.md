Here's a curated list of the **Top 50 Kubernetes Interview Questions and Answers** for someone with **1 year of experience**. These questions focus on foundational concepts, basic Kubernetes objects, and practical knowledge expected from a beginner-to-intermediate DevOps engineer or developer.

---

## 🚀 **Top 50 Kubernetes Interview Questions (1 Year Experience)**

---

### ✅ **1. What is Kubernetes?**
Kubernetes (K8s) is an open-source container orchestration platform that automates deployment, scaling, and management of containerized applications.

---

### ✅ **2. What are the key components of Kubernetes architecture?**
- **Master Node**: API Server, Scheduler, Controller Manager, etcd
- **Worker Node**: Kubelet, Kube-proxy, Container runtime (Docker/CRI-O)

---

### ✅ **3. What is a Pod in Kubernetes?**
A Pod is the smallest and simplest unit in Kubernetes that can contain one or more containers.

---

### ✅ **4. What is a Node in Kubernetes?**
A node is a physical or virtual machine on which Kubernetes runs your workloads (pods).

---

### ✅ **5. What is the use of kubelet?**
`kubelet` runs on each node and ensures containers described in PodSpecs are running and healthy.

---

### ✅ **6. What is `etcd`?**
A distributed key-value store used by Kubernetes to store all cluster data (configuration, state).

---

### ✅ **7. What is a ReplicaSet?**
A ReplicaSet ensures a specified number of identical pods are running at all times.

---

### ✅ **8. What is a Deployment?**
A Deployment manages ReplicaSets and provides declarative updates to Pods and ReplicaSets.

---

### ✅ **9. What is a Service in Kubernetes?**
A Service is an abstraction that exposes a set of Pods as a network service.

---

### ✅ **10. Types of Services in Kubernetes?**
1. ClusterIP
2. NodePort
3. LoadBalancer
4. ExternalName

---

### ✅ **11. What is a Namespace in Kubernetes?**
A namespace is a logical partition to isolate resources within the same cluster.

---

### ✅ **12. What is the difference between a Deployment and StatefulSet?**
- **Deployment**: For stateless applications
- **StatefulSet**: For stateful applications, maintains identity and order

---

### ✅ **13. What is a ConfigMap?**
A ConfigMap allows you to store configuration data in key-value pairs.

---

### ✅ **14. What is a Secret in Kubernetes?**
A Secret is used to store sensitive information (like passwords, tokens, keys).

---

### ✅ **15. How do you expose a pod externally?**
Using a **Service** of type `NodePort` or `LoadBalancer`.

---

### ✅ **16. How to check all running Pods in a namespace?**
```bash
kubectl get pods -n <namespace>
```

---

### ✅ **17. What is the use of `kubectl`?**
`kubectl` is the command-line tool to interact with the Kubernetes cluster.

---

### ✅ **18. What is a DaemonSet?**
Ensures a copy of a Pod runs on **all** (or some) nodes in the cluster.

---

### ✅ **19. What is a Job in Kubernetes?**
A Job creates one or more pods to carry out a task and ensures that a specified number of them successfully terminate.

---

### ✅ **20. What is a CronJob?**
It runs jobs on a scheduled time (like cron in Linux).

---

### ✅ **21. How do you scale a Deployment?**
```bash
kubectl scale deployment <name> --replicas=5
```

---

### ✅ **22. What is a label in Kubernetes?**
Labels are key/value pairs attached to objects for identification and selection.

---

### ✅ **23. What are annotations in Kubernetes?**
Annotations store metadata that doesn't need to be used for selection (unlike labels).

---

### ✅ **24. What is a Taint and Toleration?**
- **Taint**: Prevents pods from being scheduled on a node
- **Toleration**: Allows the pod to be scheduled on a tainted node

---

### ✅ **25. What is a NodePort?**
Exposes the service on a static port on each node's IP.

---

### ✅ **26. What is a ClusterIP?**
Default type of Service, only accessible inside the cluster.

---

### ✅ **27. What is a LoadBalancer service?**
Exposes the service externally using a cloud provider’s load balancer.

---

### ✅ **28. What is port-forwarding in Kubernetes?**
Allows you to access a pod locally:
```bash
kubectl port-forward pod-name 8080:80
```

---

### ✅ **29. How do you check pod logs?**
```bash
kubectl logs <pod-name>
```

---

### ✅ **30. How to execute a command inside a running pod?**
```bash
kubectl exec -it <pod-name> -- /bin/bash
```

---

### ✅ **31. How do you create a new namespace?**
```bash
kubectl create namespace my-namespace
```

---

### ✅ **32. What is a volume in Kubernetes?**
Volumes are used to persist data across container restarts.

---

### ✅ **33. What is the difference between ephemeral and persistent storage in Kubernetes?**
- **Ephemeral**: Lost after container restarts
- **Persistent**: Maintains data across pod restarts using Persistent Volumes

---

### ✅ **34. What is a Persistent Volume (PV)?**
A piece of storage in the cluster provisioned by an admin or dynamically provisioned.

---

### ✅ **35. What is a Persistent Volume Claim (PVC)?**
A request for storage by a user that binds to a PV.

---

### ✅ **36. What are init containers?**
Special containers that run before app containers in a pod start.

---

### ✅ **37. How do you update a deployment without downtime?**
Use rolling updates (default behavior of Deployment):
```bash
kubectl apply -f deployment.yaml
```

---

### ✅ **38. What is rolling update strategy?**
Gradually updates pods with new version without downtime.

---

### ✅ **39. What is a Horizontal Pod Autoscaler (HPA)?**
It automatically scales the number of pods based on CPU/memory usage.

---

### ✅ **40. How do you rollback a deployment?**
```bash
kubectl rollout undo deployment <name>
```

---

### ✅ **41. How do you describe a resource in Kubernetes?**
```bash
kubectl describe <resource> <name>
```

---

### ✅ **42. What is the use of `kube-proxy`?**
Manages networking rules and enables communication to services.

---

### ✅ **43. What is `apiVersion` in a manifest file?**
Specifies the Kubernetes API version to use for a resource definition.

---

### ✅ **44. How do you delete a pod?**
```bash
kubectl delete pod <pod-name>
```

---

### ✅ **45. What are resource limits in Kubernetes?**
Constraints placed on CPU and memory for a container.

---

### ✅ **46. How do you troubleshoot a CrashLoopBackOff error?**
- View logs with `kubectl logs`
- Describe pod with `kubectl describe pod`
- Check for config or image issues

---

### ✅ **47. What are probes in Kubernetes?**
- **Liveness Probe**: Checks if the app is alive
- **Readiness Probe**: Checks if the app is ready to serve traffic

---

### ✅ **48. What is the difference between Pod and Container?**
- **Container**: Runs inside a Pod
- **Pod**: Wraps one or more containers

---

### ✅ **49. What is `kubeconfig`?**
A file that contains configuration for accessing a Kubernetes cluster.

---

### ✅ **50. What is Helm in Kubernetes?**
Helm is a package manager for Kubernetes that helps you define, install, and upgrade complex Kubernetes applications.

---

Would you like:
- These questions as a **PDF**?
- **Scenario-based questions** for real-world Kubernetes use cases?
- A complete guide with **Kubernetes + Docker + CI/CD pipeline** examples?

Let me know how you want to level up!