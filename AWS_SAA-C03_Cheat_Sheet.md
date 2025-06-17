# 🧠 AWS SAA-C03 All-in-One Cheat Sheet

> **One-page master reference** for the AWS Certified Solutions Architect – Associate exam.  
> Each domain table lists individual **service variants** (e.g., S3 storage classes, EC2 purchase models), plus **When to use · Key features · Classic exam trigger phrases · Top 3–5 quotas**.

---

## 📚 Table of Contents
1. [Compute](#compute) • 2. [Storage](#storage) • 3. [Networking & CDN](#networking) • 4. [Database](#database) • 5. [Security & Identity](#security) • 6. [Management & Monitoring](#management) • 7. [Application Integration](#integration) • 8. [Analytics & Big Data](#analytics) • 9. [Developer Tools & DevOps](#devops) • 10. [Migration & Hybrid](#migration) • 11. [Machine Learning](#ml) • 12. [DR Patterns](#dr) • 13. [Acronym Key](#acronyms)

---

## 🖥️ Compute  <a id="compute"></a>

| Option | When to Use | Key Features | Classic Exam Trigger | **Top Quotas** |
|---|---|---|---|---|
| **EC2 On-Demand** | Flexible, pay-as-you-go | Any instance, no commitment | “Spiky / unpredictable load” | Instances/Region ≈ 20 |
| **EC2 Reserved (Std/Conv)** | Steady baseline ≥ 1 yr | 72 % savings, AZ or Region scope | “Always-on prod server” | RIs/Region 20 000 |
| **EC2 Spot** | Cost-opt fault-tolerant | Up to 90 % off, 2-min notice | “Batch, big data, CI” | Spot cap = On-Demand quota |
| **Compute Savings Plan** | Flexible discount | Covers EC2/Fargate/Lambda | “Want discount w/out RI lock-in” | Commit term 1 or 3 yr |
| **Lambda On-Demand** | Event-driven ≤ 15 min | 100 ms billing, auto-scale | “Serverless function” | Concurrency 1 000 |
| **Lambda Provisioned Conc.** | Predictable latency | Pre-warmed, min latency | “Cold-start sensitive API” | Same concurrency quota |
| **ECS Fargate** | Serverless containers | Pay vCPU/GB-sec | “No EC2 mgmt for containers” | Tasks/service 1 000 |
| **ECS on EC2** | Custom AMI/daemon | Full host control | “Need GPU/daemonset” | Limited by EC2 quotas |
| **EC2 Auto Scaling** | Elastic fleet mgmt | Dynamic, Scheduled, Predictive; mixed-instance policies; cooldowns | “Scale to meet target CPU” | ASGs/Region 1 000 |
| **EKS (Kubernetes)** | Managed K8s control plane | Fargate profiles, IRSA, VPC-CNI | “Need upstream K8s APIs” | Clusters 100 |

---

## 💾 Storage  <a id="storage"></a>

| Option | When to Use | Key Features | Classic Exam Trigger | **Top Quotas** |
|---|---|---|---|---|
| **S3 Standard** | Frequently accessed | Multi-AZ, 11×9s, high avail | “Hot objects, data lake” | Object 5 TB |
| **S3 Intelligent-Tier** | Unknown access pattern | Auto-moves tiers | “New or unpredictable data” | Monitoring fee/object |
| **S3 Standard-IA** | Infrequent access | 99.9 % avail, retrieval fee | “Logs, backups 1×/mo” | Min 128 KB • 30-day stay |
| **S3 One-Zone-IA** | Non-critical IA | Single-AZ cheaper | “Re-creatable data” | Same as Std-IA |
| **S3 Glacier Instant** | Archive w/ ms restore | Lower $/GB, instant get | “Archive but instant access” | Min 90 days |
| **S3 Glacier Flexible** | Deep archive mins–hrs | Bulk/expedite | “Compliance archive” | Min 90 days |
| **S3 Glacier Deep** | Lowest cost 12–48 h | Tape-like | “Decades retention” | Min 180 days |
| **EBS gp3** | Gen-purpose SSD | 3 000 IOPS base | “General workloads” | 16 K IOPS / 1 000 MB/s |
| **EBS io2 / Block Express** | Mission-crit SSD | 64 K+ IOPS, 99.999 % | “DB needs 1 ms IO” | 64 K IOPS (256 K Express) |
| **EBS st1** | Throughput HDD | 500 MiB/s seq | “Big data, log proc” | Vol 16 TB |
| **EBS sc1** | Cold HDD | Low IO $, 250 MiB/s | “Archival on block” | Vol 16 TB |
| **EFS Standard** | Multi-AZ NFS | Elastic, burst credit | “Shared Linux FS” | Burst 5 GB/s |
| **EFS One-Zone** | Single-AZ, 47 % less | Same perf, lower dur | “Non-mission-crit share” | — |
| **EFS IA** | File-level tiering | 92 % cheaper | “Cold shared files” | Lifecycle 30 days |
| **FSx Windows** | Lift SMB share | AD-join, shadow copy | “Windows file server” | Vol 64 TB |
| **FSx Lustre** | HPC / ML | 100 GB/s, mounts to S3 | “High-perf scratch” | File sys 512 TiB |

---

## 🌐 Networking & CDN  <a id="networking"></a>

| Option | When to Use | Key Features | Classic Exam Trigger | **Top Quotas** |
|---|---|---|---|---|
| **ALB** | HTTP/S 7-layer | Path/host rules, WAF | “/api vs /img routes” | Listeners 50 • Rules 100 |
| **NLB** | TCP/UDP 4-layer | Static IP, TLS offload | “Millions TPS” | TLS listeners 50 |
| **Gateway LB** | Inline appliances | 3rd-party firewall | “Deep packet inspect” | GWLB/region 20 |
| **VPCE Interface** | Private AWS API | ENI in subnet | “PrivateLink KMS/S3” | 50 / VPC |
| **VPCE Gateway** | S3/Dynamo only | Route-table target | “Private S3 bucket” | 20 / VPC |
| **Route 53 Simple** | Single record | Round-robin | “Basic DNS” | Records/zone 10 k |
| **Route 53 Latency** | Geo RTT | AWS Regions | “Send EU to eu-west-1” | same |
| **Route 53 Failover** | Active-passive | Health checks | “DR failover” | same |
| **Route 53 Weighted** | % split | Blue/green | “Shift 10 % traffic” | same |
| **CloudFront** | Global cache | 310+ PoPs, Shield Std | “Static/dynamic global” | Dists 200 |
| **NAT Gateway** | Outbound only | 45 Gbps/AZ | “Private subnet updates” | NATs/AZ 5 |
| **AWS Outposts** | On-prem AWS | Same APIs, Local SNS/SQS | “Low-latency to factory floor” | Racks/site 20 |
| **Local Zones** | Metro edge compute | Sub-10 ms latency, shares parent Region | “Media workloads near users” | Zones/Region > 25 |
| **Wavelength** | 5G MEC for telcos | Runs in carriers’ 5G core | “Ultra-low latency gaming” | Zones/Region varies |
| **Global Accelerator** | Anycast edge IP | TCP/UDP, health-based failover | “Improve cross-Region latency” | Accelerators 20 |
| **Data-Transfer Pricing** | Cost planning | **Inter-AZ $0.01/GB** · **Inter-Region $0.02–0.09/GB** · Same-AZ = free | “Cheapest path for traffic” | — |

---

## 🧮 Database  <a id="database"></a>

| Option | When to Use | Key Features | Classic Exam Trigger | **Top Quotas** |
|---|---|---|---|---|
| **RDS Single-AZ** | Dev/test | No standby | “Lower cost, okay downtime” | DBs 40 |
| **RDS Multi-AZ** | Prod HA | Synchronous standby | “Auto failover < 1 min” | same |
| **RDS Read Replica** | Scale reads | Async replication | “Read-scaling reports” | Replicas 5 |
| **Aurora Provisioned** | High TPS | 6-copy, 15 replicas | “> 5× MySQL perf” | Replicas 15 |
| **Aurora Serverless v2** | Variable load | 0.5–128 ACU scale | “Infrequent bursts” | ACU max 128 |
| **Dynamo On-Demand** | Unpredictable | Pay per request | “Spiky IoT telemetry” | RCU 40 k |
| **Dynamo Provisioned** | Consistent load | RCUs/WCUs | “Steady traffic” | same |
| **DAX Cluster** | Micro-latency | In-mem cache | “Read heavy, ≤ 1 ms” | Nodes/cluster 10 |

---

## 🔐 Security & Identity  <a id="security"></a>

| Option | When to Use | Key Features | Classic Exam Trigger | **Top Quotas** |
|---|---|---|---|---|
| **IAM** | Access control | Users, roles, policies | Always | Users 5 000 |
| **KMS CMK** | Encrypt data | 256-bit keys, FIPS | “Encrypt S3/EBS” | CMKs 1 000 |
| **Secrets Manager** | Store creds | Auto-rotate w/ Lambda | “Rotate DB pwd” | Secrets 5 000 |
| **WAF Managed** | OWASP rules | Pre-built vendor sets | “PCI compliance” | ACL rules 1 500 |
| **WAF Rate-Based** | Throttle bad IP | 100-2 M req/5 min | “Block brute force” | Rules 100 |
| **Shield Std** | Default L3/4 | Auto for all resources | “Basic DDoS” | automatic |
| **Shield Adv** | Enterprise L3/4 | 24×7 DRT, cost credit | “Mission-critical site” | 1 000 resources |
| **GuardDuty** | Threat detect | ML on VPC/CT logs | “Detect crypto-mining” | Detector 1/Region |
| **Service Control Policy (SCP)** | Org-wide guardrails | Deny/Allow, no IAM bypass, evals *first* | “Block RDS create in dev OU” | SCPs/org 5 000 |
| **IAM Access Analyzer** | Cross-acct exposure | Zelkova provable access | “Find public S3 buckets” | Analyzers 1/Region |

---

## 📈 Management & Monitoring  <a id="management"></a>

| Option | When to Use | Key Features | Classic Exam Trigger | **Top Quotas** |
|---|---|---|---|---|
| **CloudWatch Metrics** | Dashboards & alarms | Standard & custom metrics | “Scale on alarm” | Custom metrics 500 • Alarms 5 000 |
| **CloudWatch Logs Std** | Active log search | Ingestion, Logs Insights | “Debug app logs” | Event size 256 KB |
| **CloudWatch Logs Archive** | Long-term logs | 45 % cheaper, re-hydrate | “Store logs 1 yr+ cheap” | 5 GB/query limit |
| **AWS Config** | Resource drift | Rules, packs | “CIS baseline” | Rules 150 |
| **Control Tower** | Multi-acct landing zone | Guardrails (SCP + Config) | “Secure new org quickly” | OUs 300 |
| **AWS Organizations** | Account mgmt | SCPs, billing | “Restrict region” | Accts/org 10 000 |
| **CloudTrail Lake** | Searchable audit lake | SQL on 7-yr log store | “Query events w/out Athena” | Ingest 5 TB/region/mo |
| **CloudTrail Org Trail** | Central audit | One trail, multi-acct, multi-Region | “Compliance evidence” | 1 per org |
| **VPC Flow Logs – Enhanced** | Deep packet insight | Basic / Sampled / Agent tiers | “Packet-level latency drill” | Flow logs 50 |
| **AWS Auto Scaling (Console)** | Optimize fleets | Fleet Advisor, scaling plans | “Balanced cost & perf plan” | Plans/Region 50 |

---

## 📬 Application Integration  <a id="integration"></a>

| Option | When to Use | Key Features | Classic Exam Trigger | **Top Quotas** |
|---|---|---|---|---|
| **SQS Std** | High-throughput queue | At-least-once | “Buffer workload” | In-flight 120 K |
| **SQS FIFO** | Ordered queue | Exactly-once | “Preserve order” | FIFO TPS 3 K batch |
| **SNS Topic** | Pub/Sub push | Email, SMS, Lambda | “Fan-out alerts” | Subs/topic 12 500 |
| **EventBridge Default Bus** | AWS events | 90+ services | “Route AWS events” | Rules/bus 300 |
| **EventBridge Custom Bus** | App/SaaS events | Schema registry | “SaaS integration” | Buses 1 000 |

---

## 📊 Analytics & Big Data  <a id="analytics"></a>

| Option | When to Use | Key Features | Classic Exam Trigger | **Top Quotas** |
|---|---|---|---|---|
| **Athena** | SQL on S3 | Pay per TB scanned | “Ad-hoc query data lake” | Timeout 30 m |
| **Glue Crawler** | Discover schema | Auto-catalog | “Catalog parquet” | Crawlers 100 |
| **Glue ETL Job** | Transform data | PySpark, bookmarks | “CSV → Parquet” | Jobs 250 |
| **Kinesis Data Streams** | Low-latency ingest | 70 MB/s/shard | “Real-time clickstream” | Shards 10 000 |
| **Kinesis Firehose** | Load to S3/Redshift | Auto batch/compress | “Ingest logs” | TPS 5 000/stream |
| **EMR** | Managed Hadoop/Spark | Spot clusters | “Huge Spark job” | Nodes 500 |
| **EMR Serverless** | Spark SQL w/out cluster | Auto-scale slots | “One-off ETL” | Apps 100 |
| **QuickSight SPICE** | Serverless BI | In-mem engine | “Exec dashboards” | Datasets 1 000 |

---

## 🛠️ Developer Tools & DevOps  <a id="devops"></a>

| Option | When to Use | Key Features | Classic Exam Trigger | **Top Quotas** |
|---|---|---|---|---|
| **CodeCommit** | Private Git repo | Encrypted, IAM | “AWS Git” | Repos 1 000 |
| **CodeBuild** | Managed build | Docker, per-min billing | “Compile tests” | Concurrent 20 |
| **CodeDeploy EC2** | Blue/green | AppSpec hooks | “Zero-downtime” | Instances 10 000 |
| **CodePipeline** | CI/CD | Stages, cross-acct | “Automate deploy” | Pipelines 300 |
| **CFN StackSets** | Multi-acct deploy | Org-wide | “Baseline 30 accts” | StackSets 100 |

---

## 🚚 Migration & Hybrid  <a id="migration"></a>

| Option | When to Use | Key Features | Classic Exam Trigger | **Top Quotas** |
|---|---|---|---|---|
| **DMS Task** | Live DB move | CDC, hetero | “Oracle → Aurora” | Tasks 100 |
| **Snowball Edge** | Offline TB–PB | 80 TB, edge compute | “No fast link” | Devices 10 |
| **Snowcone** | Portable edge | 8 TB, rugged | “Remote field” | same |
| **Snowmobile** | Exabyte truck | 100 PB trailer | “DC to cloud” | 1 / Region |
| **VPN** | IPsec tunnel | 1.25 Gbps | “Secure on-prem” | VPNs/GW 100 |
| **Transit Gateway** | Hub multi-VPC | 50 Gbps | “20 VPCs + on-prem” | Attach 5 000 |
| **Direct Connect** | Dedicated fiber | 1/10/100 Gbps | “Consistent 5 ms” | Links 50 |

---

## 🤖 Machine Learning  <a id="ml"></a>

| Option | When to Use | Key Features | Classic Exam Trigger | **Top Quotas** |
|---|---|---|---|---|
| **SageMaker Training** | Train models | Spot, autoscale | “Train XGB 100 GB” | Jobs 250 |
| **SageMaker Inference** | Real-time endpoint | Multi-model, autoscale | “Low-latency pred” | Endpoints 200 |
| **SageMaker Notebook** | Dev notebook | Jupyter + lifecycles | “Data scientist IDE” | Notebooks 10 |
| **Bedrock** | GenAI API | Foundation models, RAG | “Generate content” | — |
| **AI APIs** | Pre-built AI | Rekog, Comprehend | “Detect faces” | TPS varies |

---

## 🌍 Disaster-Recovery (DR) Patterns  <a id="dr"></a>

| Strategy | When to Use | Key Characteristics | Classic Trigger | **RTO / RPO** |
|---|---|---|---|---|
| **Backup & Restore** | Lowest cost, tolerant downtime | S3/Glacier backups, IaC rebuild | “Accept hours-day downtime” | RTO 24 h • RPO 24 h |
| **Pilot Light** | Core services always up | Minimal DB/AMI idling | “Critical DB up, app off” | RTO < hrs • RPO < hrs |
| **Warm Standby** | Scaled-down full stack | Small fleet in DR region | “App at 10 % in DR” | RTO < 1 h • RPO < min |
| **Multi-Site / Hot-Standby** | Active-active | Route 53 latency, Aurora Global | “Sub-sec failover” | RTO < mins • RPO ≈ 0 |

_Backup → S3/Glacier, CFN • Pilot Light → small RDS + AMI • Warm Standby → ASG min-size ↓ • Multi-Site → Global Accelerator, Aurora Global …_

---

> ### 🛡️ Shared-Responsibility Rule-of-Thumb  
> **AWS → “OF”** (⚙️ Facilities, HW, Network, Hypervisor)   **You → “IN”** (🔐 Data, IAM, OS patches, App code)

### Shared Responsibility Model – “OF / IN” Cheat Table

| Responsibility | Easy Mnemonic | What it really covers | Example exam take-aways |
|----------------|--------------|-----------------------|--------------------------|
| **AWS is responsible _for everything_ “OF the cloud”** | **OF** = **O**range-shirt techs (facilities) + **F**oundational infra | • Physical data-centers & perimeter security<br>• Power, cooling, fire suppression<br>• Global network backbone, fiber, routers, switches<br>• Virtualization layer (hypervisor, Nitro)<br>• Managed service infrastructure (RDS hosts, S3 storage fleet) | - AWS swaps failed disks or servers.<br>- AWS patches Xen/Nitro CVEs.<br>- AWS maintains AZ redundancy. |
| **You are responsible for what runs “IN the cloud”** | **IN** = **I**dentity / **N**itty-gritty data | • Data encryption & retention strategy<br>• IAM users, roles, MFA, keys & secrets<br>• Guest OS & package patching (EC2)<br>• Application code & business logic<br>• VPC design, SGs, NACLs, routing<br>• Compliance mapping, CloudTrail & log retention | - You enable S3 default encryption & bucket policies.<br>- You patch Ubuntu on EC2 (or use SSM Patch Manager).<br>- You decide if CloudTrail is multi-Region & sent to a secure bucket. |

---

## 🗝️ Acronym Key  <a id="acronyms"></a>

| Acronym | Meaning |
|---------|---------|
| **ACU** | Aurora Capacity Unit |
| **ALB** | Application Load Balancer |
| **AMI** | Amazon Machine Image |
| **ASG** | Auto Scaling Group |
| **AZ** | Availability Zone |
| **BYOI** | Bring Your Own IP |
| **CDC** | Change Data Capture |
| **CFN** | AWS CloudFormation |
| **CMK** | Customer-Managed KMS Key |
| **DAX** | DynamoDB Accelerator |
| **DLQ** | Dead-Letter Queue |
| **DR** | Disaster Recovery |
| **EBS** | Elastic Block Store |
| **EC2** | Elastic Compute Cloud |
| **ECR** | Elastic Container Registry |
| **ECS** | Elastic Container Service |
| **EFS** | Elastic File System |
| **ENA** | Elastic Network Adapter |
| **ENI** | Elastic Network Interface |
| **EOL** | End of Life |
| **EOT** | Encryption at Rest |
| **FaaS** | Function-as-a-Service |
| **FIS** | Fault Injection Simulator |
| **HA** | High Availability |
| **IAM** | Identity & Access Management |
| **IRSA** | IAM Roles for Service Accounts (EKS) |
| **KMS** | Key Management Service |
| **MFA** | Multi-Factor Authentication |
| **NAT** | Network Address Translation |
| **NLB** | Network Load Balancer |
| **OU** | Organizational Unit |
| **RCU / WCU** | Read / Write Capacity Unit (DynamoDB) |
| **RDS** | Relational Database Service |
| **RI** | Reserved Instance |
| **RPO** | Recovery Point Objective |
| **RTO** | Recovery Time Objective |
| **S3** | Simple Storage Service |
| **SCP** | Service Control Policy |
| **SSM** | Systems Manager |
| **TGW** | Transit Gateway |
| **VPC** | Virtual Private Cloud |
| **VPCE** | VPC Endpoint |
| **WAF** | Web Application Firewall |

---

✅ **End of Cheat Sheet**
