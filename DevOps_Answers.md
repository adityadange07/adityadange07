# DevOps Interview Questions & Answers (Deep Dive)

## 1. Kubernetes Architecture (Internals)
**Control Plane (Master Node):**
1.  **API Server:** The entry point (REST). Validates and processes JSON requests. The only component talking to Etcd.
2.  **Etcd:** Distributed Key-Value store. Source of truth (Cluster state, Config).
3.  **Scheduler:** Watches for new Pods (unassigned). Selects the best Worker Node based on resource availability (CPU/RAM) and taints/tolerations.
4.  **Controller Manager:** Reconciles state. Checks current state vs desired state (e.g., ReplicaSet Controller ensures 3 pods are running).

**Worker Node:**
1.  **Kubelet:** Agent running on node. Talks to API Server. Manages containers (via Docker/Containerd).
2.  **Kube Proxy:** Network proxy. Maintains network rules (IPTables/IPVS) to allow communication to Pods (Service Load Balancing).
3.  **Container Runtime:** Docker, Containerd, CRI-O.

## 2. Docker Internals (Layers & UnionFS)
**Image Layers:**
A Docker image is a stack of read-only layers (Union File System - Overlay2).
1.  Base Layer (Ubuntu).
2.  Add files (Add JDK).
3.  Add App (Add JAR).
**Container Layer:**
When you run a container, a thin **Read-Write layer** is added on top. Modifications happen here.
**Copy-On-Write:** If you modify a file existing in a lower read-only layer, Docker copies the file up to the RW layer first, then modifies it.
**Benefits:** Caching. If Layer 1 (OS) is downloaded, other images using same OS don't need to redownload it.

## 3. Pod Lifecycle & Probes
**Lifecycle:** Pending -> Running -> Succeeded/Failed.
**Probes (Health Checks):**
1.  **Liveness Probe:** "Am I alive?" If fails, Kubelet **Restarts** the container (Process deadlock fix).
2.  **Readiness Probe:** "Am I ready to take traffic?" If fails, Service **Removes** IP from Load Balancer. (Startup delay fix).
3.  **Startup Probe:** Runs once at start. Used for slow-starting legacy apps to delay Liveness probe.

## 4. CI/CD Pipeline Stages (Jenkins/GitLab) (Deep Dive)
**Zero Downtime Deployment Strategy:**
Instead of `stop app -> copy new jar -> start app` (Downtime):
- **Blue/Green:** Spin up new stack (Green). Run tests. Switch Load Balancer from Blue to Green. Kill Blue.
- **Rolling Update (K8s Default):** Replace pods one by one. `maxUnavailable=1` (take down 1), `maxSurge=1` (add 1).
- **Canary Analysis:** Deploy new version to 5% users. Check PromQL metrics (Error rate). If OK, roll out to 100%.

## 5. Docker Compose vs Kubernetes
- **Docker Compose:** Great for **Dev/Test** environment. Single host. Easy YAML. No auto-scaling, no self-healing across nodes.
- **Kubernetes:** **Production** Orchestrator. Multi-node. Auto-scaling (HPA), Self-healing (Restart on crash), Service Discovery built-in.

## 6. Maven Lifecycle Deep Dive
- **Scope:**
    - `compile`: Default. Available everywhere.
    - `provided`: Compile/Test only (e.g., Servlet API provided by Tomcat).
    - `test`: JUnit/Mockito.
    - `runtime`: JDBC Driver (Not needed for compilation, only running).
- **Dependency Resolution:** Nearest wins strategy. If A->B(v1) and A->C->B(v2), Maven parses tree to avoid conflicts.

## 7. Git Internals (Objects)
Git is a content-addressable filesystem.
- **Blob:** File content (Snapshot).
- **Tree:** Directory structure (Maps names to blobs).
- **Commit:** Points to a Tree + Author + Parent Commit.
- **Branch:** Just a pointer (ref) to a specific Commit Hash.
- **Merge (3-Way):** Uses Common Ancestor to merge Branch A and Branch B.
- **Rebase:** Rewrites history. "Lifts" commits from Branch A and "Replays" them on top of Branch B. Cleaner history, but dangerous on shared branches.
