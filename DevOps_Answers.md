# DevOps & Tools Interview Questions & Answers

## 1. CI/CD Pipeline flow (Jenkins, GitLab CI)
**Detailed Explanation**: A series of automated steps to build, test, and deploy code.
*   **CI (Continuous Integration)**: Developers commit code frequently. The server detects changes, builds the code, runs unit tests, and reports errors.
*   **CD (Continuous Delivery/Deployment)**: After CI, the artifact (JAR/Docker Image) is automatically deployed to a test environment (QA) and then to Production.
*   **Typical Flow**:
    1.  **Commit**: Dev pushes code to Git.
    2.  **Trigger**: Jenkins/GitLab detects push.
    3.  **Build**: Maven/Gradle compiles code.
    4.  **Test**: JUnit tests run.
    5.  **Scan**: SonarQube checks code quality.
    6.  **Package**: Create JAR or Docker Image.
    7.  **Deploy**: Push to Artifactory/DockerHub -> Deploy to Kubernetes.

**Example (Jenkinsfile)**:
```groovy
pipeline {
    agent any
    stages {
        stage('Build') {
            steps { sh 'mvn clean install' }
        }
        stage('Test') {
            steps { sh 'mvn test' }
        }
        stage('Deploy') {
            steps { sh './deploy.sh' }
        }
    }
}
```

---

## 2. Docker: What is a Container? Image vs Container
**Detailed Explanation**:
*   **Container**: A lightweight, standalone, executable package of software that includes everything needed to run it (code, runtime, system tools, libraries, settings). It isolates the app from the host OS.
*   **Image**: The **blueprint** or template (read-only).
*   **Container**: The **running instance** of an Image.
*   **Analogy**:
    *   **Class (OOP)** = **Docker Image**.
    *   **Object (OOP)** = **Docker Container**.

---

## 3. Docker Commands
**Detailed Explanation**:
*   **`docker build -t my-app .`**: Build an image from Dockerfile.
*   **`docker run -p 8080:8080 my-app`**: Create and start a container. Map host port 8080 to container port 8080.
*   **`docker ps`**: List running containers.
*   **`docker exec -it <id> /bin/bash`**: Enter inside a running container.
*   **`docker stop <id>`**: Gracefully stop container.

---

## 4. Docker Compose
**Detailed Explanation**: A tool for defining and running **multi-container** Docker applications.
*   **Usage**: Instead of running 5 `docker run` commands for App, DB, Redis, etc., you define them in one `docker-compose.yml` file.
*   **Command**: `docker-compose up -d` starts the whole environment.

**Example (docker-compose.yml)**:
```yaml
version: '3'
services:
  web:
    image: my-web-app
    ports:
      - "8080:8080"
  database:
    image: postgres
    environment:
      POSTGRES_PASSWORD: secret
```

---

## 5. Kubernetes: What is a Pod? Deployment, Service.
**Detailed Explanation**: K8s is a container orchestration tool.
*   **Pod**: The smallest unit in K8s. Represents a running process. Can contain one or more containers (usually one).
*   **ReplicaSet**: Ensures a specified number of replicas (copies) of a Pod are running at all times.
*   **Deployment**: Manages ReplicaSets. Supports rolling updates and rollbacks.
*   **Service**: An abstraction that defines a logical set of Pods and a policy to access them (like a Load Balancer). It gives a stable IP to a group of dynamic Pods.

---

## 6. AWS Services (EC2, S3, Lambda, IAM)
**Detailed Explanation**:
*   **EC2 (Elastic Compute Cloud)**: Virtual Servers (VMs). You manage the OS and software.
*   **S3 (Simple Storage Service)**: Object storage (Files, Images, Backups). Infinite storage.
*   **Lambda**: Serverless Compute. Run code without provisioning servers. Pay only for compute time.
*   **IAM (Identity and Access Management)**: Manage Users, Roles, and Permissions.
*   **CloudWatch**: Monitoring and Logging service for AWS resources.

---

## 7. Maven Lifecycle and phases
**Detailed Explanation**:
*   **Lifecycle**: The sequence of steps to build a project.
*   **Key Phases** (in order):
    1.  **validate**: Check info.
    2.  **compile**: Compile source code.
    3.  **test**: Run unit tests.
    4.  **package**: Create JAR/WAR.
    5.  **verify**: Integration tests.
    6.  **install**: Install artifact to local repository (~/.m2).
    7.  **deploy**: Copy artifact to remote repository (Nexus/Artifactory).

---

## 8. Git Commands
**Detailed Explanation**:
*   **`git commit -m "msg"`**: Save changes locally.
*   **`git push origin main`**: Send local commits to remote server (GitHub).
*   **`git pull`**: Fetch and Merge changes from remote to local.
*   **`git merge branch`**: Combine branch history into current branch.
*   **`git rebase branch`**: Move current branch changes to top of target branch (Linear history).
*   **`git cherry-pick <hash>`**: Pick one specific commit from another branch and apply it.
*   **`git reset --hard`**: Discard all changes.
*   **`git revert <hash>`**: Create a new commit that undoes the changes of a previous commit (Safe for shared history).

---

## 9. Monitoring and Logging (ELK, Prometheus)
**Detailed Explanation**:
*   **Logging (ELK Stack)**:
    *   **Elasticsearch**: Search engine (Index logs).
    *   **Logstash**: Ingest and process logs.
    *   **Kibana**: Visualization UI (Dashboards).
*   **Monitoring**:
    *   **Prometheus**: Scrapes metrics (numbers) from apps (CPU, Request count).
    *   **Grafana**: Visualizes those metrics in beautiful charts.

---

## 10. Deployment Strategies
**Detailed Explanation**:
1.  **Blue-Green**:
    *   Two identical environments (Blue=Live, Green=New).
    *   Deploy to Green. Test it.
    *   Switch Load Balancer from Blue to Green.
    *   Zero Downtime. Quick Rollback.
2.  **Canary**:
    *   Deploy new version to a small % of users (e.g., 5%).
    *   Monitor functionality.
    *   Gradually increase traffic to 100%.

---

## 11. Linux Commands
**Detailed Explanation**:
*   **`grep "text" file`**: Search for text patterns.
*   **`cat file`**: Display file content.
*   **`chmod 777 file`**: Change permissions (Read/Write/Execute).
*   **`chown user:group file`**: Change owner.
*   **`ps -ef`**: List current processes.
*   **`top`**: Monitor system resources (CPU/RAM usage).
*   **`tail -f file.log`**: Watch log file in real-time.

---

## 12. SonarQube integration
**Detailed Explanation**:
*   **SonarQube**: A tool for continuous inspection of code quality.
*   **Checks**: Bugs, Vulnerabilities, Code Smells, Duplication.
*   **Code Coverage**: Integration with JaCoCo (Java Code Coverage) to verify unit tests cover >80% of lines.
*   **Quality Gate**: Pipeline fails if Code Coverage < 80% or Critical Issues > 0.
