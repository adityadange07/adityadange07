Here are the **Top 50 Docker Interview Questions and Answers** tailored for someone with **1 year of experience**. These cover basic to slightly intermediate concepts to help you crack interviews confidently.

---

## 🔹 **Basic Docker Interview Questions (1–20)**

1. **What is Docker?**  
   Docker is an open-source platform used to develop, ship, and run applications inside lightweight, portable containers.

2. **What is a Docker container?**  
   A container is a lightweight, standalone, executable package that includes everything needed to run a piece of software: code, runtime, system tools, libraries, and settings.

3. **What is the difference between a container and a virtual machine?**  
   Containers share the host OS kernel and are lightweight, while VMs include a full OS and are heavier in size.

4. **What is Docker Engine?**  
   Docker Engine is the core part of Docker, responsible for building and running containers.

5. **What are Docker images?**  
   Docker images are read-only templates used to create containers. They contain the app and its environment.

6. **How do you create a Docker container?**  
   Using the command: `docker run <image_name>`

7. **How do you list all running containers?**  
   `docker ps`

8. **How do you list all containers (including stopped)?**  
   `docker ps -a`

9. **How do you stop a running container?**  
   `docker stop <container_id>`

10. **How do you remove a container?**  
    `docker rm <container_id>`

11. **How do you remove an image?**  
    `docker rmi <image_id>`

12. **What is a Dockerfile?**  
    A text file with a set of instructions to build a Docker image.

13. **What is the command to build a Docker image?**  
    `docker build -t <image_name> .`

14. **How do you check Docker version?**  
    `docker --version`

15. **How do you pull an image from Docker Hub?**  
    `docker pull <image_name>`

16. **How do you push an image to Docker Hub?**
   ```
   docker tag <image_name> <dockerhub_username>/<image_name>
   docker push <dockerhub_username>/<image_name>
   ```

17. **What is Docker Hub?**  
    A cloud-based registry service where you can find and share container images.

18. **What is the difference between CMD and ENTRYPOINT in a Dockerfile?**  
    `CMD` provides defaults, while `ENTRYPOINT` is used to define the main command.

19. **How can you see logs of a container?**  
    `docker logs <container_id>`

20. **What is the use of `.dockerignore` file?**  
    It excludes files and directories from the Docker build context.

---

## 🔹 **Intermediate Docker Interview Questions (21–40)**

21. **What is the difference between `COPY` and `ADD` in Dockerfile?**  
    Both copy files, but `ADD` also supports remote URLs and extracting tar files.

22. **What is Docker Compose?**  
    A tool to define and run multi-container applications using a `docker-compose.yml` file.

23. **How do you start services in Docker Compose?**  
    `docker-compose up`

24. **How do you stop services in Docker Compose?**  
    `docker-compose down`

25. **What is the default network driver used by Docker?**  
    Bridge network.

26. **How do you create a Docker network?**  
    `docker network create <network_name>`

27. **How do containers communicate in Docker Compose?**  
    Using service names as hostnames over a common network.

28. **What is a Docker Volume?**  
    A mechanism for persisting data generated and used by Docker containers.

29. **How do you create a Docker volume?**  
    `docker volume create <volume_name>`

30. **How do you mount a volume in a container?**  
    `docker run -v <volume_name>:/path/in/container <image_name>`

31. **What is the difference between bind mounts and volumes?**  
    Bind mounts map host paths; volumes are managed by Docker and more portable.

32. **How can you enter into a running Docker container?**  
    `docker exec -it <container_id> /bin/bash`

33. **What happens when you restart the Docker daemon?**  
    Running containers are stopped and restarted depending on their restart policies.

34. **How do you view the Docker container’s resource usage?**  
    `docker stats`

35. **How do you check details of a Docker image or container?**  
    `docker inspect <image_or_container_id>`

36. **What are Docker namespaces?**  
    Namespaces isolate containers by providing separate environments for processes, filesystems, etc.

37. **What is the use of the `EXPOSE` instruction in Dockerfile?**  
    It informs Docker that the container will listen on the specified port(s).

38. **Can you run multiple processes in one Docker container?**  
    Yes, but it’s recommended to run one main process per container for maintainability.

39. **How to clean up unused containers, images, and volumes?**  
    `docker system prune`

40. **What is multi-stage build in Docker?**  
    It allows using multiple `FROM` statements to optimize image size by copying only necessary artifacts.

---

## 🔹 **Scenario-Based & Conceptual Questions (41–50)**

41. **How do you debug a Docker container that fails on start?**  
    Use `docker logs <container_id>` or run with `docker run -it --entrypoint /bin/bash <image_name>`.

42. **How do you handle secrets in Docker?**  
    Avoid hardcoding them; use environment variables or Docker secrets (in Swarm).

43. **What are Docker labels?**  
    Key-value metadata for containers and images used for organizing and managing.

44. **Can you run GUI applications in Docker?**  
    Yes, using X11 forwarding or GUI support, but it’s complex.

45. **How do you limit CPU and memory usage in Docker?**  
    Use `--memory` and `--cpus` flags in `docker run`.

46. **What is the difference between Docker Swarm and Kubernetes?**  
    Both are orchestration tools; Kubernetes is more feature-rich and widely adopted, while Swarm is simpler and integrated with Docker.

47. **How can you update a running container?**  
    You can’t directly update; stop and remove the old one, then run a new one with updated image.

48. **How do you handle application logs in Dockerized apps?**  
    Logs can be streamed using `docker logs` or redirected to external logging systems.

49. **Why is image size optimization important in Docker?**  
    Smaller images are faster to build, pull, and deploy. Use `.dockerignore`, minimal base images, and multi-stage builds.

50. **How do you make a container always restart if it crashes?**  
    Use restart policies like: `docker run --restart=always <image>`

---

Would you like a downloadable PDF or a categorized sheet for revision? Or shall I continue with another topic like **Kubernetes** or **Spring Boot** next?