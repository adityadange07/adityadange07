
## 961. Describe challenging production issue you handled.

**Answer:**
**S.T.A.R Method:**
*   **Situation:** During Black Friday sale, Checkout Service latency
    spiked to 10s.
*   **Task:** Identify the bottleneck and restore normal operations.
*   **Action:**
    1.  Checked metrics (Datadog) and found DB CPU at 100%.
    2.  Found a slow query (Missing Index on `order_date`).
    3.  Applied hotfix (Added Index).
*   **Result:** Latency dropped to 200ms. Sales resumed.

---

## 962. How do you handle tight deadlines?

**Answer:**
1.  **Prioritize:** Identify MVP (Must-Have vs Nice-to-Have).
2.  **Communicate:** Inform stakeholders early if scope needs cutting.
3.  **De-risk:** Tackle hardest parts first.
4.  **negotiate:** Can we trade scope for time?
5.  **Focus:** Minimize distractions/meetings.

---

## 963. How do you mentor juniors?

**Answer:**
1.  **Pair Programming:** Code together to share context and shortcuts.
2.  **Code Reviews:** Focus on logic/design, not just syntax. Explain "Why", not just "What".
3.  **Design Docs:** Ask them to write a design doc for small features.
4.  **Autonomy:** Let them own a task, but be available for questions.

---

## 964. How do you review code?

**Answer:**
1.  **Correctness:** Does it do what it's supposed to?
2.  **Tests:** Are there unit/integration tests covering edge cases?
3.  **Readability:** Is variable naming clear? Is logic simple?
4.  **Security:** SQL Injection? exposed secrets?
5.  **Performance:** loop inside loop? N+1 query?

---

## 965. How do you handle conflict in team?

**Answer:**
1.  **Listen:** Understand the other person's perspective.
2.  **Data-Driven:** Use metrics/facts rather than opinions (e.g., "A/B test results showed X").
3.  **Common Goal:** Remind everyone we want the best product for the user.
4.  **Compromise:** Find a middle ground (e.g., "Let's try your approach for this smaller module first").

---

## 966. How do you design scalable solution?

**Answer:**
1.  **Requirements:** Clarify DAU, QPS, Latency goals.
2.  **High Level:** Diagram services (Microservices vs Monolith).
3.  **Data Layer:** SQL vs NoSQL. Sharding? Replication?
4.  **Caching:** Redis/CDN usage.
5.  **Async:** Queues for decoupling.
6.  **Failure Modes:** What happens if DB goes down? (Circuit Breaker).

---

## 967. How do you estimate tasks?

**Answer:**
1.  **Break Down:** Split large stories into small tasks (< 1 day).
2.  **Complexity:** Use T-Shirt sizing (S, M, L) or Fibonacci points.
3.  **Buffer:** Add 20% buffer for unknowns/testing/meetings.
4.  **Comparison:** "This is similar to Feature X which took 3 days."

---

## 968. How do you handle requirement changes?

**Answer:**
1.  **Assess Impact:** How does this affect the deadline/architecture?
2.  **Communicated:** Discuss trade-offs with Product Manager (e.g., "If we add X, we must drop Y or push date").
3.  **Adapt:** Agile mindset. Embrace change but manage scope creep.

---

## 969. How do you improve code quality?

**Answer:**
1.  **CI/CD:** Automate linting (SonarQube) and testing.
2.  **Reviews:** Strict code review process.
3.  **Refactoring:** Allocate 20% time for tech debt.
4.  **Standards:** Agree on coding conventions (Google Java Style).
5.  **Testing:** Enforce min 80% coverage.

---

## 970. How do you ensure high availability?

**Answer:**
1.  **Redundancy:** Multiple instances of service across Availability Zones (AZ).
2.  **Load Balancing:** Distribute traffic.
3.  **Failover:** Active-Passive DB setup.
4.  **Monitoring:** Alerts for downtime.
5.  **Chaos Testing:** Proactively kill nodes to test recovery.

---

## 971. How do you handle on-call incident?

**Answer:**
**Process:**
1.  **Acknowledge:** Confirm receipt of alert (PagerDuty/OpsGenie).
2.  **Triage:** Assess severity (Sev1 vs Sev3). Is it affecting customers?
3.  **Mitigate:** Focus on restoring service first (Restart, Rollback, Switch Region) rather than fixing the root cause immediately.
4.  **Communicate:** Update Status Page or stakeholders.
5.  **Post-Mortem:** Analyze root cause and add prevention measures (5 Whys).

---

## 972. How do you prioritize bugs?

**Answer:**
**Matrix: Severity (Impact) vs Probability (Frequency).**
1.  **Critical (P0):** Data loss, Security breach, System down. Fix Immediately.
2.  **High (P1):** Major feature broken, no workaround. Fix in current sprint.
3.  **Medium (P2):** Annoying UI glitch, workaround exists. Backlog.
4.  **Low (P3):** Typos. "Nice to fix".

---

## 973. How do you reduce technical debt?

**Answer:**
1.  **Visibility:** Track debt in specific tickets in JIRA.
2.  **Boy Scout Rule:** "Leave the code cleaner than you found it." Refactor small things while working on features.
3.  **Dedicated Time:** Allocate 20% of sprint capacity to Engineering tasks.
4.  **Definition of Done:** Include "Refactoring / Tests" in DoD.

---

## 974. How do you communicate architecture?

**Answer:**
1.  **C4 Model:** Context, Containers, Components, Code (Zoom in/out levels).
2.  **ADRs (Architecture Decision Records):** Document `Why` a decision was made (Context, Decision, Consequences).
3.  **Whiteboarding:** Draw boxes and arrows to explain data flow to the team.

---

## 975. How do you handle cross-team dependency?

**Answer:**
1.  **Contract First:** Define API specs (OpenAPI/Swagger) before coding.
2.  **Mocking:** Use mocks/stubs to develop in parallel without waiting for the other team.
3.  **Establish SLIs/SLOs:** Agree on expected latency/uptime.
4.  **Regular Sync:** Weekly check-ins to flag blockers early.

---

## 976. How do you introduce new technology?

**Answer:**
1.  **Problem First:** Ensure it solves a real problem, not just "Resume Driven Development".
2.  **POC (Proof of Concept):** Build a small prototype to validate.
3.  **Trade-off Analysis:** Cost vs Benefit, Learning curve, Maintenance.
4.  **Team Buy-in:** Present findings to the team.
5.  **Migration Plan:** Incremental adoption.

---

## 977. How do you handle failure?

**Answer:**
**Example:** "I once deployed a change that caused a memory leak."
1.  **Own it:** Admitted the mistake immediately.
2.  **Fix it:** Rolled back the change.
3.  **Learn:** Wrote a blameless post-mortem.
4.  **Prevent:** Added a load test to the CI pipeline to catch leaks in the future.

---

## 978. What is your leadership style?

**Answer:**
**Servant Leadership:**
*   **Support:** Blocking distractions, removing obstacles for the team.
*   **Empowerment:** Giving developers ownership of their features.
*   **Empathy:** Understanding personal situations and burnout.
*   **Growth:** Focusing on team members' career progression.

---

## 979. How do you handle performance issue?

**Answer:**
**Systematic Approach:**
1.  **Baseline:** Measure current performance.
2.  **Profile:** Identify the bottleneck (CPU? I/O? DB? Network?).
3.  **Hypothesis:** "Adding cache will reduce load."
4.  **Experiments:** Apply fix in isolation.
5.  **Verify:** Measure again.
6.  **Monitor:** Set alerts to prevent regression.

---

## 980. How do you motivate team?

**Answer:**
**Dan Pink's Drive (AMP):**
1.  **Autonomy:** Let them allow *how* to solve the problem.
2.  **Mastery:** Give difficult/interesting challenges that help them grow.
3.  **Purpose:** Connect their work to the business impact ("This feature helps 1M users").
4.  **Recognition:** Publicly celebrate wins.

---

## 981. How do you handle production outage?

**Answer:**
**Incident Response:**
1.  **Assign Roles:** Incident Commander (Communicates), Ops Lead (Fixes).
2.  **Mitigate:** Focus on bringing service UP (even if degraded).
3.  **Communication:** Update status page every 30 mins.
4.  **Investigate:** Check logs, metrics, recent changes.
5.  **Review:** Conduct a Post-Incident Review (PIR) within 24 hours.

---

## 982. How do you document system?

**Answer:**
1.  **High-Level:** Architecture Diagrams (C4), Data Flow.
2.  **Low-Level:** Swagger/OpenAPI for APIs.
3.  **Operational:** Runbooks for on-call (How to restart, How to rollback).
4.  **Decisions:** ADRs (Architecture Decision Records).
5.  **Onboarding:** `README.md` in every repo with "How to run locally".

---

## 983. How do you handle disagreement on design?

**Answer:**
1.  **Standardize:** Do we have existing patterns?
2.  **Pros/Cons:** List trade-offs (Complexity vs Performance).
3.  **POC:** "Let's code both quick prototypes and compare."
4.  **Disagree and Commit:** If consensus isn't reached, the Tech Lead decides, and everyone supports it.

---

## 984. How do you scale a system from 1k to 1M users?

**Answer:**
1.  **1k:** Monolith, Single DB.
2.  **10k:** Separate DB, Load Balancer, Caching (Redis).
3.  **100k:** CDN for static assets, Read Replicas for DB, Message Queues (Async).
4.  **1M:** Microservices, Sharding DB, Geolocation routing, Data Lake for analytics.

---

## 985. How do you ensure security compliance?

**Answer:**
1.  **Automated:** SAST/DAST tools in CI/CD pipeline.
2.  **Dependencies:** Snyk/Dependabot for vulnerable libraries.
3.  **Access:** Least Privilege Principle (IAM roles).
4.  **Audit:** Regular penetration testing (PenTest) by external firms.
5.  **Data:** Encrypt at REST and in Transit (TLS 1.3).

---

## 986. How do you handle customer escalation?

**Answer:**
1.  **Empathize:** Acknowledge the frustration.
2.  **Prioritize:** Is this an edge case or affecting many users?
3.  **Transparency:** "We found the issue and are working on it. ETA 2 hours."
4.  **Root Cause:** Fix the process so it doesn't happen again.

---

## 987. How do you conduct root cause analysis?

**Answer:**
**5 Whys Technique:**
*   **Problem:** The DB crashed.
1.  **Why?** ran out of connection.
2.  **Why?** Connection pool wasn't releasing connections.
3.  **Why?** Code exception didn't close connection in `finally` block.
4.  **Why?** Developer forgot.
5.  **Why?** No code review or linter checked for resource leaks.
*   **Root Cause:** Process failure (missing linter rules).

---

## 988. How do you measure team productivity?

**Answer:**
**DORA Metrics (DevOps Research and Assessment):**
1.  **Deployment Frequency:** How often we ship.
2.  **Lead Time for Changes:** Commit to Production time.
3.  **Change Failure Rate:** % of deployments causing failure.
4.  **Time to Restore Service:** How fast we recover.
*   *Avoid:* Lines of code (LOC) or Hours worked.

---

## 989. How do you improve deployment frequency?

**Answer:**
1.  **Small Batches:** Merge small changes often (Trunk-based).
2.  **Automated Testing:** Trust the test suite (Unit > Integration > E2E).
3.  **Feature Flags:** Deploy code that is "off" by default.
4.  **CI/CD Optimization:** Parallelize builds to reducing waiting time.

---

## 990. How do you reduce downtime?

**Answer:**
1.  **Blue-Green Deployment:** Switch traffic only when new version is healthy.
2.  **Canary Release:** Roll out to 1% of users first.
3.  **Auto-Healing:** Kubernetes restarts crashed pods automatically.
4.  **Circuit Breakers:** Fail fast instead of cascading failure.

---

## 991. How do you plan migration project?

**Answer:**
**Strategies:**
1.  **Dual Write:** Write to both Old and New systems.
2.  **Backfill:** Copy historical data.
3.  **Verification:** Compare data consistency between both.
4.  **Shadow Traffic:** Route traffic to new system but discard response (to test load).
5.  **Canary:** Switch 1% users.
6.  **Cutover:** Switch 100%.

---

## 992. How do you ensure observability?

**Answer:**
**Three Pillars:**
1.  **Logs (ELK/Splunk):** "What happened?" (Error details).
2.  **Metrics (Prometheus/Grafana):** "What is the trend?" (CPU, Request Count, Latency).
3.  **Tracing (Jaeger/Zipkin):** "Where did it happen?" (Distributed transaction flow).
*   **Alerting:** PagerDuty for critical thresholds.

---

## 993. How do you build resilient system?

**Answer:**
1.  **Circuit Breaker:** Stop calling failing service throughout.
2.  **Bulkhead:** Isolate resources so one failure doesn't crash everything (e.g., separate thread pools).
3.  **Retry with Backoff:** Exponential backoff for transient errors.
4.  **Fallback:** Return default value/cache if service fails.
5.  **Rate Limiting:** Protect against traffic spikes.

---

## 994. How do you conduct technical interviews?

**Answer:**
1.  **Coding:** Focus on logic and clean code, not obscure algorithms.
2.  **System Design:** Evaluate thinking process on scalability and trade-offs.
3.  **Behavioral:** Assess culture fit and past experiences (STAR method).
4.  **Scenario:** "What would you do if..." (Debugging/Production outage).

---

## 995. How do you evaluate architecture trade-offs?

**Answer:**
1.  **CAP Theorem:** Consistency vs Availability.
2.  **Complexity vs Maintainability:** Is Microservices worth the ops overhead vs Monolith?
3.  **Cost vs Performance:** Is AWS Lambda cheaper than EC2 for this workload?
4.  **Build vs Buy:** Do we need custom solution or use SaaS (Auth0)?

---

## 996. How do you balance speed vs quality?

**Answer:**
1.  **MVP:** Build minimum viable feature first.
2.  **Tech Debt Management:** Accumulate debt intentionally for speed, pay it back later.
3.  **Automation:** CI/CD and Tests ensure speed doesn't break quality.
4.  **Good Enough:** Don't optimized prematurely.

---

## 997. How do you handle legacy system modernization?

**Answer:**
1.  **Anti-Corruption Layer (ACL):** Adapter between New and Old system.
2.  **Strangler Fig:** Replace piece by piece.
3.  **CDC (Change Data Capture):** Sync data from Old DB to New DB (Debezium).
4.  **Documentation:** Understand existing business rules before rewriting.

---

## 998. What is your biggest technical achievement?

**Answer:**
**(Personalize this answer using STAR):**
"I led the migration of our monolith to microservices (Task), solving the scalability bottleneck (Situation). I designed the event-driven architecture using Kafka (Action), which reduced latency by 40% and enabled handling 5x traffic (Result)."

---

## 999. What is biggest production failure and learning?

**Answer:**
**(Personalize this answer):**
"Accidentally deleted a prod table (Situation). Restored from backup which took 4 hours (Action). Learned to automate backups and remove write access for developers in prod (Result). Implemented a 'terraform plan' review process to prevent infrastructure deletion."

---

## 1000. Why should we hire you as Senior Developer?

**Answer:**
1.  **Technical Depth:** Strong Java/Spring/Cloud skills.
2.  **Problem Solving:** Proven track record of fixing complex production issues.
3.  **Leadership:** Mentored juniors and improved team velocity.
4.  **Ownership:** I care about the product, not just code.
5.  **Communication:** Can bridge gap between Tech and Business.
