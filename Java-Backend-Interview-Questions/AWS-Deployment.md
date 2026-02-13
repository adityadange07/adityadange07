
## 471. What is AWS?

**Answer:**
**AWS (Amazon Web Services)** is a secure cloud services platform, offering compute power, database storage, content delivery, and other functionality.
*   **Infrastructure as a Service (IaaS):** Provides virtualized computing resources over the internet.
*   **Benefits:** Scalability, Pay-as-you-go pricing, Global reliability.

---

## 472. What is EC2?

**Answer:**
**EC2 (Elastic Compute Cloud)** is a web service that provides secure, resizable compute capacity in the cloud.
*   **Instance:** Virtual server.
*   **Types:** General Purpose (T3, M5), Compute Optimized (C5), Memory Optimized (R5).
*   **Role:** Running applications, backend servers, microservices.

---

## 473. What is S3?

**Answer:**
**S3 (Simple Storage Service)** is an object storage service.
*   **Object:** File + Metadata (not a block store).
*   **Structure:** Data is stored in **Buckets**.
*   **Use Case:** Storing backups, static website hosting, media files, data lakes.
*   **Durability:** 99.999999999% (11 9s).

---

## 474. What is RDS?

**Answer:**
**RDS (Relational Database Service)** makes it easy to set up, operate, and scale a relational database in the cloud.
*   **Engines:** MySQL, PostgreSQL, MariaDB, Oracle, SQL Server, Aurora.
*   **Managed Features:** Automated backups, patching, Multi-AZ deployment (High Availability), Read Replicas.

---

## 475. What is IAM?

**Answer:**
**IAM (Identity and Access Management)** enables you to manage access to AWS services and resources securely.
*   **Users:** People/Applications.
*   **Groups:** Collections of users.
*   **Roles:** Permissions assigned to trusted entities (e.g., EC2 instance accessing S3).
*   **Policies:** JSON documents defining permissions (Allow/Deny).

---

## 476. What is VPC?

**Answer:**
**VPC (Virtual Private Cloud)** is a logically isolated section of the AWS Cloud where you can launch resources in a virtual network that you define.
*   **Control:** You control IP ranges, subnets, route tables, and gateways.
*   **Goal:** Security and Network isolation.

---

## 477. What is subnet?

**Answer:**
A **Subnet** is a range of IP addresses in your VPC.
*   **Public Subnet:** Has a route to the Internet Gateway (can access internet). Used for Load Balancers, Bastion Hosts.
*   **Private Subnet:** No direct route to the Internet. Used for App Servers, Databases (Security best practice).

---

## 478. What is security group?

**Answer:**
A **Security Group** acts as a **virtual firewall** for your instance to control inbound and outbound traffic.
*   **Stateful:** If you allow an incoming request, the response is automatically allowed.
*   **Scope:** Applied at the **Instance level**.
*   **Default:** Deny all inbound, Allow all outbound.

---

## 479. What is NACL?

**Answer:**
**NACL (Network Access Control List)** is an optional layer of security for your VPC that acts as a firewall for controlling traffic in and out of one or more subnets.
*   **Stateless:** You must explicitly allow both inbound and outbound traffic.
*   **Scope:** Applied at the **Subnet level**.

---

## 480. What is Elastic Load Balancer?

**Answer:**
**ELB (Elastic Load Balancer)** automatically distributes incoming application traffic across multiple targets, such as EC2 instances, containers, and IP addresses.
*   **Types:**
    1.  **ALB (Application Load Balancer):** Layer 7 (HTTP/HTTPS). Path-based routing.
    2.  **NLB (Network Load Balancer):** Layer 4 (TCP/UDP). High performance.
    3.  **CLB (Classic Load Balancer):** Legacy.

---

## 481. What is Auto Scaling?

**Answer:**
**Auto Scaling** monitors your applications and automatically adjusts capacity to maintain steady, predictable performance at the lowest possible cost.
*   **Scale Out:** Add EC2 instances when CPU > 70%.
*   **Scale In:** Remove EC2 instances when CPU < 20%.
*   **Group:** **ASG (Auto Scaling Group)** manages the collection of EC2 instances.

---

## 482. What is Route 53?

**Answer:**
**Route 53** is a highly available and scalable **DNS (Domain Name System)** web service.
*   **Function:** Translates domain names (`www.example.com`) to IP addresses (`192.0.2.1`).
*   **Features:** Health checks, Failover routing, Latency-based routing, Geo-location routing.

---

## 483. What is CloudFront?

**Answer:**
**CloudFront** is a global **CDN (Content Delivery Network)** service that delivers data, videos, applications, and APIs to customers globally with low latency.
*   **Mechanism:** Caches content at **Edge Locations** closer to the user.
*   **Benefit:** Reduces load on the origin server (S3/EC2) and speeds up content delivery.

---

## 484. What is ECR?

**Answer:**
**ECR (Elastic Container Registry)** is a fully managed Docker container registry.
*   **Role:** Stores, manages, and deploys Docker container images.
*   **Integration:** Works seamlessly with ECS and EKS.

---

## 485. What is ECS?

**Answer:**
**ECS (Elastic Container Service)** is a fully managed container orchestration service.
*   **Role:** Runs and manages Docker containers on a cluster of EC2 instances (or Fargate).
*   **Simplicity:** Easier to set up than Kubernetes but less flexible.

---

## 486. What is EKS?

**Answer:**
**EKS (Elastic Kubernetes Service)** is a managed service to run **Kubernetes** on AWS.
*   **Role:** Runs K8s control plane and worker nodes.
*   **Use Case:** Standard way to run K8s applications, migrating existing K8s workloads.

---

## 487. What is Lambda?

**Answer:**
**Lambda** is a **Serverless** compute service that lets you run code without provisioning or managing servers.
*   **Trigger:** Responds to events (S3 upload, API Gateway request, DynamoDB update).
*   **Pricing:** Pay only for the compute time you consume (millis).
*   **Limit:** Execution time limit (15 mins).

---

## 488. What is API Gateway?

**Answer:**
**API Gateway** is a fully managed service that makes it easy for developers to create, publish, maintain, monitor, and secure APIs.
*   **Role:** Acts as a "front door" for applications to access data/logic from backend services (Lambda, EC2).
*   **Features:** Throttling, Caching, Authentication (Cognito/IAM), API Keys.

---

## 489. What is CloudWatch?

**Answer:**
**CloudWatch** is a **monitoring** and observability service.
*   **Metrics:** CPU utilization, Disk I/O, Network traffic.
*   **Logs:** Collects and stores logs from EC2, Lambda, etc.
*   **Alarms:** Send notifications (SNS) when a threshold is breached (e.g., CPU > 80%).

---

## 490. What is CloudTrail?

**Answer:**
**CloudTrail** provides **auditing**, security monitoring, and operational troubleshooting.
*   **Function:** Records **API calls** made on your account.
*   **Use Case:** "Who deleted this S3 bucket?" "Who terminated this EC2 instance?" - CloudTrail has the answer.

---

## 491. What is blue-green deployment in AWS?

**Answer:**
**Blue-Green Deployment** is a technique that reduces downtime and risk by running two identical production environments.
*   **Blue:** Current live environment.
*   **Green:** New version of the application.
*   **Switch:** Once Green is tested, you switch the Load Balancer/DNS to point to Green. Blue becomes idle.
*   **Rollback:** Instant. Just switch back to Blue.

---

## 492. What is rolling deployment?

**Answer:**
**Rolling Deployment** updates instances with the new version incrementally.
*   **Process:** Update 2 instances -> Wait for health check -> Update next 2 -> Repeat.
*   **Pros:** Zero downtime, no need for double capacity (like Blue-Green).
*   **Cons:** Application runs in mixed versions during the deployment window.

---

## 493. What is infrastructure as code?

**Answer:**
**IaC (Infrastructure as Code)** is the practice of managing and provisioning infrastructure through machine-readable definition files, rather than physical hardware configuration or interactive configuration tools.
*   **Tools:** Terraform, AWS CloudFormation, Ansible.
*   **Benefits:** Consistency, Version Control (Git), Reproducibility.

---

## 494. What is CloudFormation?

**Answer:**
**AWS CloudFormation** is a service that gives developers an easy way to create a collection of related AWS resources (stack) using templates (JSON/YAML).
*   **Native:** deeply integrated with AWS.
*   **State:** Manages the state of your stack automatically.

---

## 495. What is Terraform?

**Answer:**
**Terraform** is an open-source IaC tool by HashiCorp that allows you to define cloud and on-prem resources in human-readable configuration files (HCL).
*   **Cloud Agnostic:** Works with AWS, Azure, GCP.
*   **State Management:** Uses a state file (`terraform.tfstate`) to map resources to configuration.

---

## 496. How to deploy Spring Boot in AWS?

**Answer:**
1.  **EC2:** Copy JAR, run `java -jar app.jar`. Manual or via User Data script.
2.  **Elastic Beanstalk:** Upload JAR, AWS manages OS/Tomcat/Scaling.
3.  **ECS/EKS:** Dockerize app, push to ECR, deploy as a Task/pod.
4.  **Lambda:** Deploy as a Serverless function (SnapStart for faster cold starts).

---

## 497. How to secure application in AWS?

**Answer:**
1.  **VPC:** Deploy app in Private Subnets.
2.  **Security Groups:** Allow traffic only from Load Balancer (port 80/443).
3.  **IAM:** Use Roles (not Access Keys) for EC2 to access S3/DB. **Least Privilege** principle.
4.  **WAF (Web App Firewall):** Protect against SQLi, XSS.
5.  **HTTPS:** Use ACM (Amazon Certificate Manager) for SSL.

---

## 498. What is SSL termination?

**Answer:**
**SSL Termination** is the process of decrypting encrypted traffic (HTTPS) at the Load Balancer (ELB) before sending it to the backend servers (over HTTP).
*   **Benefit:** Offloads the CPU-intensive decryption work from the application servers, allowing them to focus on logic.

---

## 499. How to configure autoscaling?

**Answer:**
1.  **Launch Template:** Define "What" to launch (AMI, Instance Type, Security Groups).
2.  **Auto Scaling Group (ASG):** Define "Where" (VPC, Subnets) and "How many" (Min: 2, Max: 10).
3.  **Scaling Policies:**
    *   **Target Tracking:** Keep CPU at 50%.
    *   **Step/Simple:** If Alarm > 80%, add 2 instances.

---

## 500. Production deployment checklist?

**Answer:**
1.  **Code:** Unit/Integration tests passed? Code reviewed?
2.  **Config:** Env variables set? Secrets (DB params) in Secrets Manager?
3.  **Database:** Migrations (Flyway) tested? backup taken?
4.  **Infrastructure:** Autoscaling configured? Health checks (Liveness/Readiness) active?
5.  **Security:** HTTPS enabled? Security Groups tight?
6.  **Observability:** Logging (CloudWatch/Splunk) and Monitoring (NewRelic/Datadog) enabled?
7.  **Rollback Strategy:** Is Blue-Green or Rolling enabled?

---

## 501. Design highly available architecture in AWS.

**Answer:**
**Goal:** Eliminate Single Points of Failure (SPOF).
1.  **Region:** Choose a region (e.g., us-east-1).
2.  **VPC:** Multi-AZ deployment.
3.  **Compute:** Auto Scaling Group spanning at least 2 **Availability Zones (AZs)**.
4.  **Database:** RDS Multi-AZ (Primary in AZ A, Standby in AZ B).
5.  **Load Balancing:** ALB distributing traffic across instances in all AZs.

---

## 502. Multi-region deployment strategy?

**Answer:**
**Goal:** Global low latency and Disaster Recovery.
1.  **Active-Active:** Traffic goes to both regions (Route 53 Geo Routing). DynamoDB Global Tables or Aurora Global Database sync data.
2.  **Active-Passive:** Traffic goes to Region A. Region B is cold/warm standby.

---

## 503. Disaster recovery strategy?

**Answer:**
RPO (Recovery Point Objective - Data Loss) vs RTO (Recovery Time Objective - Downtime).
1.  **Backup & Restore:** Cheapest, highest RTO/RPO.
2.  **Pilot Light:** DB data is live in DR region, app servers are off.
3.  **Warm Standby:** Scaled-down version running in DR region.
4.  **Multi-Site Active/Active:** Zero downtime, most expensive.

---

## 504. Backup strategy?

**Answer:**
1.  **RDS:** Enable Automated Backups (Retention 7-35 days). Manual Snapshots before major changes.
2.  **S3:** Enable Versioning and Cross-Region Replication (CRR) for critical buckets.
3.  **EBS:** AWS Backup service to automate volume snapshots.
4.  **DynamoDB:** Point-In-Time Recovery (PITR).

---

## 505. High traffic scaling strategy?

**Answer:**
1.  **CDN (CloudFront):** Offload static assets.
2.  **Caching (ElastiCache):** Offload DB reads.
3.  **Auto Scaling (ASG):** Scale compute based on traffic.
4.  **DB Scaling:** Read Replicas for reads, Sharding for writes.
5.  **Async Processing:** Use SQS/Kinesis to buffer writes during spikes.

---

## 506. Secure microservices in AWS?

**Answer:**
1.  **Private Subnets:** No direct internet access.
2.  **Internal ALB:** Use internal load balancers for inter-service comms.
3.  **Security Groups:** Service A SG allows traffic only from Service B SG.
4.  **IAM Roles:** Services use IAM roles (IRSA for EKS) to access resources.
5.  **mTLS:** Use App Mesh or Istio for encrypted service-to-service communication.

---

## 507. Deploy Kafka in AWS?

**Answer:**
1.  **MSK (Managed Streaming for Kafka):** Fully managed, High Availability, auto-patching. Best for production.
2.  **EC2:** Install Kafka on EC2. Full control, but high maintenance (Zookeeper management, OS patching).

---

## 508. Deploy Redis in AWS?

**Answer:**
1.  **ElastiCache for Redis:** Fully managed.
    *   **Cluster Mode Enabled:** Sharding for write scaling.
    *   **Multi-AZ:** Auto-failover.
2.  **EC2:** Self-managed Redis (Avoid unless necessary).

---

## 509. RDS performance tuning?

**Answer:**
1.  **Instance Class:** Upgrade CPU/RAM (Vertical Scaling).
2.  **IOPS:** Switch storage type to **Provisioned IOPS (io1/io2)** for high disk throughput.
3.  **Performance Insights:** Use AWS tool to find slow SQL.
4.  **Read Replicas:** Offload reads.
5.  **Parameter Group:** Tune MySQL/PG params (e.g., `innodb_buffer_pool_size`).

---

## 510. Cost optimization strategies?

**Answer:**
1.  **Reserved Instances (RI) / Savings Plans:** Commit for 1-3 years for ~70% discount.
2.  **Spot Instances:** Use for fault-tolerant batch jobs (~90% discount).
3.  **Right Sizing:** Compute Optimizer acts to downgrade oversized instances.
4.  **S3 Lifecycle Policies:** Move old logs to S3 Glacier.
5.  **Stop Idle Resources:** Lambda script to stop Dev instances at night.

---

## 511. How to monitor production apps?

**Answer:**
**Observability Trinity:**
1.  **Metrics:** "What is happening?" (CPU is 90%).
2.  **Logs:** "Why is it happening?" (Exception stack trace).
3.  **Traces:** "Where is it happening?" (Microservice A -> B -> C).

---

## 512. What metrics do you track?

**Answer:**
**USE Method (for Infrastructure):**
1.  **Utilization:** % time busy (CPU use).
2.  **Saturation:** Queue length (Disk I/O wait).
3.  **Errors:** Count of error events.

**RED Method (for Services):**
1.  **Rate:** Requests per second (RPS).
2.  **Errors:** Failed requests per second (HTTP 500s).
3.  **Duration:** Latency (p95, p99).

---

## 513. Log aggregation tools?

**Answer:**
Tools to collect logs from multiple servers into a central search engine.
1.  **ELK Stack:** Elasticsearch, Logstash, Kibana.
2.  **Splunk:** Enterprise log management.
3.  **CloudWatch Logs:** AWS native.
4.  **Datadog/NewRelic:** SaaS observability platforms.

---

## 514. What is centralized logging?

**Answer:**
**Centralized Logging** aggregates logs from all microservices/servers into a single location.
*   **Why?** In a distributed system, you can't SSH into 50 different servers to `grep` logs.
*   **Structure:** Uses a correlation ID (Trace ID) to stitch logs across services.

---

## 515. How to debug production issue in AWS?

**Answer:**
1.  **Check Dashboards:** CloudWatch/Datadog to identify the spike/error.
2.  **Check Logs:** Query Centralized Logs using the Trace ID.
3.  **Check Traces:** Distributed Tracing (X-Ray/Jaeger) to find the slow component.
4.  **Reproduce:** Try to reproduce in Staging.

---

## 516. How to configure alerts?

**Answer:**
Alerts notify engineers when things go wrong.
*   **Threshold:** "Alert if CPU > 80% for 5 mins".
*   **Anomaly Detection:** "Alert if traffic drops by 50% compared to last week".
*   **Channels:** Slack, Email, PagerDuty (for urgent incidents).

---

## 517. How to reduce downtime?

**Answer:**
1.  **Redundancy:** Multi-AZ/Multi-Region.
2.  **Failover:** Automated health checks and DNS failover.
3.  **Circuit Breakers:** Prevent cascading failures.
4.  **Rate Limiting:** Prevent DDOS/Accidental overload.
5.  **Rollback:** Quick rollback mechanism for bad deployments.

---

## 518. What is SLA vs SLO?

**Answer:**
*   **SLA (Service Level Agreement):** Contract with the customer. "We promise 99.9% uptime or we pay you."
*   **SLO (Service Level Objective):** Internal goal. "We aim for 99.95% uptime." (Stricter than SLA).
*   **SLI (Service Level Indicator):** The actual metric. "Current uptime is 99.99%."

---

## 519. What is error budget?

**Answer:**
**Error Budget** is the amount of unreliability you are allowed to have.
*   **Calculation:** 100% - SLO (e.g., 100% - 99.9% = 0.1% budget).
*   **Use:** If you have budget left, you can ship risky features. If budget is exhausted, freeze changes and focus on stability.

---

## 520. What is autoscaling metric selection?

**Answer:**
Choosing the right metric to trigger scaling:
1.  **CPU Utilization:** Good for compute-heavy apps.
2.  **Request Count:** Good for I/O bound web apps.
3.  **SQS Queue Depth:** Good for worker services processing jobs.
4.  **Memory:** Rarely used (Java GC complicates this), but useful for memory leaks.

---

## 521. IAM best practices?

**Answer:**
1.  **Least Privilege:** Grant only necessary permissions.
2.  **MFA:** Enable Multi-Factor Authentication for Root and IAM users.
3.  **Roles over User:** Use IAM Roles for EC2/Lambda instead of long-term credentials (Access Keys).
4.  **Rotate Credentials:** Rotate Access Keys every 90 days.
5.  **No Root:** Never use the Root account for daily tasks.

---

## 522. How to protect secrets?

**Answer:**
Never hardcode secrets (DB passwords, API Keys) in code.
1.  **AWS Secrets Manager:** Automatic rotation, centralized management.
2.  **AWS Systems Manager Parameter Store:** Cheaper alternative for config/secrets (SecureString).
*   **Access:** App retrieves secret at runtime using IAM Role.

---

## 523. What is KMS?

**Answer:**
**KMS (Key Management Service)** is a managed service to create and control cryptographic keys.
*   **CMK (Customer Master Key):** Used to encrypt/decrypt data encryption keys.
*   **Integration:** Integrated with S3, EBS, RDS for "Encryption at Rest".

---

## 524. What is WAF?

**Answer:**
**WAF (Web Application Firewall)** protects web applications from common exploits.
*   **Layer:** Layer 7 (HTTP).
*   **Rules:** Block SQL Injection, XSS, Geo-blocking (block traffic from specific countries), Rate-based rules (DDoS).

---

## 525. DDoS protection?

**Answer:**
1.  **AWS Shield Standard:** Free, protects against L3/L4 attacks (SYN floods).
2.  **AWS Shield Advanced:** Paid, protects against sophisticated L7 attacks, provides 24/7 access to DRT (DDoS Response Team).
3.  **CloudFront/WAF:** Absorbs traffic at the edge.

---

## 526. How to restrict S3 bucket?

**Answer:**
1.  **Block Public Access:** Enable "Block all public access" setting.
2.  **Bucket Policy:** JSON policy to explicitly allow/deny access (e.g., only allowing CloudFront OAI).
3.  **ACLs:** (Legacy) Access Control Lists.
4.  **IAM Policy:** Control which users/roles can access the bucket.

---

## 527. How to encrypt data at rest?

**Answer:**
Encryption of data when it is stored on disk.
*   **S3:** Server-Side Encryption (SSE-S3, SSE-KMS).
*   **EBS/RDS:** Enable encryption checkbox during creation (uses KMS).
*   **DynamoDB:** Encrypted by default.

---

## 528. How to encrypt data in transit?

**Answer:**
Encryption of data as it moves between client and server.
*   **HTTPS (TLS/SSL):** Use ACM certificates on Load Balancers/CloudFront.
*   **VPN/Direct Connect:** Encrypted tunnel between on-prem and AWS.

---

## 529. Key rotation strategy?

**Answer:**
1.  **KMS:** Enable automatic key rotation (changes backing key material every year).
2.  **Secrets Manager:** Configured to rotate DB passwords automatically (calls a Lambda function to update DB and Secret).
3.  **IAM Access Keys:** Enforce policy to rotate every 90 days.

---

## 530. Secure CI/CD pipeline?

**Answer:**
1.  **Least Privilege:** CI/CD role should only have permission to deploy to specific resources using `AssumeRole`.
2.  **Scan Artifacts:** Scan Docker images (ECR) and Code (SonarQube) for vulnerabilities.
3.  **No Secrets in Repo:** Use OIDC (OpenID Connect) for git provider (GitHub Actions) to auth with AWS without long-lived keys.
4.  **Audit:** Enable CloudTrail to track deployment activities.
