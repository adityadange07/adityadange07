Here you go, Aditya — a **complete list of the Top 100 AWS Interview Questions** for someone with **3–5 years of experience** in cloud and backend development. This set covers **core AWS services, architecture, security, deployment, scalability, monitoring, and DevOps integrations** — ideal for **developer, SDE, DevOps, or cloud engineer roles**.

---

## ✅ Top 100 AWS Interview Questions
**[Grouped by Topics – EC2, S3, VPC, Lambda, IAM, RDS, DevOps, Security, Design, etc.]**

---

# 🔹 1–15: **AWS Fundamentals**

## 1. What is AWS and what are its key benefits?

AWS, or Amazon Web Services, is a comprehensive cloud computing platform provided by Amazon. It offers a wide range of services, including computing power, storage, databases, machine learning, analytics, and more, all delivered over the internet. Businesses and individuals use AWS to build, deploy, and manage applications and services without needing to invest heavily in physical hardware or infrastructure.

### Key Benefits of AWS:
1. **Scalability**: AWS allows users to scale resources up or down based on demand. You only pay for what you use, making it flexible for startups, enterprises, or seasonal workloads.
2. **Cost-Effectiveness**: With a pay-as-you-go pricing model, AWS eliminates the need for large upfront investments in hardware. It also reduces maintenance costs since AWS manages the infrastructure.
3. **Global Reach**: AWS has data centers (regions and availability zones) worldwide, enabling low-latency access and data redundancy across geographies.
4. **Wide Range of Services**: From basic storage (like Amazon S3) to advanced AI tools (like SageMaker), AWS provides solutions for virtually every tech need.
5. **Reliability**: AWS offers high availability and fault tolerance through its distributed infrastructure, ensuring minimal downtime.
6. **Security**: AWS provides robust security features, including encryption, identity management, and compliance with industry standards, helping users protect their data.
7. **Speed and Agility**: Developers can quickly deploy applications, experiment with new ideas, and iterate faster without hardware procurement delays.
8. **Ecosystem and Community**: AWS integrates with a vast ecosystem of tools and has a large community, offering extensive support, documentation, and third-party solutions.

In short, AWS empowers businesses to innovate quickly, reduce costs, and operate globally with a reliable and secure cloud infrastructure.

---

## 2. What’s the difference between IaaS, PaaS, and SaaS in AWS?

In the context of AWS (and cloud computing in general), IaaS, PaaS, and SaaS represent different service models that define how much control and responsibility you have versus what AWS manages for you. Here’s how they break down:

### 1. **IaaS (Infrastructure as a Service)**
- **Definition**: AWS provides the foundational infrastructure—virtual machines, storage, and networking—that you can rent and manage. You’re responsible for the operating systems, applications, and data running on that infrastructure.
- **AWS Examples**:
    - **Amazon EC2 (Elastic Compute Cloud)**: Virtual servers for computing power.
    - **Amazon S3 (Simple Storage Service)**: Scalable object storage.
    - **Amazon VPC (Virtual Private Cloud)**: Isolated networking environments.
- **Key Characteristics**:
    - You control the OS, software, and configurations.
    - AWS handles the physical hardware, virtualization, and uptime.
- **Use Case**: Ideal for businesses needing full control over their systems (e.g., custom server setups or legacy app migrations).
- **Responsibility**: You manage apps, data, runtime, and OS; AWS manages the underlying infrastructure.

---

### 2. **PaaS (Platform as a Service)**
- **Definition**: AWS provides a platform that includes the infrastructure *and* the runtime environment (OS, middleware, etc.), so you can focus on developing, deploying, and managing applications without worrying about the underlying systems.
- **AWS Examples**:
    - **AWS Elastic Beanstalk**: Simplifies app deployment and scaling.
    - **AWS Lambda**: Serverless computing for running code without managing servers.
    - **Amazon RDS (Relational Database Service)**: Managed database services.
- **Key Characteristics**:
    - AWS manages the OS, runtime, and scaling; you focus on your app code and logic.
    - Faster setup since server management is abstracted away.
- **Use Case**: Great for developers building apps quickly (e.g., web apps or microservices) without handling server maintenance.
- **Responsibility**: You manage the application and data; AWS handles the platform, OS, and infrastructure.

---

### 3. **SaaS (Software as a Service)**
- **Definition**: AWS (or third-party providers hosted on AWS) delivers fully managed software applications over the internet. You simply use the software without worrying about infrastructure, platforms, or maintenance.
- **AWS Examples**:
    - **Amazon WorkMail**: Managed email and calendaring service.
    - **AWS Chime**: Video conferencing and chat service.
    - (Note: Many SaaS products on AWS Marketplace are third-party offerings running on AWS infrastructure.)
- **Key Characteristics**:
    - No setup or management required—just log in and use.
    - Subscription-based, fully hosted by the provider.
- **Use Case**: Perfect for end-users or businesses needing ready-to-use tools (e.g., email, CRM, or collaboration software).
- **Responsibility**: You manage your data and user access; AWS (or the SaaS provider) handles everything else.

---

### Key Differences in AWS Context:
| **Aspect**          | **IaaS**               | **PaaS**               | **SaaS**              |
|---------------------|------------------------|------------------------|-----------------------|
| **Control**         | High (you manage OS/apps) | Medium (you manage code) | Low (you just use it) |
| **AWS Management**  | Hardware, virtualization | Hardware, OS, runtime  | Entire stack          |
| **Flexibility**     | Very flexible          | Moderately flexible    | Limited to app features |
| **Examples**        | EC2, S3, VPC           | Elastic Beanstalk, Lambda | WorkMail, Chime       |
| **Who Uses It**     | Sysadmins, IT teams    | Developers             | End-users, businesses |

---

### AWS Spin:
AWS offers all three models, letting you mix and match based on your needs. For example, you could use EC2 (IaaS) for a custom server, Lambda (PaaS) for a serverless app, and WorkMail (SaaS) for email—all within the AWS ecosystem. The choice depends on how much control you want versus how much you’re willing to let AWS handle.

---

## 3. What regions and availability zones mean in AWS?

In AWS, **regions** and **availability zones (AZs)** are key concepts that define how its global infrastructure is organized. They help ensure scalability, reliability, and low-latency access to services. Here’s what they mean:

---

### **Regions**
- **Definition**: A region is a distinct geographic area where AWS has set up its data centers. Each region operates independently and is isolated from others to enhance fault tolerance and data sovereignty.
- **Key Points**:
    - Regions are named based on their location, e.g., **us-east-1** (Northern Virginia), **eu-west-1** (Ireland), or **ap-southeast-2** (Sydney).
    - As of April 2025, AWS has over 30 regions worldwide (and growing), each hosting a cluster of data centers.
    - Not all services are available in every region—some cutting-edge features might roll out in specific regions first (e.g., us-west-2).
    - You choose a region based on:
        - **Latency**: Proximity to your users.
        - **Compliance**: Local data residency laws (e.g., GDPR in Europe).
        - **Cost**: Pricing can vary slightly by region.
- **Example**: If your app serves European customers, you might deploy it in **eu-central-1** (Frankfurt) to minimize latency and comply with EU regulations.

---

### **Availability Zones (AZs)**
- **Definition**: An availability zone is an isolated location within a region, consisting of one or more data centers with independent power, cooling, and networking. AZs are designed to be insulated from failures in other AZs within the same region.
- **Key Points**:
    - Each region has multiple AZs (usually 2–6), identified with letters, e.g., **us-east-1a**, **us-east-1b**, etc.
    - AZs are physically separated (often by tens of miles) but connected with low-latency, high-bandwidth links.
    - They enable **high availability** and **fault tolerance**. If one AZ fails (e.g., due to a power outage), your app can failover to another AZ in the same region.
    - You can’t choose the exact physical AZ (like “data center X”); AWS maps them to your account uniquely for security (e.g., your **us-east-1a** might differ from another user’s).
- **Example**: In **us-west-2** (Oregon), there might be **us-west-2a**, **us-west-2b**, and **us-west-2c**. You could run your app’s servers across these AZs for redundancy.

---

### **How They Work Together**
- **Region**: The broader geographic container (e.g., **us-east-1**).
- **AZs**: The isolated units within that region (e.g., **us-east-1a**, **us-east-1b**).
- **Practical Use**:
    - Deploy resources (like EC2 instances or databases) across multiple AZs in a region for resilience.
    - Use multiple regions for global reach or disaster recovery (e.g., replicate data between **us-east-1** and **eu-west-1**).
- **Visual**: Think of a region as a “city” and AZs as “neighborhoods” with their own power grids—close enough to work together, but separate enough to avoid a single point of failure.

---

### **Why They Matter in AWS**
1. **Reliability**: Spreading workloads across AZs ensures your app stays online even if one data center fails.
2. **Performance**: Choosing a region close to your users reduces latency.
3. **Compliance**: Storing data in a specific region meets legal requirements.
4. **Cost Optimization**: Some regions/AZs might be cheaper, and staying within a region avoids cross-region data transfer fees.

For example, a web app might use **us-east-1** with EC2 instances in **us-east-1a** and **us-east-1b**, load-balanced via AWS Elastic Load Balancer, and store backups in **us-west-2** for disaster recovery. That’s the power of AWS’s region/AZ structure!

---

## 4. What is an AWS AMI?

An **AWS AMI** (Amazon Machine Image) is a pre-configured template used to create virtual machines (instances) in Amazon EC2 (Elastic Compute Cloud). Think of it as a blueprint or snapshot that contains everything needed to launch a fully functional server in the cloud—operating system, software, configurations, and sometimes even data.

---

### **What’s Inside an AMI?**
An AMI typically includes:
1. **Operating System**: E.g., Amazon Linux, Ubuntu, Windows Server, etc.
2. **Application Software**: Pre-installed tools or apps (e.g., a web server like Apache, a database like MySQL, or a custom app).
3. **Configuration Settings**: System settings, libraries, or dependencies tailored for a specific use case.
4. **Root Volume**: A template for the instance’s storage (e.g., an EBS-backed volume).

It’s essentially a packaged environment that lets you launch an EC2 instance without starting from scratch.

---

### **Types of AMIs**
1. **AWS-Provided AMIs**:
    - Official images from Amazon (e.g., Amazon Linux 2) or partners (e.g., Windows Server).
    - Optimized for AWS, often free or included with EC2 usage.
2. **Marketplace AMIs**:
    - Created by third-party vendors, available in the AWS Marketplace.
    - Often include specialized software (e.g., a pre-configured WordPress stack) and may have additional licensing costs.
3. **Community AMIs**:
    - Shared by other AWS users for free.
    - Useful for testing but require caution due to potential security risks.
4. **Custom AMIs**:
    - Built by you! Start with an existing AMI, customize it (install software, tweak settings), and save it as your own AMI.

---

### **How Does It Work?**
1. **Launch**: When you create an EC2 instance, you select an AMI from the AWS console, CLI, or SDK.
2. **Instantiation**: AWS uses the AMI to provision a virtual machine with the specified OS and software.
3. **Customization**: You can further tweak the instance after launch, or save a new AMI from it for reuse.

For example:
- Pick the **Ubuntu 20.04 AMI**, launch an EC2 instance, install Nginx, and you’ve got a web server running in minutes.
- Later, save that setup as a custom AMI to replicate it anytime.

---

### **Key Benefits**
1. **Speed**: Launch pre-configured instances instantly instead of manually setting up servers.
2. **Consistency**: Ensure every instance has the same software and settings, reducing errors in deployments.
3. **Reusability**: Share or reuse AMIs across projects, regions, or teams.
4. **Scalability**: Pair with Auto Scaling to launch identical instances automatically as demand grows.
5. **Backup**: AMIs can act as a recovery point—create one from an instance to preserve its state.

---

### **Things to Know**
- **Storage Backing**: AMIs can be EBS-backed (stored on Elastic Block Store for fast snapshots) or instance-store-backed (ephemeral, less common).
- **Region-Specific**: AMIs are tied to a region (e.g., **us-east-1**). To use one elsewhere, you must copy it to another region.
- **Permissions**: You can keep AMIs private, share them with specific AWS accounts, or make them public.
- **Cost**: Storing custom AMIs incurs minimal EBS snapshot fees; public AMIs are typically free unless from the Marketplace.

---

### **Real-World Example**
Imagine you’re running a web app:
- Start with an Amazon Linux 2 AMI.
- Install Node.js, your app code, and configure security settings on an EC2 instance.
- Save it as “MyApp-AMI-v1.”
- Now, launch 10 identical instances from “MyApp-AMI-v1” behind a load balancer—or share it with your team.

In short, an AMI is your shortcut to consistent, repeatable, and efficient server setups in AWS!

---

## 5. What are edge locations?

In the context of AWS, **edge locations** are specialized data centers used primarily by AWS’s content delivery network (CDN) service, **Amazon CloudFront**, and other services like **AWS Global Accelerator** or **Amazon Route 53**. Unlike full-fledged AWS regions or availability zones, edge locations are designed to cache content, accelerate data delivery, and reduce latency by bringing resources closer to end-users worldwide.

---

### **What Are Edge Locations?**
- **Definition**: Edge locations are smaller, strategically placed facilities that store cached copies of data (like web content, videos, or files) or handle specific networking tasks. They act as intermediaries between users and the main AWS infrastructure.
- **Purpose**: To improve performance by serving content from a location physically closer to the user, rather than fetching it from a distant region.
- **Scale**: AWS has over 400 edge locations globally as of 2025 (far more than the 30+ regions), spread across hundreds of cities in dozens of countries.

---

### **How Do They Work?**
1. **Content Delivery (CloudFront)**:
    - When a user requests content (e.g., a video or webpage), CloudFront checks the nearest edge location.
    - If the content is cached there (a “hit”), it’s delivered immediately—super fast.
    - If not (a “miss”), CloudFront fetches it from the origin server (e.g., an S3 bucket or EC2 instance), caches it at the edge, and then serves it.
2. **Networking (Global Accelerator, Route 53)**:
    - Edge locations can route traffic to the optimal AWS region or endpoint, reducing latency and improving reliability.
    - For example, Global Accelerator uses edge locations to direct user requests over AWS’s private network instead of the public internet.

---

### **Key Features**
- **Caching**: Temporarily stores frequently accessed data (e.g., images, videos, static web files) to reduce load on origin servers.
- **Low Latency**: Proximity to users cuts down round-trip time—think milliseconds instead of hundreds of milliseconds.
- **Global Coverage**: Edge locations exist in major cities (e.g., New York, Tokyo, London) and even smaller markets, far beyond AWS’s full regions.
- **Dynamic Content**: With CloudFront, edge locations can also handle dynamic requests (via Lambda@Edge) by running lightweight code closer to users.

---

### **Edge Locations vs. Regions vs. Availability Zones**
| **Aspect**          | **Edge Locations**          | **Regions**              | **Availability Zones**  |
|---------------------|-----------------------------|--------------------------|-------------------------|
| **Purpose**         | Cache content, optimize delivery | Host full AWS services   | Provide fault tolerance |
| **Size**            | Small, lightweight          | Large, multi-data-center | Medium, isolated units  |
| **Number**          | 400+ globally              | 30+ globally            | 2–6 per region          |
| **Services**        | CloudFront, Route 53, etc.  | EC2, S3, RDS, etc.       | Core compute/storage    |
| **Location Example**| Miami, Paris, Mumbai        | us-east-1 (N. Virginia)  | us-east-1a             |

---

### **Real-World Example**
- **Streaming Video**: A user in Sydney watches a video stored in an S3 bucket in **us-west-2** (Oregon). Instead of fetching it from Oregon (high latency), CloudFront delivers it from an edge location in Sydney, cached from the last request.
- **Website**: A global e-commerce site uses CloudFront to serve static assets (CSS, images) from edge locations, while dynamic content (cart updates) is processed via Lambda@Edge or routed to a region.

---

### **Why They Matter**
1. **Performance**: Users get content faster—crucial for apps, websites, or media.
2. **Scalability**: Offloads traffic from origin servers, handling spikes (e.g., Black Friday sales).
3. **Cost**: Reduces data transfer costs by minimizing requests to the origin.
4. **Reliability**: If one edge location fails, traffic reroutes to another nearby one.

In short, edge locations are AWS’s way of putting a “fast lane” between your content and your users, leveraging a massive global network to boost speed and efficiency!

---

## 6. What are the main pricing models in AWS?

AWS offers a variety of pricing models designed to provide flexibility and cost optimization based on how you use its services. These models apply across services like EC2, S3, Lambda, and more. Here are the main pricing models in AWS:

---

### 1. **Pay-As-You-Go (On-Demand Pricing)**
- **How It Works**: You pay only for what you use, by the hour, second, or gigabyte, with no upfront commitment or long-term contracts.
- **Key Features**:
    - No minimum fees or subscriptions.
    - Charged based on usage (e.g., EC2 hours, S3 storage GBs, Lambda invocations).
    - Billing granularity varies (e.g., EC2 by the second, S3 by the month).
- **Examples**:
    - EC2 On-Demand Instances: $0.0116/hour for a t3.micro in us-east-1.
    - S3: $0.023/GB-month for standard storage.
- **Best For**: Short-term workloads, testing, unpredictable usage, or when you want maximum flexibility.
- **Pros**: No commitment, easy to start/stop.
- **Cons**: Most expensive per-unit rate compared to other models.

---

### 2. **Reserved Instances (RIs)**
- **How It Works**: You commit to using a specific resource (e.g., an EC2 instance type) for a 1- or 3-year term in exchange for a significant discount over On-Demand pricing.
- **Key Features**:
    - Options: Standard RIs (up to 72% off) or Convertible RIs (up to 54% off, with flexibility to change instance types).
    - Payment: All upfront, partial upfront, or no upfront (higher savings with more upfront payment).
- **Examples**:
    - A t3.medium in us-east-1 might cost $0.0418/hour On-Demand but $0.025/hour with a 1-year Standard RI (all upfront).
- **Best For**: Predictable, steady-state workloads (e.g., databases, web servers).
- **Pros**: Big savings for long-term use.
- **Cons**: Locked into a commitment; less flexibility.

---

### 3. **Savings Plans**
- **How It Works**: A more flexible evolution of Reserved Instances. You commit to a consistent amount of usage (e.g., $10/hour) for 1 or 3 years, and AWS applies discounts across eligible services.
- **Key Features**:
    - Types:
        - **Compute Savings Plans**: Covers EC2, Lambda, and Fargate (up to 66% off).
        - **EC2 Instance Savings Plans**: Specific to an instance family/region (up to 72% off).
    - Payment: All upfront, partial, or no upfront.
- **Examples**:
    - Commit to $5/hour on Compute Savings Plan; use it on any EC2 instance type or Lambda, and get discounted rates.
- **Best For**: Workloads with variable instance types or multi-service usage.
- **Pros**: More flexible than RIs, broader coverage.
- **Cons**: Requires planning your spend; less savings than RIs for fixed workloads.

---

### 4. **Spot Instances**
- **How It Works**: You bid on unused AWS capacity at steep discounts (up to 90% off On-Demand). However, AWS can reclaim the instance with a 2-minute notice if demand spikes.
- **Key Features**:
    - Pricing fluctuates based on supply/demand.
    - You set a max bid price; if the spot price exceeds it, your instance stops.
- **Examples**:
    - A t3.large might drop from $0.0832/hour (On-Demand) to $0.025/hour on Spot.
- **Best For**: Fault-tolerant, interruptible workloads (e.g., batch processing, CI/CD, big data).
- **Pros**: Cheapest option for flexible tasks.
- **Cons**: Instances can terminate unexpectedly; not for critical apps.

---

### 5. **Free Tier**
- **How It Works**: AWS offers a limited amount of free usage for new customers (for 12 months) or specific services (always free).
- **Key Features**:
    - Examples: 750 hours/month of t2/t3.micro EC2, 5 GB S3 storage, 1 million Lambda requests/month.
    - Limits apply (e.g., only certain regions, instance types).
- **Best For**: Learning AWS, small projects, or testing.
- **Pros**: No cost to start.
- **Cons**: Limited scope; usage beyond free tier incurs standard rates.

---

### 6. **Per-Request Pricing**
- **How It Works**: Common in serverless or event-driven services, you pay per action or request rather than per hour.
- **Examples**:
    - **AWS Lambda**: $0.20 per 1 million requests + compute duration (GB-seconds).
    - **API Gateway**: $1.00 per million API calls.
- **Best For**: Event-driven apps, microservices, or low-traffic workloads.
- **Pros**: Scales to zero (no idle costs); cost-effective for sporadic use.
- **Cons**: Can get pricey with high request volumes.

---

### 7. **Data Transfer and Storage Pricing**
- **How It Works**: Charges apply for storing data and moving it in/out of AWS services.
- **Key Features**:
    - **Storage**: E.g., S3 at $0.023/GB-month (Standard tier), cheaper for infrequent access tiers.
    - **Data Transfer**: Free within a region; fees for outbound (e.g., $0.09/GB from us-east-1 to the internet) or cross-region transfers.
- **Best For**: Any service using storage or bandwidth.
- **Pros**: Predictable for storage; free inbound transfers.
- **Cons**: Outbound costs can add up for high-traffic apps.

---

### **Key Considerations**
- **Mix and Match**: You can combine models (e.g., use Spot for testing, RIs for production, Lambda for events).
- **Cost Management Tools**: AWS Budgets, Cost Explorer, and Trusted Advisor help track and optimize spending.
- **Region Variability**: Prices differ slightly by region (e.g., us-east-1 is often cheaper than ap-northeast-1).
- **Billing**: Consolidated monthly via AWS Billing Dashboard; detailed with Cost Allocation Tags.

---

### **Real-World Example**
- A startup might:
    - Use Free Tier to prototype (t3.micro + S3).
    - Switch to On-Demand for a launch ($0.0116/hour).
    - Buy a Savings Plan ($5/hour) as traffic stabilizes.
    - Add Spot Instances for batch jobs (90% off).
    - Pay per-request for Lambda APIs ($0.20/million).

AWS’s pricing is all about flexibility—pick the model that fits your workload, budget, and growth stage!

---

## 7. What are Reserved Instances vs On-Demand vs Spot Instances?

In AWS, **Reserved Instances (RIs)**, **On-Demand Instances**, and **Spot Instances** are pricing models for EC2 (Elastic Compute Cloud) that cater to different use cases based on cost, flexibility, and reliability. Here’s a breakdown of each and how they compare:

---

### **1. On-Demand Instances**
- **What It Is**: You pay for EC2 compute capacity by the hour or second (depending on the instance type) with no upfront commitment or long-term contract. It’s the "default" pricing model.
- **How It Works**:
    - Launch instances whenever you need them, stop them when you don’t.
    - Billed only for the time they’re running (e.g., 1-second increments for Linux instances).
- **Pricing Example**: A t3.micro in us-east-1 might cost $0.0116/hour.
- **Key Features**:
    - Full flexibility—no lock-in.
    - AWS guarantees availability (no interruptions unless you stop them).
- **Best For**:
    - Short-term workloads, testing, or unpredictable usage (e.g., dev environments, one-off tasks).
- **Pros**:
    - Simple and flexible; no planning required.
    - Pay only for what you use.
- **Cons**:
    - Most expensive per-hour rate compared to RIs or Spot.

---

### **2. Reserved Instances (RIs)**
- **What It Is**: You commit to using a specific EC2 instance type (e.g., t3.large) in a specific region for a 1- or 3-year term, getting a significant discount (up to 72% off On-Demand).
- **How It Works**:
    - Choose an instance family, size, OS, and region, then reserve it.
    - Payment options: All upfront (biggest discount), partial upfront, or no upfront (smaller discount).
    - Two types:
        - **Standard RIs**: Fixed configuration, max savings.
        - **Convertible RIs**: Swap instance types later, slightly less savings (up to 54% off).
- **Pricing Example**: A t3.medium might drop from $0.0418/hour (On-Demand) to $0.025/hour (1-year Standard RI, all upfront).
- **Key Features**:
    - Guaranteed capacity in the chosen region/AZ.
    - Discount applies as long as you’re running matching instances.
- **Best For**:
    - Predictable, steady workloads (e.g., production databases, web servers running 24/7).
- **Pros**:
    - Huge cost savings for long-term use.
    - Capacity reservation option for critical apps.
- **Cons**:
    - Locked into a commitment; less flexibility if needs change.

---

### **3. Spot Instances**
- **What It Is**: You bid on unused EC2 capacity at steep discounts (up to 90% off On-Demand), but AWS can reclaim the instance with a 2-minute notice if demand rises.
- **How It Works**:
    - Set a maximum bid price; if the Spot price (set by AWS based on supply/demand) is below your bid, you get the instance.
    - If the Spot price exceeds your bid or capacity runs low, AWS terminates your instance after a 2-minute warning.
- **Pricing Example**: A t3.large might fall from $0.0832/hour (On-Demand) to $0.025/hour on Spot (price varies dynamically).
- **Key Features**:
    - No commitment; instances can stop anytime.
    - Ideal for stateless or interruptible tasks.
- **Best For**:
    - Fault-tolerant, flexible workloads (e.g., batch processing, data analysis, CI/CD pipelines).
- **Pros**:
    - Cheapest option by far when available.
    - Great for scaling non-critical tasks.
- **Cons**:
    - Unreliable—can be interrupted with little notice.
    - Not suited for critical or stateful apps.

---

### **Comparison Table**
| **Aspect**          | **On-Demand**          | **Reserved Instances**   | **Spot Instances**    |
|---------------------|------------------------|--------------------------|-----------------------|
| **Cost**            | Highest ($/hour)       | Medium (up to 72% off)   | Lowest (up to 90% off) |
| **Commitment**      | None                  | 1 or 3 years             | None                  |
| **Flexibility**     | High (start/stop anytime) | Low (fixed term/type) | Medium (bid-based)    |
| **Availability**    | Guaranteed            | Guaranteed               | Interruptible         |
| **Billing**         | Per hour/second       | Upfront + hourly         | Per hour (while running) |
| **Use Case**        | Testing, short-term   | Steady, long-term        | Batch, fault-tolerant |
| **Example Price**   | $0.0832/hr (t3.large) | $0.045/hr (1-yr RI)      | $0.025/hr (varies)    |

---

### **Real-World Scenarios**
1. **Startup Testing**: Use On-Demand to launch a t3.micro ($0.0116/hour) for a proof-of-concept—no commitment, full control.
2. **E-commerce Site**: Reserve t3.large instances ($0.045/hour with RI) for a web server running 24/7—predictable cost, reliable uptime.
3. **Data Crunching**: Run Spot Instances for a Hadoop cluster—save 90% on a t3.xlarge ($0.05/hour vs. $0.1664/hour) since interruptions are manageable.

---

### **Key Takeaways**
- **On-Demand**: Pay full price for maximum flexibility and reliability.
- **Reserved Instances**: Lock in for big savings on predictable workloads.
- **Spot Instances**: Gamble on cheap capacity for non-critical, interruptible tasks.

You can mix these models in a single app—e.g., RIs for the core, Spot for scaling, and On-Demand for spikes—to optimize cost and performance!

---

## 8. What is the AWS Shared Responsibility Model?

The **AWS Shared Responsibility Model** is a framework that defines the division of security and operational responsibilities between AWS and its customers when using AWS cloud services. It clarifies who handles what to ensure a secure and reliable cloud environment. The core idea is that AWS manages the security *of* the cloud (infrastructure), while customers manage Angstrom manage the security *in* the cloud (applications, data, etc.).

---

### **Breakdown of Responsibilities**
The model splits responsibilities into two main categories:

#### **AWS’s Responsibility: Security "Of" the Cloud**
AWS takes care of the underlying infrastructure and services that power the cloud. This includes:
- **Physical Security**: Securing data centers (e.g., access controls, surveillance).
- **Compute, Storage, Networking**: Maintaining the hardware and virtualization layers (e.g., EC2 instances, S3 buckets).
- **Global Infrastructure**: Ensuring regions, availability zones, and edge locations are operational and resilient.
- **Software**: Managing the hypervisors, operating systems, and foundational services AWS provides.
- **Compliance**: Meeting industry standards (e.g., ISO 27001, SOC) for the infrastructure.

In short, AWS ensures the cloud platform itself is secure, reliable, and available.

#### **Customer’s Responsibility: Security "In" the Cloud**
Customers are responsible for how they configure and use AWS services. This includes:
- **Data Security**: Encrypting data at rest and in transit, managing encryption keys.
- **Identity and Access Management (IAM)**: Setting up users, roles, permissions, and multi-factor authentication (MFA).
- **Operating Systems and Applications**: Patching, securing, and configuring software running on EC2 instances or containers.
- **Network Security**: Configuring firewalls, security groups, VPCs, and network access control lists (ACLs).
- **Compliance**: Ensuring applications and data handling meet regulatory requirements (e.g., GDPR, HIPAA).

Essentially, customers control what they build and deploy *on* AWS, including securing their workloads and data.

---

### **Visualizing the Model**
Think of it like renting a house:
- **AWS (Landlord)**: Maintains the building structure, plumbing, and electricity (the cloud infrastructure).
- **Customer (Tenant)**: Locks the doors, installs alarms, and manages what’s inside (the applications and data).

AWS provides the tools (e.g., IAM, KMS, CloudTrail), but customers must use them correctly.

---

### **Service-Specific Variations**
The split shifts depending on the service model:
- **IaaS (e.g., EC2)**: AWS manages hardware and virtualization; customers handle OS, apps, and security settings.
- **PaaS (e.g., Elastic Beanstalk, Lambda)**: AWS takes on more (e.g., OS, runtime); customers focus on app code and data.
- **SaaS (e.g., WorkMail)**: AWS manages almost everything; customers just configure users and policies.

For example:
- On EC2, you patch the OS; AWS ensures the server hardware works.
- With Lambda, AWS patches the runtime; you secure your function’s code.

---

### **Why It Matters**
- **Clarity**: Avoids confusion over who’s accountable for what.
- **Security**: Both parties must do their part to prevent breaches or downtime.
- **Flexibility**: Customers can tailor security to their needs, while AWS ensures a solid foundation.

---

### **Real-World Example**
- **S3 Bucket Leak**: If a customer leaves an S3 bucket public (misconfiguration), it’s their fault—not AWS’s—since access control is the customer’s responsibility.
- **Data Center Failure**: If an AWS region goes down due to a power outage, AWS fixes it—they own the infrastructure.

In short, the Shared Responsibility Model is a partnership: AWS builds a secure cloud, and you secure what you put in it!

---

## 9. What is the AWS Free Tier?

The **AWS Free Tier** is a program offered by Amazon Web Services that allows new and existing customers to explore and use certain AWS services at no cost, up to specified limits. It’s designed to help users learn AWS, test services, or run small projects without upfront expenses. The Free Tier includes a mix of time-limited offers (for new customers) and always-free options (for all users), but usage beyond the limits incurs standard pricing.

---

### **Types of AWS Free Tier Offers**
The Free Tier is divided into three categories:

#### 1. **12-Month Free Tier (New Customers Only)**
- **Duration**: Starts when you create an AWS account and lasts for 12 months.
- **Purpose**: Gives new users a chance to try core services for free within limits.
- **Examples**:
    - **Amazon EC2**: 750 hours/month of t2.micro or t3.micro instances (enough for one instance running 24/7).
    - **Amazon S3**: 5 GB of standard storage, 20,000 GET requests, 2,000 PUT requests.
    - **AWS Lambda**: 1 million free requests and 3.2 million seconds of compute time per month.
    - **Amazon RDS**: 750 hours/month of a db.t2.micro or db.t3.micro database instance, plus 20 GB of storage.
- **Key Details**:
    - Expires 12 months after account creation—unused hours don’t roll over.
    - Only applies to specific instance types/regions (e.g., t2.micro in us-east-1).

#### 2. **Always Free Tier (All Customers)**
- **Duration**: No expiration—available indefinitely to all AWS users.
- **Purpose**: Supports small-scale or ongoing use cases (e.g., learning, personal projects).
- **Examples**:
    - **AWS Lambda**: 1 million requests and 3.2 million seconds of compute time per month.
    - **Amazon DynamoDB**: 25 GB of storage and 25 write/read capacity units.
    - **Amazon SNS**: 1 million publishes (notifications) per month.
    - **AWS CloudWatch**: 10 custom metrics and 10 alarms.
- **Key Details**:
    - Limits reset monthly; no time restriction on eligibility.

#### 3. **Free Trials (Service-Specific)**
- **Duration**: Varies by service (e.g., 30 days, 60 days, or a usage cap).
- **Purpose**: Lets you test premium or specialized services briefly.
- **Examples**:
    - **Amazon SageMaker**: 250 hours of free compute for machine learning (first 2 months).
    - **AWS DeepRacer**: 10 hours of free training (first month).
    - **Amazon QuickSight**: 1 user free for 30 days.
- **Key Details**:
    - Starts when you first use the service; converts to paid after the trial ends.

---

### **Key Features**
- **No Upfront Cost**: Free within limits—no credit card charges until you exceed them.
- **Wide Coverage**: Includes over 100 services, from compute (EC2, Lambda) to storage (S3) and databases (RDS, DynamoDB).
- **Monitoring**: AWS Free Tier Usage Alerts notify you if you’re nearing limits.
- **Eligibility**: New accounts get the 12-month tier; all accounts get always-free offers.

---

### **Limits and Gotchas**
- **Overages**: Usage beyond Free Tier limits (e.g., running a second t3.micro) incurs standard On-Demand rates (e.g., $0.0116/hour for t3.micro).
- **Regions**: Some free offerings are region-specific (e.g., us-east-1, not ap-northeast-1).
- **Service Restrictions**: Only basic tiers are free (e.g., S3 Standard, not Glacier).
- **Billing Surprise Risk**: Forgetting to shut down resources (e.g., an EC2 instance) after the 12-month tier expires can lead to charges.

---

### **Real-World Examples**
1. **Learning AWS**: Use 750 EC2 hours to run a t3.micro web server all month, store files in 5 GB of S3, and experiment with 1 million Lambda requests—all free for 12 months.
2. **Micro Startup**: Host a small app with Lambda (1 million free requests) and DynamoDB (25 GB free) indefinitely under the always-free tier.
3. **ML Experiment**: Test SageMaker with 250 free hours in the first 2 months, then decide if it’s worth paying for.

---

### **Why It Exists**
- **Onboarding**: Encourages new users to try AWS without financial risk.
- **Innovation**: Lets developers prototype ideas cheaply.
- **Stickiness**: Hooks users into the AWS ecosystem, hoping they’ll scale up to paid tiers.

In short, the AWS Free Tier is a sandbox for learning and small-scale projects—just keep an eye on usage to avoid unexpected bills after the free limits!

---

## 10. Explain elasticity and scalability in AWS.

In AWS, **elasticity** and **scalability** are related but distinct concepts that describe how cloud resources adapt to workload changes. They’re key to AWS’s value proposition, enabling cost efficiency, performance, and resilience. Here’s a clear explanation of each, how they work in AWS, and how they differ:

---

### **Scalability**
- **Definition**: Scalability is the ability of a system to handle increased load (e.g., more users, traffic, or data) by adding resources, either manually or through planning. It’s about capacity growth over time.
- **Types**:
    1. **Vertical Scalability (Scaling Up/Down)**:
        - Increase the size or power of an existing resource (e.g., upgrading an EC2 instance from t3.micro to t3.large).
        - Limited by the maximum size of the resource (e.g., biggest instance type).
    2. **Horizontal Scalability (Scaling Out/In)**:
        - Add more instances or nodes to distribute the load (e.g., adding more EC2 instances behind a load balancer).
        - Virtually limitless in AWS due to its vast infrastructure.
- **How It Works in AWS**:
    - **Manual Scaling**: You adjust resources yourself (e.g., launch more EC2 instances or increase RDS storage).
    - **Planned Scaling**: Use tools like AWS Auto Scaling with predefined rules (e.g., add 2 instances when CPU hits 70%).
- **Examples**:
    - A web app scales up from a t3.medium to a t3.xlarge to handle more users.
    - A database scales out by adding read replicas in Amazon RDS.
- **Best For**: Long-term growth, predictable increases (e.g., a growing business adding users monthly).

---

### **Elasticity**
- **Definition**: Elasticity is the ability of a system to automatically and dynamically adjust resources (up or down) in real-time to match fluctuating demand, then return to a baseline when demand drops. It’s about responsiveness and efficiency.
- **Key Characteristics**:
    - Fully automated and rapid—resources adapt without human intervention.
    - Temporary adjustments—resources scale back when no longer needed.
- **How It Works in AWS**:
    - **AWS Auto Scaling**: Automatically adds or removes EC2 instances based on metrics (e.g., CPU usage, request count).
    - **Elastic Load Balancer (ELB)**: Distributes traffic across instances as they scale.
    - **Serverless Services**: Lambda scales instantly per request; S3 handles unlimited storage growth.
- **Examples**:
    - During a Black Friday sale, Auto Scaling adds 10 EC2 instances as traffic spikes, then removes them when it drops.
    - Lambda executes 1 function for 1 user, then 1,000 functions for 1,000 users, scaling to zero when idle.
- **Best For**: Short-term, unpredictable fluctuations (e.g., traffic surges, seasonal peaks).

---

### **Key Differences**
| **Aspect**          | **Scalability**              | **Elasticity**              |
|---------------------|------------------------------|-----------------------------|
| **Definition**      | Ability to grow capacity     | Ability to adapt dynamically|
| **Timeframe**       | Long-term, planned           | Short-term, real-time       |
| **Automation**      | Can be manual or automated  | Always automated            |
| **Direction**       | Often upward (growth)       | Up and down (flexible)      |
| **Goal**            | Handle increased load       | Match demand efficiently    |
| **AWS Example**     | Add EC2 instances for users | Auto Scale for a traffic spike |

---

### **How AWS Enables Both**
1. **Scalability Tools**:
    - **EC2 Instance Types**: Scale up by choosing larger instances (e.g., m5.large to m5.4xlarge).
    - **RDS**: Increase storage or add read replicas.
    - **S3**: Unlimited object storage without manual intervention.
2. **Elasticity Tools**:
    - **Auto Scaling Groups**: Automatically adjust EC2 instance counts based on CloudWatch metrics.
    - **Elastic Load Balancing**: Distributes traffic across scaled resources.
    - **Serverless**: Lambda, Fargate, and DynamoDB scale seamlessly with no capacity planning.
3. **Monitoring**: CloudWatch tracks metrics (CPU, traffic) to trigger scaling actions.

---

### **Real-World Scenarios**
- **Scalability**: A startup’s user base grows from 1,000 to 10,000 over a year. They manually upgrade their EC2 instance from t3.medium to t3.xlarge and add a second instance for redundancy.
- **Elasticity**: During a product launch, traffic jumps from 100 to 10,000 users in an hour. Auto Scaling spins up 5 extra EC2 instances, then terminates them when traffic normalizes.

---

### **Why They Matter**
- **Cost Efficiency**: Elasticity prevents over-provisioning (paying for idle resources); scalability avoids under-provisioning (performance bottlenecks).
- **Performance**: Scalability supports growth; elasticity handles spikes without downtime.
- **Flexibility**: AWS’s cloud model lets you scale and stretch resources as needed, unlike rigid on-premises setups.

In short, **scalability** builds capacity for growth, while **elasticity** flexes with demand—together, they make AWS a powerhouse for dynamic workloads!

---

## 11. What’s the difference between vertical and horizontal scaling?



---

## 12. What are AWS Trusted Advisor and its benefits?

---

## 13. What is AWS Well-Architected Framework?

---

## 14. What is an AWS Landing Zone?

---

15. What is AWS Organizations and how is it used?

---

### 🔹 16–30: **EC2 (Elastic Compute Cloud)**

16. What is EC2 and what are its use cases?
17. What are EC2 instance types and how do you choose one?
18. What is an EC2 key pair and how is it used?
19. What are EC2 security groups and how do they work?
20. What is a user data script in EC2?
21. What is an EC2 placement group?
22. How do you attach and detach EBS volumes?
23. What is the difference between EBS and instance store?
24. What is an Auto Scaling Group (ASG)?
25. How do you configure an EC2 instance to scale automatically?
26. How do you monitor an EC2 instance?
27. What happens when an EC2 instance is stopped vs terminated?
28. How do you take a snapshot of an EC2 instance?
29. How do you implement high availability with EC2?
30. What are EC2 launch templates?

---

### 🔹 31–45: **S3 (Simple Storage Service)**

31. What is Amazon S3?
32. What is the durability and availability of S3?
33. What is the difference between S3 Standard and S3 Glacier?
34. What are S3 buckets and object keys?
35. How do you make an S3 bucket public?
36. What is S3 Versioning and why is it useful?
37. What are S3 lifecycle rules?
38. How does S3 encryption work (SSE-S3 vs SSE-KMS vs SSE-C)?
39. How do you enable static website hosting on S3?
40. What is S3 Transfer Acceleration?
41. What are S3 pre-signed URLs?
42. What is an S3 Event Notification?
43. How do you secure access to S3 buckets?
44. How do you use S3 with CloudFront?
45. What is cross-region replication in S3?

---

### 🔹 46–55: **IAM (Identity and Access Management)**

46. What is IAM and why is it important?
47. What are IAM users, groups, and roles?
48. What is an IAM policy and how is it structured?
49. What is the principle of least privilege in IAM?
50. How do IAM roles work with EC2?
51. How do you troubleshoot “Access Denied” in AWS?
52. What are IAM policies vs resource-based policies?
53. What are inline vs managed policies?
54. What is AWS STS (Security Token Service)?
55. How do you enforce MFA in AWS?

---

### 🔹 56–65: **Networking & VPC**

56. What is a VPC and what are its components?
57. What is a subnet? What is the difference between public and private subnets?
58. What is an Internet Gateway and how is it used?
59. What is a NAT Gateway?
60. What is a Route Table?
61. What is a VPC peering connection?
62. What is a security group vs network ACL?
63. What are Elastic IPs?
64. What is a Bastion Host?
65. How do you create a high-availability architecture in a VPC?

---

### 🔹 66–75: **Databases (RDS, DynamoDB, Aurora)**

66. What is Amazon RDS?
67. What databases are supported by RDS?
68. What is RDS Multi-AZ deployment?
69. How does RDS automated backup and snapshot work?
70. What is Amazon Aurora and why is it better?
71. What is DynamoDB?
72. What are read and write capacity units in DynamoDB?
73. What is a DynamoDB global secondary index?
74. What are DynamoDB streams?
75. How does DynamoDB handle replication and consistency?

---

### 🔹 76–85: **Lambda, API Gateway & Serverless**

76. What is AWS Lambda?
77. How is Lambda billed?
78. What are Lambda triggers and destinations?
79. What are cold starts in Lambda?
80. What is AWS API Gateway?
81. How do you secure API Gateway endpoints?
82. What is the integration between Lambda and API Gateway?
83. What are Lambda layers?
84. What are common Lambda use cases?
85. What are the limits of AWS Lambda?

---

### 🔹 86–90: **CloudFormation & Infrastructure as Code**

86. What is AWS CloudFormation?
87. What is a CloudFormation stack?
88. What is a CloudFormation template?
89. What is drift detection in CloudFormation?
90. What are alternatives to CloudFormation (e.g., Terraform)?

---

### 🔹 91–95: **Monitoring, DevOps & CI/CD**

91. What is Amazon CloudWatch?
92. How do you set up CloudWatch alarms?
93. What is AWS CloudTrail and how is it used?
94. What is AWS CodePipeline?
95. How do you deploy Docker containers in AWS?

---

### 🔹 96–100: **Architecture, Best Practices & Security**

96. How do you secure an AWS architecture?
97. How do you design a fault-tolerant system in AWS?
98. How would you implement a multi-region architecture?
99. What is AWS WAF and how does it help?
100. How do you audit, monitor, and log access in a production AWS environment?

---

### 📘 Bonus

Would you like any of the following?
- A **PDF version** of this complete list
- A **deep-dive on AWS interview Q&A** (with answers and scenarios)
- **Architecture diagrams and real-world use cases**
- **AWS certification preparation tips (Solutions Architect / DevOps)**

Let me know how you'd like to proceed, and I’ll tailor it to your prep goals!