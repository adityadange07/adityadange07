Here are the **Top 50 Docker Interview Questions and Answers** tailored for someone with **5 years of experience**. These questions go beyond the basics and focus more on real-world Docker use, advanced Docker concepts, DevOps integration, optimization, orchestration, security, and troubleshooting.

---

## 🚀 **Top 50 Docker Interview Questions (5 Years Experience)**

---

### ✅ **1. Explain Docker architecture in detail.**
Docker uses a client-server architecture:
- **Docker Client**: CLI for interacting with Docker.
- **Docker Daemon** (`dockerd`): Manages Docker objects (containers, images, etc.).
- **Docker Images**: Read-only templates.
- **Docker Containers**: Running instances of images.
- **Docker Registry**: Stores images (e.g., Docker Hub).

---

### ✅ **2. What’s the lifecycle of a Docker container?**
1. Create
2. Run
3. Pause/Unpause
4. Stop
5. Kill
6. Remove

---

### ✅ **3. What are the different types of Docker networks?**
1. **Bridge** (default)
2. **Host**
3. **Overlay**
4. **None**
5. **Macvlan**

---

### ✅ **4. How does Docker handle networking in multi-host scenarios?**
Using **overlay networks** in **Docker Swarm** or with **Docker Enterprise** / Kubernetes CNI plugins.

---

### ✅ **5. How do you secure Docker containers in production?**
- Use minimal base images
- Drop root privileges (use non-root user)
- Use read-only filesystem
- Apply Docker security profiles (AppArmor, SELinux)
- Use secrets management
- Regular vulnerability scanning

---

### ✅ **6. Explain Docker image layering.**
Images are built in layers (each instruction in the Dockerfile creates a new layer). Layers are cached and shared among containers to optimize build and storage.

---

### ✅ **7. What is the difference between `ENTRYPOINT` and `CMD`?**
- **ENTRYPOINT**: Always runs (primary command)
- **CMD**: Provides default arguments for ENTRYPOINT

---

### ✅ **8. What are multi-stage builds in Docker and when should you use them?**
Multi-stage builds allow you to have multiple `FROM` statements in one Dockerfile, enabling separation of build-time and runtime environments, reducing image size.

---

### ✅ **9. How do you handle configuration management inside Docker containers?**
- Use environment variables
- Config files via mounted volumes
- Use secrets/config in Docker Swarm or Kubernetes
- Use `.env` with `docker-compose`

---

### ✅ **10. What’s the best way to persist logs from a container?**
- Use logging drivers (json-file, fluentd, awslogs)
- Forward to ELK/EFK stack
- Mount host directory to store logs
- Use log shippers like Fluent Bit or Filebeat

---

### ✅ **11. What are Docker volumes vs bind mounts?**
- **Volumes**: Managed by Docker, stored in `/var/lib/docker/volumes`
- **Bind mounts**: Mount host directory into container (can be less secure)

---

### ✅ **12. How to manage secret data in Docker?**
- In Docker Swarm: `docker secret`
- Use Docker secrets API
- External tools: HashiCorp Vault, AWS Secrets Manager

---

### ✅ **13. How to minimize Docker image size?**
- Use Alpine Linux base image
- Remove unnecessary build artifacts
- Use `.dockerignore`
- Multi-stage builds

---

### ✅ **14. What is a dangling image in Docker?**
Images not tagged and not referenced by any container.

---

### ✅ **15. How to remove dangling images and stopped containers?**
```bash
docker system prune
```

---

### ✅ **16. What is Docker Swarm and its architecture?**
Swarm is Docker's native clustering. Architecture includes:
- **Manager Nodes**
- **Worker Nodes**
- **Services**
- **Tasks**

---

### ✅ **17. Compare Docker Swarm and Kubernetes.**
| Feature | Docker Swarm | Kubernetes |
|--------|---------------|------------|
| Setup | Easier | Complex |
| Scalability | Limited | Very high |
| Features | Basic | Advanced |
| Ecosystem | Small | Huge |

---

### ✅ **18. How do you update a running container without downtime?**
- Blue-green deployment
- Canary deployment
- Use Docker Compose or Swarm rolling updates

---

### ✅ **19. What’s the use of `HEALTHCHECK` in Dockerfile?**
It defines a command to monitor the container’s health.

---

### ✅ **20. How does Docker handle memory and CPU limits?**
Use flags like:
```bash
--memory="256m" --cpus="1.5"
```

---

### ✅ **21. Explain how `docker-compose` works.**
Defines multi-container apps with a YAML file (`docker-compose.yml`), manages networking, volume sharing, and service dependencies.

---

### ✅ **22. What’s the difference between `docker run` and `docker start`?**
- `docker run`: Creates and starts a new container
- `docker start`: Starts an existing stopped container

---

### ✅ **23. What is a container orchestration tool?**
It automates deployment, scaling, networking, and management of containers (e.g., Kubernetes, Docker Swarm, ECS).

---

### ✅ **24. How to build and push a Docker image to a private registry?**
```bash
docker build -t myregistry.com/myapp:1.0 .  
docker push myregistry.com/myapp:1.0
```

---

### ✅ **25. What is the purpose of `.dockerignore`?**
It excludes files and directories during the image build process, similar to `.gitignore`.

---

### ✅ **26. What’s the difference between `EXPOSE` and `-p`?**
- `EXPOSE`: Documents ports (no actual binding)
- `-p`: Binds container port to host port

---

### ✅ **27. What happens when a container exits?**
The container moves to "Exited" state unless `--restart` policy is used.

---

### ✅ **28. How to troubleshoot a failed container?**
- Use `docker logs`
- Run with `--entrypoint /bin/sh`
- Use `docker inspect`
- Check image and startup scripts

---

### ✅ **29. What is the `overlay` network in Docker?**
Used in Swarm to enable containers on different hosts to communicate.

---

### ✅ **30. How does Docker handle DNS resolution?**
By default, Docker uses an embedded DNS server for container name resolution.

---

### ✅ **31. What’s the use of labels in Docker?**
Attach metadata to images/containers:
```bash
LABEL version="1.0" maintainer="aditya@example.com"
```

---

### ✅ **32. What are Docker logging drivers?**
Mechanisms to send logs to different systems: `json-file`, `syslog`, `fluentd`, `awslogs`, etc.

---

### ✅ **33. Explain copy-on-write (CoW) in Docker.**
Containers share image layers and only write changes in their own writable layer, using CoW to avoid duplicating data.

---

### ✅ **34. How to rollback a failed deployment in Docker Swarm?**
Swarm tracks previous service versions and can rollback automatically or manually using:
```bash
docker service update --rollback <service>
```

---

### ✅ **35. What is the purpose of `--privileged` mode?**
Gives a container extended Linux capabilities. Should be avoided unless necessary.

---

### ✅ **36. Can a Docker container access the host network?**
Yes, using `--network host`, but it removes network isolation.

---

### ✅ **37. How to monitor Docker containers?**
- Docker stats
- Prometheus + cAdvisor
- ELK stack
- Grafana dashboards

---

### ✅ **38. What is container drift?**
When a containerized environment diverges from the original image definition. Use CI/CD pipelines to avoid it.

---

### ✅ **39. How to ensure image immutability?**
- Tag with immutable hashes (e.g., SHA256)
- Use read-only containers
- Avoid `latest` tag

---

### ✅ **40. How to scan Docker images for vulnerabilities?**
- Docker Scout
- Trivy
- Clair
- Snyk

---

### ✅ **41. How do you implement CI/CD with Docker?**
- Build Docker images in CI
- Push to registry
- Deploy using Compose, Swarm, or Kubernetes

---

### ✅ **42. What’s the difference between `restart=always` and `restart=unless-stopped`?**
- `always`: Restarts always, even after manual stop
- `unless-stopped`: Doesn’t restart after manual stop

---

### ✅ **43. What’s the role of an init system like `tini` in Docker?**
Handles zombie processes and proper signal forwarding in containers.

---

### ✅ **44. How can you check container performance?**
```bash
docker stats
```

---

### ✅ **45. What are the downsides of using Docker in production?**
- Security risks if not managed properly
- Complexity with orchestration
- Learning curve

---

### ✅ **46. What’s the purpose of `docker inspect`?**
Shows detailed low-level info about containers, images, volumes, etc.

---

### ✅ **47. How do you backup and restore Docker volumes?**
Backup:
```bash
docker run --rm -v myvol:/volume -v $(pwd):/backup alpine tar czf /backup/backup.tar.gz -C /volume .
```
Restore:
```bash
docker run --rm -v myvol:/volume -v $(pwd):/backup alpine tar xzf /backup/backup.tar.gz -C /volume
```

---

### ✅ **48. What’s the impact of using `:latest` tag in images?**
- Risk of unpredictability in deployments
- No version locking
- Better to use specific version tags

---

### ✅ **49. How do you share images in a team environment securely?**
- Use private Docker registry
- Authenticate access
- Use role-based access control (RBAC)

---

### ✅ **50. What is the OCI standard?**
Open Container Initiative defines standards for container image and runtime specifications to ensure interoperability.

---

Would you like these questions as a PDF or want me to move to **Kubernetes**, **CI/CD with Docker**, or **Docker + DevOps scenario-based** questions next?