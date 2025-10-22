Here are the **Top 50 Docker Interview Questions and Answers tailored for 4 years of experience**. These questions go beyond the basics and cover **real-world, intermediate-to-advanced topics**, including performance, security, orchestration, networking, and optimization.

---

### ✅ **1. What is Docker and how does it differ from a VM?**
Docker uses containerization to isolate applications with shared OS resources, unlike VMs which run full OS instances using hypervisors.

---

### ✅ **2. How does Docker ensure isolation between containers?**
Docker uses Linux kernel features like **cgroups** and **namespaces** for process, network, and file system isolation.

---

### ✅ **3. Explain Docker architecture.**
- **Docker Client**
- **Docker Daemon**
- **Docker Images**
- **Docker Containers**
- **Docker Registry**

---

### ✅ **4. How is a Docker container different from an image?**
- **Image**: Read-only template
- **Container**: Live, running instance of an image

---

### ✅ **5. What are namespaces in Docker?**
They isolate containers in terms of PID, NET, IPC, MNT, and UTS.

---

### ✅ **6. What is the role of cgroups in Docker?**
Control Groups (cgroups) manage and limit resource usage (CPU, memory, disk I/O) of containers.

---

### ✅ **7. What happens when you run `docker run` command?**
1. Docker daemon pulls the image
2. Creates a container from image
3. Allocates filesystem and network
4. Executes the entrypoint or command

---

### ✅ **8. How do multi-stage builds help in Docker?**
They help in creating **leaner, optimized** images by separating build dependencies from runtime.

---

### ✅ **9. What is the difference between `ENTRYPOINT` and `CMD`?**
- `CMD`: Default args
- `ENTRYPOINT`: Command that always runs

---

### ✅ **10. What is a Docker Volume?**
Persistent storage outside of the container's writable layer, managed by Docker.

---

### ✅ **11. Difference between Volumes and Bind Mounts?**
- **Volumes**: Managed by Docker
- **Bind Mounts**: Link host directory directly

---

### ✅ **12. How to pass environment variables into Docker containers?**
```bash
docker run -e VAR=value myimage
```

---

### ✅ **13. How do you secure Docker containers?**
- Use non-root users
- Minimize image size
- Use image signing
- Enable SELinux/AppArmor
- Network and secrets management

---

### ✅ **14. What is Docker Content Trust (DCT)?**
It ensures the integrity and publisher of Docker images using **digital signatures**.

---

### ✅ **15. What is the purpose of `.dockerignore`?**
To prevent unnecessary files from being copied into the image, optimizing build time.

---

### ✅ **16. How do you reduce Docker image size?**
- Use Alpine Linux
- Clean up apt/yum caches
- Combine RUN commands
- Use multi-stage builds

---

### ✅ **17. Explain image layers in Docker.**
Each instruction in Dockerfile creates a layer. Docker uses layer caching to speed up builds.

---

### ✅ **18. What is the purpose of `WORKDIR` in Dockerfile?**
Sets the working directory for following instructions and container run time.

---

### ✅ **19. What is the difference between `COPY` and `ADD` in Dockerfile?**
- **COPY**: Simpler, preferred
- **ADD**: Supports remote URLs and extracting archives

---

### ✅ **20. How do you debug a Docker container that exits immediately?**
```bash
docker run -it --entrypoint /bin/sh myimage
```

---

### ✅ **21. How do you manage container logs?**
- Use `docker logs`
- Configure logging drivers: `json-file`, `syslog`, `fluentd`, `awslogs`, etc.

---

### ✅ **22. How do you connect multiple containers?**
Use a **custom user-defined bridge network** for easy name resolution and communication.

---

### ✅ **23. What are the types of Docker networks?**
- Bridge
- Host
- None
- Overlay (for Swarm)
- Macvlan

---

### ✅ **24. What is Docker Compose and why is it used?**
Tool for defining multi-container applications using YAML (`docker-compose.yml`).

---

### ✅ **25. How to scale services using Docker Compose?**
```bash
docker-compose up --scale web=3
```

---

### ✅ **26. What is a health check in Docker?**
Used to monitor container health via Dockerfile:
```Dockerfile
HEALTHCHECK CMD curl --fail http://localhost || exit 1
```

---

### ✅ **27. What are restart policies in Docker?**
- `no`
- `on-failure`
- `always`
- `unless-stopped`

---

### ✅ **28. How do you push and pull Docker images from Docker Hub?**
```bash
docker login  
docker push <username>/image  
docker pull <username>/image
```

---

### ✅ **29. How can you version Docker images?**
Using tags:
```bash
docker tag myimage myimage:v1.0
```

---

### ✅ **30. How to remove unused Docker images and containers?**
```bash
docker system prune
```

---

### ✅ **31. How do you set resource limits on containers?**
```bash
docker run --memory="512m" --cpus="1.5" myimage
```

---

### ✅ **32. What are dangling images in Docker?**
Images with no tag and not used by any container.

---

### ✅ **33. How do you handle secrets in Docker?**
Use Docker Swarm secrets or external tools like **HashiCorp Vault**, **AWS Secrets Manager**.

---

### ✅ **34. How to update an image in a running container?**
You can't update directly. Rebuild the image and re-deploy the container.

---

### ✅ **35. Explain image layering and caching in builds.**
Docker caches intermediate layers during build unless source or instruction changes.

---

### ✅ **36. What is a scratch image?**
A special base image with **nothing** in it. Used to build **minimal, secure** containers.

---

### ✅ **37. Can a container have multiple processes?**
Yes, but it’s discouraged. Use a process manager like `supervisord` if needed.

---

### ✅ **38. How do you manage Docker in production?**
- Use orchestration (Kubernetes, Swarm)
- Logging and monitoring
- Image scanning (Trivy, Clair)
- Immutable infrastructure

---

### ✅ **39. What are image digests in Docker?**
SHA256 hash representing an image, used to uniquely identify exact image version.

---

### ✅ **40. How do you troubleshoot a slow container startup?**
- Check image size
- Inspect container logs
- Use health checks
- Profile the application

---

### ✅ **41. How do you inspect a Docker container?**
```bash
docker inspect <container_id>
```

---

### ✅ **42. How do you share data between containers?**
Use volumes or shared mounts in a user-defined bridge network.

---

### ✅ **43. What is the difference between `docker exec` and `docker attach`?**
- `exec`: Run a new command in a container
- `attach`: Connect to container's main process

---

### ✅ **44. What is the use of `docker save` and `docker load`?**
- `save`: Save image to a tar archive
- `load`: Load image from archive

---

### ✅ **45. What is `docker export` and `docker import`?**
- `export`: Export container's filesystem as tar
- `import`: Create image from tarball

---

### ✅ **46. What is the purpose of `docker events`?**
It shows real-time events from the Docker daemon.

---

### ✅ **47. What’s the difference between `--link` and user-defined networks?**
`--link` is legacy and limited; user-defined networks are recommended.

---

### ✅ **48. What tools do you use for Docker image scanning?**
- **Trivy**
- **Clair**
- **Anchore**
- **Docker Hub scanning**

---

### ✅ **49. How do you monitor Docker containers in production?**
- **cAdvisor**
- **Prometheus + Grafana**
- **Datadog**
- **ELK Stack**

---

### ✅ **50. How would you deploy a Dockerized app in Kubernetes?**
- Write Dockerfile
- Push image to registry
- Create Kubernetes `Deployment` YAML
- Expose using `Service`

---

If you want:
- A **PDF version** of these questions
- 50 **Advanced Docker + Kubernetes** questions
- Docker questions with **coding exercises**
- Docker interview **assignments/tasks** examples

Let me know, Aditya!