
## 781. What is Spring Security?

**Answer:**
**Spring Security** is a powerful and highly customizable authentication and access-control framework for Java applications.
*   **Key Features:**
    *   **Authentication:** Verifying identity (Login).
    *   **Authorization:** Verifying permissions (Roles/Authority).
    *   **Protection:** Against common attacks (CSRF, Session Fixation).
*   **Core:** Based on Servlet Filters (FilterChain).

---

## 782. What is authentication vs authorization?

**Answer:**
*   **Authentication (AuthN):** "Who are you?"
    *   Verifying the identity of a user (e.g., Login with Username/Password, OTP, Bio-metrics).
    *   *Examples:* 401 Unauthorized.
*   **Authorization (AuthZ):** "What are you allowed to do?"
    *   Verifying if the authenticated user has permission to access a resource.
    *   *Examples:* 403 Forbidden (Admin vs User roles).

---

## 783. What is JWT?

**Answer:**
**JWT (JSON Web Token)** is a compact URL-safe means of representing claims to be transferred between two parties.
*   **Structure:**
    *   **Header:** Algo type (HS256).
    *   **Payload:** Data (User ID, Role, Expiry).
    *   **Signature:** Hash of Header + Payload + Secret Key.
*   **Stateless:** Server doesn't store session; validates token signature.

---

## 784. What is OAuth2?

**Answer:**
**OAuth 2.0** is an industry-standard protocol for **Authorization**.
*   **Goal:** Allow a third-party application to access user data on another service (e.g., Google, Facebook) **without sharing the password**.
*   **Roles:**
    1.  **Resource Owner:** User.
    2.  **Client:** The App trying to access data.
    3.  **Authorization Server:** Google/FB (issues tokens).
    4.  **Resource Server:** API hosting the data.

---

## 785. What is OpenID Connect?

**Answer:**
**OpenID Connect (OIDC)** is an identity layer built **on top of OAuth 2.0**.
*   **Goal:** **Authentication**. (OAuth is for Authorization, OIDC adds Authentication).
*   **Mechanism:** It returns an  (JWT) along with the OAuth .
*   **Use Case:** "Sign in with Google".

---

## 786. What is CSRF?

**Answer:**
**CSRF (Cross-Site Request Forgery)** is an attack that forces an authenticated user to execute unwanted actions on a web application they are currently logged into.
*   **Scenario:** User logs into Bank A. User visits Malicious Site B. Site B sends a hidden form POST request to Bank A to transfer money. Bank A accepts it because User's session cookie is sent automatically.
*   **Prevention:** Synchronizer Token Pattern (CSRF Token) - a random token required for state-changing requests (POST/PUT/DELETE).

---

## 787. What is CORS?

**Answer:**
**CORS (Cross-Origin Resource Sharing)** is a browser security mechanism that restricts web pages from making requests to a different domain than the one that served the web page.
*   **Default:** Browsers block cross-origin AJAX requests (Same-Origin Policy).
*   **Server Config:** The server must explicitly allow the origin via headers:
    *
    *

---

## 788. What is XSS?

**Answer:**
**XSS (Cross-Site Scripting)** allows attackers to inject malicious scripts into web pages viewed by other users.
*   **Types:**
    *   **Stored XSS:** Script saved in DB (e.g., comment section) and shown to everyone.
    *   **Reflected XSS:** Script in URL query param, executed immediately.
*   **Impact:** Stealing session cookies (), redirecting users.
*   **Prevention:** Escaping/Sanitizing user input (e.g., converting  to ).

---

## 789. What is SQL Injection?

**Answer:**
**SQL Injection (SQLi)** occurs when an attacker interferes with the queries an application makes to its database.
*   **Mechanism:** Injecting malicious SQL code via input fields.
*   **Example:** Inputting  in a login field might bypass authentication:
    (Always True).

---

## 790. How to prevent SQL injection?

**Answer:**
1.  **Prepared Statements (Parameterized Queries):** The DB treats input as data, not executable code. (Best Defense).
    *   *Java:*  or JPA/Hibernate (uses parameters by default).
2.  **Input Validation:** Whitelist allowed characters.
3.  **Least Privilege:** DB user should have limited permissions.
4.  **ORM:** Use Hibernate/JPA which handles escaping automatically.

---

## 791. What is password hashing?

**Answer:**
**Password Hashing** is the process of converting a plain-text password into a fixed-length string of characters (hash) using a mathematical algorithm.
*   **One-way:** You cannot convert the hash back to the password.
*   **Purpose:** Protect user passwords if the database is compromised.
*   **Salting:** Adding random data to the password before hashing to prevent **Rainbow Table** attacks.

---

## 792. What is bcrypt?

**Answer:**
**BCrypt** is a popular password hashing function designed to be **slow**.
*   **Adaptive:** You can configure the "work factor" (cost) to make it slower as computers get faster.
*   **Why Slow?** To make Brute-Force and Dictionary attacks computationally expensive.
*   **Format:** Integrating the salt and hash in the output string .

---

## 793. What is role-based access control?

**Answer:**
**RBAC (Role-Based Access Control)** restricts network access based on the roles of individual users within an enterprise.
*   **Concept:**
    *   **User:** Assigned one or more Roles (e.g., , ).
    *   **Permission:** Assigned to Roles (e.g., , ).
    *   **Access:** Granted if the User has the required Role.

---

## 794. What is method-level security?

**Answer:**
**Method-Level Security** protects individual service layer methods (Java functions) rather than just HTTP endpoints.
*   **Spring Security:** Enabled via .
*   **Annotations:**
    *   : Check before method execution.
    *   : Check after method execution (can access return value).
    *   : Legacy annotation for simple role checks.

---

## 795. What is @PreAuthorize?

**Answer:**
is a Spring Security annotation that uses **SpEL (Spring Expression Language)** to enforce access control before a method is entered.
*   **Example:**

*   **Power:** Allows complex logic (e.g., checking if the user owns the data).

---

## 796. What is security filter chain?

**Answer:**
The **Security Filter Chain** is the heart of Spring Security's web infrastructure.
*   **Mechanism:** When a request comes in, it passes through a chain of Servlet Filters.
*   **Filters:**
    1.  : Loads user details.
    2.  : Handles form login.
    3.  : Handles Basic Auth.
    4.  : Final check for authorization.

---

## 797. What is stateless authentication?

**Answer:**
**Stateless Authentication** means the server does **not** keep a record of logged-in users (no Session ID in memory).
*   **Mechanism:** Every request must contain all necessary info to identify the user (usually a **Token** like JWT).
*   **Scalability:** High, as any server in a cluster can handle the request without needing shared session storage.

---

## 798. What is session fixation?

**Answer:**
**Session Fixation** is an attack where the attacker tricks a user into authenticating with a Session ID known to the attacker.
*   **Attack:** Attacker sends a link with . User logs in. Attacker uses  to hijack the session.
*   **Prevention:** **Migrate Session** on login (Spring Security does this by default: creates a new Session ID upon successful authentication).

---

## 799. What is brute-force protection?

**Answer:**
**Brute-Force Protection** prevents attackers from guessing passwords by trying millions of combinations.
*   **Mechanisms:**
    1.  **Account Lockout:** Lock account after 5 failed attempts.
    2.  **Delay (Throttling):** Introduce a delay after each failed attempt.
    3.  **CAPTCHA:** Verify the user is human.
    4.  **2FA:** Require a second factor.

---

## 800. What is rate limiting?

**Answer:**
**Rate Limiting** controls the number of requests a user/client can make to an API within a given time frame.
*   **Purpose:** Prevent DoS (Denial of Service) attacks and ensure fair usage.
*   **Algorithms:** Token Bucket, Leaky Bucket, Fixed Window.
*   **Tools:** Bucket4j, Redis, API Gateways (Kong, AWS API Gateway).
*   **Response:** .

---

## 801. What is encryption vs hashing?

**Answer:**
*   **Encryption:** Two-way function. Converts data into ciphertext using a key. Can be decrypted back to original text with the correct key.
    *   *Goal:* Confidentiality (e.g., encrypting credit card numbers).
*   **Hashing:** One-way function. Converts data into a fixed-size string (digest). Cannot be reversed.
    *   *Goal:* Integrity/Verification (e.g., password storage).

---

## 802. What is symmetric vs asymmetric encryption?

**Answer:**
*   **Symmetric:** Uses the **SAME key** for both encryption and decryption.
    *   *Pros:* Fast.
    *   *Cons:* Key distribution is risky (how to share the key securely?).
    *   *Algo:* AES, DES.
*   **Asymmetric:** Uses a **Key Pair** (Public Key and Private Key).
    *   *Mechanism:* Encrypt with Public Key -> Decrypt with Private Key.
    *   *Pros:* Secure key exchange.
    *   *Cons:* Slow.
    *   *Algo:* RSA, ECC.

---

## 803. What is TLS?

**Answer:**
**TLS (Transport Layer Security)** is a cryptographic protocol designed to provide secure communication over a network (replacement for SSL).
*   **Features:**
    1.  **Encryption:** Hides data from eavesdroppers.
    2.  **Authentication:** Ensures you are talking to the right server.
    3.  **Integrity:** Ensures data hasn't been tampered with.

---

## 804. What is HTTPS handshake?

**Answer:**
The **HTTPS Handshake** establishes a secure connection between Client and Server.
1.  **Client Hello:** Sends supported crypto algorithms and TLS version.
2.  **Server Hello:** Selects algorithm and sends its **Certificate** (Public Key).
3.  **Verification:** Client validates the Certificate with a CA (Certificate Authority).
4.  **Key Exchange:** Client generates a session key, encrypts it with Server's Public Key, and sends it.
5.  **Finished:** Both parties switch to encrypted communication using the session key (Symmetric).

---

## 805. What is certificate?

**Answer:**
A **Digital Certificate** is an electronic credential that binds a Public Key to an identity (domain name, organization).
*   **Issued By:** A trusted Certificate Authority (CA) like DigiCert, Let's Encrypt.
*   **Contains:** Domain Name, Expiration Date, Public Key, CA Signature.

---

## 806. What is key rotation?

**Answer:**
**Key Rotation** is the practice of replacing cryptographic keys (API keys, DB credentials, Encryption keys) on a regular schedule.
*   **Purpose:**
    1.  Limits the amount of data encrypted with a single key (crypto-period).
    2.  Reduces the impact if a key is compromised (attacker only gets access to a slice of data/time).

---

## 807. What is secret management?

**Answer:**
**Secret Management** involves storing sensitive data (passwords, API keys, certificates) securely, away from source code / config files.
*   **Bad Practice:** Hardcoding secrets in git.
*   **Best Practice:** Use tools like **HashiCorp Vault**, **AWS Secrets Manager**, or K8s Secrets.
    *   Encrypts secrets at rest.
    *   Controls access via policies.
    *   Audits who accessed what.

---

## 808. What is zero trust?

**Answer:**
**Zero Trust** is a security model that assumes **no trust**, even for users/devices inside the network perimeter.
*   **Motto:** "Never trust, always verify."
*   **Principles:**
    1.  Verify explicitly (AuthN/AuthZ for every request).
    2.  Least Privilege Access.
    3.  Assume Breach (Segment networks).

---

## 809. What is SSO?

**Answer:**
**SSO (Single Sign-On)** allows a user to log in once and gain access to multiple independent applications without re-entering credentials.
*   **Protocol:** Often uses **SAML** (XML-based) or **OIDC** (JSON-based).
*   **Flow:** User visits App A -> Redirected to Identity Provider (IdP) -> Logs in -> IdP sends token back to App A -> User visits App B -> App B trusts IdP token -> Logs in automatically.

---

## 810. What is multi-factor authentication?

**Answer:**
**MFA (Multi-Factor Authentication)** requires two or more pieces of evidence to verify identity.
*   **Factors:**
    1.  **Something you know:** Password, PIN.
    2.  **Something you have:** Phone (SMS/OTP Code), Hardware Key (YubiKey).
    3.  **Something you are:** Fingerprint, FaceID.
*   **Security:** Significantly reduces the risk of account takeover even if the password is stolen.

---

## 811. What is OAuth2 flow types?

**Answer:**
**Grant Types** determine how the client gets the Access Token.
1.  **Authorization Code Flow:** (Best for Web Apps) Redirects user to IdP login page. Returns code -> exchange for token.
2.  **Client Credentials Flow:** (Server-to-Server) No user involved. App uses ID/Secret to get token.
3.  **Implicit Flow:** (Deprecated) Returns token directly in URL. Unsecure.
4.  **Password Grant:** (Deprecated) App sends username/password directly.

---

## 812. What is refresh token?

**Answer:**
A **Refresh Token** is a special token used to obtain a new Access Token without requiring the user to log in again.
*   **Life Cycle:**
    1.  Access Token expires (short-lived, e.g., 15 mins).
    2.  Client sends Refresh Token (long-lived, e.g., 7 days) to Auth Server.
    3.  Auth Server validates and issues new Access Token + new Refresh Token (Refresh Token Rotation).

---

## 813. What is access token expiry strategy?

**Answer:**
**Short-lived Access Tokens** reduce the window of attack if stolen.
*   **Strategy:**
    *   **Access Token:** 5-15 minutes.
    *   **Refresh Token:** Days or Weeks.
    *   **Hard Expiry:** Force re-login after X days regardless of activity.
    *   **Idle Expiry:** Force re-login if inactive for X minutes.

---

## 814. What is API key security?

**Answer:**
**API Keys** are long-lived credentials used to identify a client application.
*   **Risks:** Often checked into code (leakage).
*   **Best Practices:**
    1.  **Rotation:** Rotate keys periodically.
    2.  **Scope:** Restrict what endpoints the key can access (Least Privilege).
    3.  **Usage Limits:** Rate limit per key to prevent abuse.
    4.  **Storage:** Store in Env Variables or Vault, never in code.

---

## 815. What is token revocation?

**Answer:**
**Token Revocation** is the process of invalidating a token before its expiry.
*   **Challenge:** JWTs are stateless; server doesn't know they exist.
*   **Solutions:**
    1.  **Blacklist:** Store revoked JWT IDs (jti) in Redis with TTL = JWT expiry.
    2.  **Short TTL:** Just wait for it to expire (5 mins).
    3.  **Reference Tokens:** Use opaque tokens instead of JWT (requires DB lookup on every request, allowing instant revocation).

---

## 816. What is HMAC?

**Answer:**
**HMAC (Hash-Based Message Authentication Code)** ensures both **Integrity** and **Authenticity**.
*   **Mechanism:** Hash(Message + Secret Key).
*   **Usage:**
    *   Verifying JWT signatures (HS256).
    *   Verifying Webhook payloads (Provider signs payload with shared secret; receiver verifies).

---

## 817. What is digital signature?

**Answer:**
A **Digital Signature** guarantees the authenticity of a document/message using **Asymmetric Encryption**.
*   **Process:**
    1.  Sender hashes the message.
    2.  Sender encrypts the hash with their **Private Key** (Signature).
    3.  Receiver decrypts the signature with Sender's **Public Key**.
    4.  Receiver compares the decrypted hash with their own hash of the message.
*   **Verification:** If they match, the message came from the Sender and wasn't changed.

---

## 818. What is OWASP Top 10?

**Answer:**
The **OWASP Top 10** is a standard awareness document for developers and web application security. It lists the most critical security risks.
*   **Examples:**
    1.  Broken Access Control.
    2.  Cryptographic Failures.
    3.  Injection (SQLi, etc.).
    4.  Insecure Design.
    5.  Security Misconfiguration.

---

## 819. What is dependency vulnerability scanning?

**Answer:**
Checks third-party libraries (Maven/Gradle dependencies) for known security vulnerabilities (CVEs).
*   **Tool:** **OWASP Dependency Check**, **Snyk**, **GitHub Dependabot**.
*   **Action:** If `log4j` version 2.14 is found (vulnerable), the build fails and suggests upgrading to 2.17.

---

## 820. What is secure coding practices?

**Answer:**
Guidelines to prevent security flaws during development.
1.  **Input Validation:** Never trust user input. Verify length, type, format.
2.  **Output Encoding:** Prevent XSS.
3.  **Error Handling:** Don't expose stack traces to users.
4.  **Logging:** Don't log PII (Personally Identifiable Information) or passwords.
5.  **Principle of Least Privilege:** Run apps with minimum required permissions.

---

## 821. What is CSP?

**Answer:**
**CSP (Content Security Policy)** is an HTTP response header that allows site administrators to declare approved sources of content that browsers are allowed to load.
*   **Goal:** Mitigate XSS and Data Injection attacks.
*   **Example:**  (Only allow scripts from own domain and trusted-scripts.com).

---

## 822. What is clickjacking?

**Answer:**
**Clickjacking** (UI Redressing) is a malicious technique where an attacker tricks a user into clicking on something different from what the user perceives.
*   **Mechanism:** Embedding the target service inside an invisible  overlaid on a decoy website.
*   **Prevention:**  or  header (prevents the site from being rendered in a frame).

---

## 823. What is SSRF?

**Answer:**
**SSRF (Server-Side Request Forgery)** occurs when an attacker can induce the server to make requests to an unintended location.
*   **Scenario:** Attacker sends a URL to the server (e.g., ). If the server fetches it blindly, the attacker can access internal services behind the firewall.
*   **Prevention:** Whitelist allowed domains/IPs; disable fetching from internal IPs (127.0.0.1, 10.x.x.x).

---

## 824. What is IDOR?

**Answer:**
**IDOR (Insecure Direct Object References)** occurs when an application exposes a reference to an internal implementation object (like a database ID) to users without access control checks.
*   **Example:** . Attacker changes  to  and views another user's data.
*   **Prevention:** Implement proper Access Control checks () verifying if the logged-in user owns the requested resource ID.

---

## 825. What is data masking?

**Answer:**
**Data Masking** (Obfuscation) creates a structurally similar but fake version of data to protect sensitive information during non-production use (e.g., Testing, Training).
*   **Dynamic Masking:** Hiding data on-the-fly (e.g., showing  for credit cards).
*   **Static Masking:** Permanently replacing data in a database copy.

---

## 826. What is audit logging?

**Answer:**
**Audit Logging** involves recording a chronological trail of system activities to enable the reconstruction and examination of the sequence of environments and activities.
*   **What to Log:** WHO (User), DID WHAT (Action), WHEN (Timestamp), WHERE (IP/Resource), RESULT (Success/Failure).
*   **Purpose:** Forensics, Compliance, Troubleshooting.

---

## 827. What is intrusion detection?

**Answer:**
**IDS (Intrusion Detection System)** monitors network traffic for suspicious activity and issues alerts.
**IPS (Intrusion Prevention System)** also monitors but *takes action* to block the activity.
*   **Types:**
    *   **NIDS:** Network-based (analyzes packets).
    *   **HIDS:** Host-based (analyzes system calls/logs on a specific server).

---

## 828. What is WAF?

**Answer:**
**WAF (Web Application Firewall)** protects web applications by filtering and monitoring HTTP traffic between a web application and the Internet.
*   **Layer 7:** Operates at the Application Layer.
*   **Protects Against:** SQL Injection, XSS, DDoS, Cookie Poisoning.
*   **Example:** AWS WAF, Cloudflare.

---

## 829. What is cloud security best practice?

**Answer:**
1.  **Shared Responsibility Model:** Understand what you are responsible for (Data, App) vs Cloud Provider (Hardware, Network).
2.  **IAM:** Use Least Privilege. Rotate keys. Use MFA.
3.  **Encryption:** Encrypt data at Rest (S3/EBS encryption) and in Transit (TLS).
4.  **Logging:** Enable CloudTrail/VPC Flow Logs.
5.  **Network:** Use Private Subnets for backend; limit Security Group rules.

---

## 830. What is compliance (GDPR, PCI)?

**Answer:**
*   **GDPR (General Data Protection Regulation):** EU law on data privacy.
    *   *Rights:* Right to be ignored (Deletion), Right to Access.
    *   *Requirement:* Consent for cookies/tracking.
*   **PCI-DSS (Payment Card Industry Data Security Standard):** For handling credit cards.
    *   *Requirement:* Encrypt transmission, never store CVV, restrict physical access.

---

## 831. How to secure microservices?

**Answer:**
**Microservices Security** requires a Defense-in-Depth approach (layers).
1.  **Gateway:** SSL/TLS termination, Rate Limiting, WAF (Edge Security).
2.  **AuthN/AuthZ:** Centralized Identity Provider (OAuth2/OIDC) passing JWTs to services.
3.  **Service-to-Service:** Mutual TLS (mTLS) for encrypted and authenticated internal communication (e.g., using Istio/Linkerd).
4.  **Network:** Private Subnets, Security Groups (Firewalls) restricting traffic.
5.  **Secrets:** Use Vault/Secrets Manager, don't hardcode.

---

## 832. How to secure REST APIs?

**Answer:**
1.  **HTTPS Everywhere:** Encrypt data in transit.
2.  **Authentication:** Use Standard Auth (Bearer Token/API Key).
3.  **Input Validation:** Sanitize all inputs to prevent Injection attacks.
4.  **Output Encoding:** Prevent XSS.
5.  **Rate Limiting:** Prevent Abuse/DoS.
6.  **CORS:** Restrict cross-origin access.
7.  **Error Handling:** Generic error messages (don't leak stack traces).

---

## 833. How to protect against DDoS?

**Answer:**
**DDoS (Distributed Denial of Service)** aims to overwhelm the system.
*   **Protection:**
    1.  **Edge Network:** Use a CDN (Cloudflare, AWS CloudFront) to absorb traffic.
    2.  **WAF:** Block malicious IPs and bot signatures.
    3.  **Auto-Scaling:** Scale out servers to handle the load spike.
    4.  **Rate Limiting:** Throttle requests per IP.
    5.  **Traffic Analysis:** Monitor for abnormal patterns (e.g., slowloris).

---

## 834. What is IAM policy design?

**Answer:**
**IAM (Identity and Access Management)** policies define permissions.
*   **Best Practices:**
    1.  **Least Privilege:** Grant *only* what is needed (e.g., allow  on , not ).
    2.  **Role-Based:** Assign permissions to Roles, not Users.
    3.  **Conditions:** Add conditions (e.g., allow access only from specific IP or time).
    4.  **Separation of Duties:** Devs shouldn't have delete permissions in Prod.

---

## 835. What is least privilege principle?

**Answer:**
The **Principle of Least Privilege (PoLP)** states that a subject (user/process) should be given only those privileges needed for it to complete its task.
*   **Example:** A  needs read access to the DB, but shouldn't have write/delete access.
*   **Benefit:** Minimizes the blast radius if the entity is compromised.

---

## 836. What is security testing lifecycle?

**Answer:**
Integrating security into every phase of SDLC (DevSecOps):
1.  **Design:** Threat Modeling.
2.  **Code:** Static Analysis (SAST), Pre-commit hooks (Secret scanning).
3.  **Build:** Dependency Scanning (SCA), Container Scanning.
4.  **Test:** Dynamic Analysis (DAST).
5.  **Deploy:** Infrastructure as Code (IaC) scanning.
6.  **Monitor:** Runtime Application Self-Protection (RASP), IDS.

---

## 837. What is vulnerability management?

**Answer:**
**Vulnerability Management** is the cyclical practice of identifying, classifying, remediating, and mitigating vulnerabilities.
*   **Cycle:** Scan -> prioritize (Critical/High) -> Patch/Update -> Rescan.
*   **SLA:** e.g., "Critical vulnerabilities must be patched within 24 hours".

---

## 838. What is threat modeling?

**Answer:**
**Threat Modeling** is a structured approach to identifying potential security threats and vulnerabilities **during the design phase**.
*   **Steps:**
    1.  Decompose the application (Data Flow Diagrams).
    2.  Identify threats (STRIDE model: Spoofing, Tampering, Repudiation, Information Disclosure, DoS, Elevation of Privilege).
    3.  Determine mitigations.

---

## 839. What is risk assessment?

**Answer:**
**Risk Assessment** evaluates the potential impact of a threat vs the likelihood of it occurring.
*   **Formula:**
*   **Outcome:** Prioritized list of risks to address (e.g., High Risk: SQL Injection in Login; Low Risk: Info disclosure in debug logs).

---

## 840. Real production security incident handled?

**Answer:**
*(Behavioral Question - Example Format)*
"In a previous project, we detected a **Credential Stuffing** attack on our login API.
1.  **Detection:** Monitoring showed a 500% spike in failed login attempts from varied IPs.
2.  **Containment:** We immediately enabled **IP Throttling** on the WAF and temporarily blocked the aggressive subnets.
3.  **Mitigation:** We forced a password reset for affected users and implemented **reCAPTCHA** on the login page.
4.  **Post-Mortem:** We updated our alerting thresholds and expedited the MFA rollout."
