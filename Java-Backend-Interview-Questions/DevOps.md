
## 841. What is DevOps?

**Answer:**
**DevOps** is a set of practices, tools, and cultural philosophies that automate and integrate the processes between software development (**Dev**) and IT teams (**Ops**).
*   **Goal:** Shorten the systems development life cycle and provide continuous delivery with high software quality.
*   **Key Pillars:** CAMS (Culture, Automation, Measurement, Sharing).

---

## 842. DevOps vs Agile?

**Answer:**
*   **Agile:** Focuses on **Software Development** processes.
    *   *Goal:* Faster delivery of features, adapting to change, customer collaboration.
    *   *Artifacts:* Sprints, User Stories, Scrum.
*   **DevOps:** Focuses on **End-to-End Delivery** (Dev + Ops).
    *   *Goal:* Automation of build, test, and deployment.
    *   *Artifacts:* CI/CD Pipelines, IaC, Monitoring.
*   *Relation:* DevOps often enables Agile by providing the speed associated with Agile development.

---

## 843. What is CI/CD pipeline?

**Answer:**
**CI/CD** allows frequent and reliable code delivery.
*   **CI (Continuous Integration):** Developers merge changes to the main branch often. Automated builds and tests run to validate changes.
*   **CD (Continuous Delivery):** Automatically preparing the code for release to production (requires manual approval to deploy).
*   **CD (Continuous Deployment):** Automatically deploying every change that passes tests to production (no manual approval).

---

## 844. What is infrastructure as code?

**Answer:**
**IaC (Infrastructure as Code)** is the managing and provisioning of infrastructure through code instead of manual processes.
*   **Tools:** Terraform, CloudFormation, Ansible.
*   **Benefits:**
    *   **Consistency:** Prevents configuration drift.
    *   **Version Control:** Infrastructure changes are tracked in Git.
    *   **Speed:** Rapid setup/teardown of environments.

---

## 845. What is configuration management?

**Answer:**
**Configuration Management** maintains the consistency of a product's performance and functional/physical attributes throughout its life.
*   **In DevOps:** Tools that manage software installation, patching, and configuration on servers.
*   **Tools:** Ansible (Agentless, Push), Chef (Agent-based, Pull), Puppet.

---

## 846. What is monitoring in DevOps?

**Answer:**
**Monitoring** involves collecting data about the system's performance and health.
*   **Levels:**
    1.  **Infrastructure:** CPU, RAM, Disk (e.g., Nagios, Zabbix).
    2.  **Application:** JVM Heap, Response Time (e.g., Prometheus, New Relic).
    3.  **Network:** Latency, Packet Loss.

---

## 847. What is observability?

**Answer:**
**Observability** is the measure of how well you can understand the internal state of a system from its external outputs. It answers "Why is this happening?"
*   **Three Pillars:**
    1.  **Logs:** (Events) "Something happened at X time."
    2.  **Metrics:** (Numbers) "CPU is at 90%."
    3.  **Traces:** (Flow) "Request took 500ms in Service A and 200ms in Service B."

---

## 848. What is logging strategy?

**Answer:**
A **Logging Strategy** defines what, how, and where to log.
*   **Best Practices:**
    1.  **Structured Logging:** JSON format (easier to parse).
    2.  **Correlation ID:** Unique ID per request passed across microservices.
    3.  **Levels:** Use correct levels (ERROR, WARN, INFO, DEBUG).
    4.  **Centralization:** Ship logs to ELK Stack (Elasticsearch, Logstash, Kibana) or Splunk.
    5.  **Retention:** Archive old logs to S3 (cheaper) and delete after X days.

---

## 849. What is blue-green deployment?

**Answer:**
**Blue-Green Deployment** is a release management strategy that reduces downtime.
*   **Setup:** Two identical environments (Blue = Live, Green = Idle/New Version).
*   **Process:**
    1.  Deploy new version to **Green**.
    2.  Run tests on Green.
    3.  Switch Router/Load Balancer to point to **Green** (Instant cutover).
    4.  Blue becomes idle (can be used for rollback).

---

## 850. What is canary release?

**Answer:**
**Canary Release** involves rolling out the new version to a **small subset of users** first before a full rollout.
*   **Goal:** Reduce risk. If the new version is buggy, only 5% of users are affected.
*   **Process:**
    1.  Route 5% traffic to V2, 95% to V1.
    2.  Monitor errors/metrics.
    3.  Gradually increase traffic (10%, 50%, 100%).

---

## 851. What is rolling update?

**Answer:**
**Rolling Update** replaces instances of the old version with the new version **incrementally** (one by one or in batches).
*   **Process:**
    1.  Deploy V2 to Instance 1. Wait for health check.
    2.  Deploy V2 to Instance 2. Wait...
    3.  Repeat until all instances are V2.
*   **Pros:** Zero downtime.
*   **Cons:** Slow rollouts; temporary version mismatch (some users see V1, some V2).

---

## 852. What is rollback plan?

**Answer:**
A **Rollback Plan** is a pre-defined strategy to revert the system to a previous stable state if a deployment fails.
*   **Strategies:**
    *   **Blue-Green:** Switch traffic back to Blue environment.
    *   **Rolling:** Re-deploy the previous Docker image/tag.
    *   **Database:** Restore from backup or run "down" migration scripts (hard if data was mutated).

---

## 853. What is artifact versioning?

**Answer:**
**Artifact Versioning** assigns unique identifiers to build artifacts (JARs, Docker Images).
*   **Scheme:** Semantic Versioning (SemVer)  (e.g., ).
*   **Antipattern:** Overwriting  tag without unique versioning (makes rollback impossible).
*   **Best Practice:** Use Git Commit SHA or Build Number as part of the version (e.g., ).

---

## 854. What is release management?

**Answer:**
**Release Management** represents the planning, scheduling, and controlling of the build, test, and deployment of releases.
*   **Goal:** Ensure we deliver new features while protecting the integrity of the existing production environment.
*   **Key:** Communication between Dev, QA, and Ops.

---

## 855. What is environment strategy?

**Answer:**
Defining separate environments to ensure quality progression.
1.  **Dev/Local:** For coding (mocked external dependencies).
2.  **QA/Test:** Functional testing (stable environment).
3.  **Staging/Pre-Prod:** Mirror of Production (same data size, configs). Performance testing happens here.
4.  **Production:** Real user traffic.

---

## 856. What is GitOps?

**Answer:**
**GitOps** is a way of implementing Continuous Deployment for cloud native applications.
*   **Core Idea:** Git is the **Single Source of Truth** for infrastructure and application configuration.
*   **Mechanism:** An operator (like ArgoCD or Flux) inside the cluster detects drift between Git repo (desired state) and the Cluster (actual state) and syncs them automatically.

---

## 857. What is SRE?

**Answer:**
**SRE (Site Reliability Engineering)** is a discipline that incorporates aspects of software engineering and applies them to infrastructure and operations problems.
*   **Origin:** Google.
*   **Goal:** Create scalable and highly reliable software systems.
*   **Key Concept:** "Hope is not a strategy." Automate everything. Treat Ops problems as software problems.

---

## 858. What is incident management?

**Answer:**
**Incident Management** is the process of handling unplanned interruptions (outages/degradation) to restore service as quickly as possible.
*   **Process:**
    1.  **Detect:** Monitoring alerts.
    2.  **Respond:** On-call engineer acknowledges.
    3.  **Recover:** Apply fix/workaround.
    4.  **Communicate:** Update status page for users.

---

## 859. What is postmortem?

**Answer:**
A **Postmortem (RCA - Root Cause Analysis)** is a document written after an incident is resolved.
*   **Goal:** Learn from failure, not to blame. (Blameless Culture).
*   **Contents:**
    *   Timeline of events.
    *   Root cause (5 Whys).
    *   Impact.
    *   Action items to prevent recurrence.

---

## 860. What is SLA vs SLO vs SLI?

**Answer:**
*   **SLI (Service Level Indicator):** The **metric** (Number).
    *   *e.g.,* "Request Latency".
*   **SLO (Service Level Objective):** The **goal** (Threshold).
    *   *e.g.,* "99% of requests < 200ms".
*   **SLA (Service Level Agreement):** The **contract** (Consequence).
    *   *e.g.,* "If we miss the SLO, we give customers 10% credit back."

---

## 861. What is container security?

**Answer:**
**Container Security** involves protecting the container pipeline, deployment, and runtime.
*   **Best Practices:**
    1.  **Image Scanning:** Scan for CVEs (Trivy, Clair).
    2.  **Base Image:** Use minimal images (Distroless, Alpine) to reduce attack surface.
    3.  **Non-Root:** Do NOT run containers as  user.
    4.  **Runtime:** Use tools like **Falco** to detect abnormal behavior (e.g., shell spawned in a pod).

---

## 862. What is secrets management best practice?

**Answer:**
Managing sensitive config (Passwords, Keys) in a dynamic environment.
*   **Do Not:** Hardcode in Dockerfile or commit to Git.
*   **Do:**
    1.  **Externalize:** Use Vault, AWS Secrets Manager, or Azure Key Vault.
    2.  **inject:** Mount as a volume or environment variable at runtime only.
    3.  **Rotate:** Automate rotation of database credentials.

---

## 863. What is pipeline failure handling?

**Answer:**
How to manage broken CI/CD pipelines.
*   **Strategy:**
    1.  **Stop the Line:** Prevent merging further code until fixed.
    2.  **Notification:** Alert the team immediately (Slack/Teams).
    3.  **Fast Fail:** Fail the build as early as possible (e.g., Linting first, then Unit Tests).
    4.  **Auto-Rollback:** If CD fails, revert to the last stable artifact.

---

## 864. What is capacity planning?

**Answer:**
**Capacity Planning** is the process of determining the production capacity needed to meet changing demands for the application.
*   **Inputs:** Current usage metrics, Growth projections, Load Test results.
*   **Output:** Hardware requirements (Number of Nodes, CPU/RAM sizing, Storage IOPS).

---

## 865. What is cost optimization?

**Answer:**
**FinOps** practices to reduce Cloud spend without sacrificing performance.
*   **Techniques:**
    1.  **Right-Sizing:** Matching instance types to actual load.
    2.  **Spot Instances:** Using spare capacity (cheaper) for stateless workloads.
    3.  **Auto-Scaling:** Scaling down during off-peak hours.
    4.  **Storage:** Moving infrequently accessed data to Cold Storage (S3 Glacier).

---

## 866. What is autoscaling?

**Answer:**
**Autoscaling** automatically adjusts the number of compute resources based on load.
*   **Types:**
    1.  **Horizontal (Scale Out):** Adding more instances/pods (e.g., K8s HPA).
    2.  **Vertical (Scale Up):** Increasing CPU/RAM of an existing instance (e.g., K8s VPA).
    3.  **Cluster Autoscaler:** Adding nodes to the cluster when pods are pending.

---

## 867. What is chaos engineering?

**Answer:**
**Chaos Engineering** is the discipline of experimenting on a system to build confidence in its capability to withstand turbulent conditions.
*   **Tool:** **Chaos Monkey** (Netflix).
*   **Action:** Intentionally kill services/pods, add latency, or sever network links in production (controlled) to ensure the system recovers gracefully.

---

## 868. What is fault tolerance?

**Answer:**
**Fault Tolerance** is the property that enables a system to continue operating properly in the event of the failure of some of its components.
*   **Mechanisms:**
    *   **Redundancy:** Multiple replicas of a service.
    *   **Failover:** Switching to a backup database.
    *   **Isolating:** Bulkheads (one failure doesn't crash the whole system).

---

## 869. What is backup strategy?

**Answer:**
A plan to copy data to protect against loss.
*   **3-2-1 Rule:**
    *   **3** copies of data.
    *   **2** different media types (Disk, Tape/Cloud).
    *   **1** copy offsite (Different Region).
*   **RPO (Recovery Point Objective):** Max data loss allowed (e.g., 5 mins).
*   **RTO (Recovery Time Objective):** Max downtime allowed (e.g., 1 hour).

---

## 870. What is disaster recovery?

**Answer:**
**Disaster Recovery (DR)** is the process of regaining access to infrastructure and data after a catastrophe (natural disaster, cyber attack).
*   **Strategies:**
    1.  **Backup & Restore:** Cheapest, Slowest.
    2.  **Pilot Light:** Minimal version running in DR region (db sync active, app servers off).
    3.  **Warm Standby:** Scaled-down version running always.
    4.  **Multi-Site (Hot-Hot):** Active-Active traffic in multiple regions (Zero downtime).

---

## 871. What is immutable infrastructure?

**Answer:**
**Immutable Infrastructure** is a paradigm where servers are **never modified** after deployment.
*   **Process:** If you need to update software, you replace the entire server/container with a new one built from a fresh image.
*   **Benefit:** Eliminates configuration drift (Snowflake servers).
*   **Tool:** Docker, VM Images (AMI).

---

## 872. What is ephemeral environment?

**Answer:**
An **Ephemeral Environment** (Preview Environment) is a temporary, on-demand environment created for a specific branch or Pull Request.
*   **Usage:** Created automatically when a PR is opened. Used for testing/QA. Destroyed when the PR is merged.
*   **Benefit:** Allows parallel testing without blocking Staging/Dev environments.

---

## 873. What is build optimization?

**Answer:**
Techniques to speed up CI build times.
1.  **Caching:** Cache dependencies (Maven/Gradle) and Docker layers.
2.  **Parallelization:** Run independent tests in parallel.
3.  **Incremental Builds:** Only build what changed (Gradle does this well).
4.  **Multi-Stage Builds:** Use smaller runtime images (Docker) to speed up pushing/pulling.

---

## 874. What is deployment automation?

**Answer:**
**Deployment Automation** allows deploying software to environments (Test/Prod) with a single click or commit, without manual intervention.
*   **Benefits:**
    *   **Repeatability:** Eliminates human error.
    *   **Speed:** Deploys take minutes, not hours.
    *   **Auditability:** Who deployed what and when is logged.

---

## 875. What is observability stack?

**Answer:**
The set of tools used to collect and analyze telemetry data.
*   **Common Stack (LGTM):**
    *   **L**ogs: Loki / Elasticsearch.
    *   **G**rafana: Visualization.
    *   **T**racing: Tempo / Jaeger.
    *   **M**etrics: Prometheus / Mimir.

---

## 876. What is log retention policy?

**Answer:**
Defines how long logs are kept and where.
*   **Hot Storage (7-30 days):** Fast access (Elasticsearch/Splunk) for debugging recent issues. Expensive.
*   **Cold Storage (1-7 years):** Slow access (S3/Glacier) for compliance/audit. Cheap.
*   **Policy:** Delete DEBUG logs after 3 days; Keep ERROR logs for 1 year.

---

## 877. What is alert fatigue?

**Answer:**
**Alert Fatigue** occurs when engineers become desensitized to frequent, non-actionable alerts (false positives).
*   **Consequence:** Critical alerts are ignored or missed.
*   **Fix:**
    *   Delete flaky alerts.
    *   Make alerts actionable (Runbook link).
    *   Group related alerts.
    *   Only page on symptoms that affect users (SLO burn).

---

## 878. What is CI/CD security?

**Answer:**
Securing the pipeline itself.
1.  **Secret Injection:** Don't store secrets in the repo.
2.  **Signed Commits:** Verify who wrote the code.
3.  **Runner Security:** Don't run builds on Production servers. Use ephemeral runners.
4.  **Artifact Signing:** Sign Docker images (Cosign) to ensure integrity.

---

## 879. What is supply chain attack?

**Answer:**
An attack that targets the software dependencies or build process to inject malicious code into the final application.
*   **Example:** **SolarWinds**, **Log4Shell**.
*   **Prevention:** SBOM (Software Bill of Materials), Dependency Scanning, Pinning versions.

---

## 880. What is platform engineering?

**Answer:**
**Platform Engineering** is the discipline of designing and building toolchains and workflows ("Internal Developer Platform") that enable self-service capabilities for software engineering organizations.
*   **Goal:** Reduce cognitive load on developers (Golden Paths).
*   **Example:** Providing a "Create Service" template that sets up Repo, CI/CD, K8s manifest, and Monitoring automatically.
