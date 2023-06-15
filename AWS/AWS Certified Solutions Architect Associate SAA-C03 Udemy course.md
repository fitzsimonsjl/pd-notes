#Udemy #Cloud #AWS #SAA-C03 #Cert

# Introduction

### What is AWS? 
- Cloud provider 
- Provide servers and services for use on-demand that can scale easily
- Powers some of the biggest websites in the world - Amazon, Netflix

# Getting started with AWS

## Cloud overview - Regions & AZ
- Launched internally in 2002
- Idea to market to others in 2003 - launched publicly in 2004

**AWS Use Cases**
- Allows you to build sophisticated scalable applications
- Applicable to a diverse set of industries
- Enterprise IT, backup and storage, or big data analytics
- Can host a website or use as a backend for mobile and social apps

**Global Infrastructure**

AWS Regions (and choosing one):
- Compliance
- Proximity
- Available services (not every region has every service)
- Pricing (varies by region)

AWS Availability Zones
- Each region has many availability zones (usually 3, min is 3, max is 6)
AWS Data Centers

AWS Edge Locations / Points of Presence:
- 400+ PoP
- 400+ Edge Locations & 10 Regional Caches in 90 cities across 40+ countries

**Tour AWS Console**
AWS has global services such as:
- Identity & Access Management (IAM)
- Route 53 (DNS)
- CloudFront (Content Delivery Network)
- WAF (Web Application Firewall)

Most AWS services are region-scoped:
- Amazon EC2 (IaaS)
- Elastic Beanstalk (PaaS)
- Lambda (FaaS)
- Rekognition (SaaS)

# IAM & AWS CLI

**IAM: Users, Groups, Policies**

IAM = Identity and Access Management - a Global service
Root account created by default shouldn't be used or shared

IAM Permissions
- Users or Groups can be assigned with JSON policies
- Define permissions for users
- Principle of Least Privilege
- Use IAM user for course unless otherwise specified

## IAM Policies
- Inherits at group level 
- Can specify an inline policy for users 

## IAM Policy Structure
Consists of:
- Version: policy language version (required)
- ID: an identifier for the policy (optional)
- Statement: one or more individual statements (required)

Statements consist of:
- Sid: identifier for the statement (optional)
- Effect: whether the statement allows or denies access (Allow, Deny)
- Principal: account/user/role which the policy applies to
- Action: list of actions the policy allows or denies
- Resource: list of resources to which the actions applied to
- Condition: conditions for when this policy is in effect (optional)

## IAM MFA Overview
We have two ways to protect user accounts:

**Password policy**
- Set a required password length
- Require specific characters
- Allow IAM users to change their own passwords
- Require users to change their password after some time 
- Prevent password re-use

**MFA**
- Virtual MFA device (e.g. Authenticator App)
- Security Key (e.g. Yubikey)
- Hardware Key Fob MFA Device
- Hardware Key Fob MFA Device for AWS GovCloud (US)
- You can register up to 8 MFA devices per account 
- Upon initial setup you need to enter 2 MFA codes for AWS to verify that the authenticator has been correctly set up

## AWS Access Keys, CLI, and SDK
You can access AWS in three ways:

- AWS Management Console (protected by password + MFA)
- AWS CLI (protected by access keys)
- AWS SDK (for code, protected by access keys)

Access keys are generated through the AWS console
Users manage their own access keys
Access keys are secret like a password - don't share them
Access Key ID = username essentially

**AWS CLI**
- A tool enabling you to interact with AWS services using commands in your shell
- Direct access to the public APIs of AWS services
- Can develop scripts to manage your resources
- Open source (https://github.com/aws/aws-cli)
- Alternative to using AWS Management Console

**AWS SDK**
- AWS Software Development Kit
- Language-specific APIs
- Enables you to access and manage AWS services programmatically
- Embedded in your application
- Supports many languages, also available for Mobile SDKs and IoT devices

## Creating an Access Key
- Head to IAM in the Console and click "Create Access Key"
- Choose the use case from the multiple choice menu (e.g. CLI), then Next
- Copy the access key and then run aws configure in the terminal
- You will then be asked to enter the Access Key ID and the Secret access key
- Give a default region name (pick where is closest to you e.g. eu-west-1)
- Default output format (press enter for none)

## AWS CloudShell
- Same as terminal (AWS CLI) but directly from the AWS Console instead)

## IAM Roles for AWS Services
- Some AWS services will need to perform actions on your behalf
- To do so we will assign permissions to AWS service with IAM Roles 

## IAM Security Tools
- IAM Credentials Report (account-level) - report that lists all your account's users and the status of various creds
- IAM Access Advisor (user-level) - shows the service permissions granted to a user and when those services were last accessed. Can use this information to revise policies

## IAM Guidelines & Best Practices
- Do not use the root account except for AWS account setup
- One physical user = One AWS user
- Assign users to groups and assign permissions to groups
- Create a strong password policy
- Use and enforce the use of MFA
- Create and use Roles for giving permissions to AWS services
- User Access Keys for Programmatic Access (CLI/SDK)
- Audit permissions of your account using IAM Credentials Report & IAM Access Advisor
- Never share IAM users & Access Keys

# EC2 Fundamentals

## AWS Budget Setup
If we want a general overview we can use the dashboard to drill into where our charges are and which service is responsible for them (so we can stop/delete anything we have left running).

To explicitly set budgets, we can use the "Budgets" option under Cost Management from the left-hand menu.

## EC2 Basics
- One of the most popular AWS offerings
- EC2 = Elastic Compute Cloud (IaaS)
Consists of:
  - Renting VMs (EC2 instances)
  - Storing data on virtual drives (EBS)
  - Distributing load across machines (ELB)
  - Scaling services using an auto-scaling group (ASG)

**EC2 sizing and configuration options**
- OS (Linux, Windows, or macOS)
- How much compute powers and cores (CPU)
- How much RAM
- How much storage (Network attached: EBS & EFS OR Hardware attached: EC2 Instance Store)
- Network card: speed, Public IP
- Firewall rules: security group
- Bootstrap script (configure at first launch): EC2 User Data

**EC2 User Data**
- Possible to bootstrap our instances using an EC2 User data script
- Bootstrapping means launching commands when a machine starts (same as Azure Custom Script Extension)
- Used to automate boot tasks such as installing software updates, installing software, download common files from the internet
- Script runs as root user

**EC2 instance types example**
![[Pasted image 20230519104651.png]]

t2.micro is part of the AWS free tier (up to 750 hours per month)

## EC2 Instance Types
We can use different types of EC2 instances optimised for different use cases (https://aws.amazon.com/ec2/instance-types). Optimisations include:

**General Purpose**: 
- Great for a diversity of workloads such as web servers or code repos
- Balance between compute, memory, and networking
- In the course we'll be using t2.micro which is a General Purpose EC2 instance

**Compute Optimised**:
- Great for compute-intensive tasks that require high performance processors like 
- Batch processing workloads
- Media transcoding
- High performance web servers
- High performance computing (HPC)
- Scientific modelling and machine learning
- Dedicated gaming servers

**Memory Optimised:**
- Fast performance for workloads that process large data sets in memory
- High performance, relational/non-relational databases
- Distributed web scale cache stores
- In-memory databases optimised for BI
- Applications perofmring real-time processing of big unstructured data

**Accelerated Computing**

**Storage Optimised**:
- Great for storage intensive tasks that require high sequential read and write access to large data sets on local storage
- High frequency online transaction processing (OLTP) systems
- Relational and NoSQL databases
- Cache for in-memory databases (e.g Redis)
- Data warehousing applications
- Distributed file systems

**Instance Features**

**Measuring Instance Performance**

AWS has the following naming convention:

m5.2xlarge

m = instance class
5 = generation (AWS improves them over time)
2xlarge = size within the instance class

## Security Groups & Classic Ports
- Fundamental of network security in AWS
- Control how traffic is allowed into or out of our EC2 instances
- Security groups only contain allow rules
- Security groups rules can reference by IP or by security group

**Deeper Dive**
Security groups act as a "firewall" on EC2 instances. They regulate:
- Access to ports
- Authorised IP ranges - IPv4 and IPv6
- Control of inbound network
- Control of outbound network

**Good to know**
- Security groups can be attached to multiple instances
- Can be locked down to a region /VPC combination
- Does live "outside" the EC2 - if traffic is blocked the EC2 instance won't see it
- Good to maintain one separate security group for SSH access
- If your application is not accessible (timeout) then it is a security group issue
- If your application gives a "connection refused" error, then it's an application error or it isn't launched
- All inbound traffic is blocked by default
- All outbound traffic is authorised by default

## EC2 Instance Connect
Like Bastion but not as fancy...

## Instance Roles
- Can use the above to run commands in our shell e.g. aws iam list users (to see roles etc)
- It might say it isn't possible because we have no credentials configured. To fix this, run aws configure - however this should be done via IAM roles - do not pass keys in directly!

## EC2 Instance Purchasing Options
On Demand - (short workload, predictable pricing, pay by second): 
- Pay for what you use 
- Linux or Win - billing per second after first minute
- All other OS billing per hour
- Has highest cost but no upfront payment
- No long-term commitment
- Recommended for short term and uninterrupted workloads where you can't predict how application will behave

Reserved - (1 & 3 years), Reserved instances for long workloads, Convertible reserved instances long workloads but more flexible:
- Up to 72% discount compared to on-demand
- You reserve a specific instance attributes (Instance type, region, tenancy, OS)
- Reservation Period - 1 year (+) or 3 years (+++)
- Payment options - No up front, partial, or all
- Reserved instances scope - Regional or Zonal
- Recommended for steady state usage applications e.g. DB
- Can buy and sell in Reserved Instances Marketplace
- Convertible reserved: can change instance type, family, os, scope, tenancy -  up to 66% discount

Savings Plans (1 & 3 years): - commitment to an amount of usage, long workload:
- Get a discount based on long-term usage (up to 72% same as RIs)
- Commit to a certain type of usage
- Usage beyond EC2 savings plan billed at on-demand price
- Locked to a specific instance family and AWS Region
- Flexible across instance size and OS

Spot: short workloads, cheap, can lose instances (less reliable):

- Can get a discount of 90% compared compared to on demand
- Instances that you can "lose" at any point in time if your max price is less than current spot price
- Most cost efficient instances in AWS
- Useful for workloads resilient to failure (batch jobs, data analysis, image processing, distribute workloads)
- Not suitable for critical jobs or databases

Dedicated Hosts: book an entire physical server, control instance placement:
- Physical server with EC2 instance capacity fully dedicated to your use
- Allows you to address compliance requirements and use your existing server-bound software licenses
- Purchasing options are on-demand or reserved
- Most expensive option
- Useful for software that has a complicated licensing model or for companies with strong regulatory or compliance needs

Dedicated instances: no other customers will share your hardware:
- May share hardware with other instances in same account
- No control over instance placement (can move hardware after stop/start)

Capacity Reservations: reserve capacity in a specific AZ for any duration:
- Always have access to EC2 capacity when needed
- No time commitment, but no billing discounts
- Combine with Regional Reserved Instances and Savings Plans to benefit from billing discounts
- Charged at on-demand rate whether you run out of instances or not
- Suitable for short-term uninterrupted workloads that needs to be in a specific AZ

## Spot Instances & Spot Fleet
- Can get a discount of up to 90% compared to on-demand
- Define max spot price and get the instance while current spot price < max
- If the hourly spot price > your max price, you can choose to stop or terminate instance with 2 min grace period
- Alternative strategy: Spot Block - "block" a spot instance during specified timeframes (1-6 hours). No longer offered as of December 31 2022!

**Terminating spot instances**

Create request, specifying:
- Max price
- Dedicated no. of instances
- Launch specification
- Request type (one time or persistent)
- Valid from, valid until

Request is either started, or failed. When it comes to terminating it, you can only do so if the request is open, active, or disabled. This means the process is cancel spot request --> terminate associated spot instances 

**Spot fleets**
- A set of spot instances + (optional) on demand instances
- Spot fleet will try met the target capacity with price constraints
   - Define possible launch protocols: instance type, OS, AZ
   - Can have multiple launch pools so fleet can choose
   - Spot fleet stops launching instances when reaching capacity or max cost
Strategies to allocate spot instances:
- lowestPrice: from the pool with the lowest price (cost optimisation, short workload)
- diversified: distributed across all pools (great for availability, long workloads)
- capacityOptimised: pool with the optimal capacity for number of instances
- priceCapacityOptimised: (recommended) pools with highest capacity available, then select pools with the lowest price
- Spot fleets allow us to automatically request spot instances with the lowest price

# EC2 - SAA Level
## Private vs Public vs Elastic IP
Public:
- accessible over the internet
- Must be unique across entire web
- Can be geo-located easily

Private IP:
- Only accessible within your private network
- IP must be unique across the private network
- Two different private networks (two companies) can have the same IPs
- Machines connect to WWW using a NAT + internet gateway (a proxy)
- Only a specified range of IPs can be used as a private IP

Elastic:
- When you stop and start an EC2 instance it can change its public IP
- IF you need a fixed public IP for your instance, then you need an Elastic IP
- An Elastic IP is a public IPv4 you own as long as you don't delete it
- Can attach it to one instance at a time
- Can mask failure of an instance or software by rapidly remapping the address to another instance in your account
- Can only have 5 elastic IPs in your account (ask AWS to increase)
- Overall, try avoid using them

## EC2 Placement Groups
Sometimes you want control over the EC2 instance placement strategy. When you create a placement group you specify one of the following strategies:

Cluster: 
- clusters instances into a low-latency group in a single AZ
- Higher risk, but low latency. Good for large data jobs that need completing quickly

Spread: 
- spreads instances across underlying hardware (max 7 instances per group per AZ) - critical applications

Pros: 
- Can span across Availability Zones
- Reduced risk is simultaneous failure
- EC2 Instances are on different physical hardware

Cons:
- Limited to 7 instances per AZ per placement group


Partition: spreads instances across many different partitions (which rely on different sets of racks) within an AZ. Scales to 100s of EC2 instances per group.
- Up to 7 partitions per AZ
- Can span across multiple AZs in same region
- Up to 100s of EC2 instances
- Instances in a partition do not share racks with instances in other partitions
- A partition failure can affect many EC2 but won't affect other partitions
- EC2 instances get access to the partition information such as metadata

## Elastic Network Interfaces
- Logical component in a VPC that represents a virtual network card
The ENI can have the following attributes:
- Primary private IPv4 - one or more secondary
- One Elastic IP (IPv4) per private IPv4
- One Public IP
- One or more security groups
- A MAC address
- Can create ENI independently and attach them on the fly (move them) on EC2 instances for failover
- Bound to a specific availability zone

## EC2 Hibernate
We already know we can stop and terminate instances
- Stop: data on disk (EBS) is kept intact for next start
- Terminate: any EBS volumes (root) also set-up to be destroyed are lost

On start the following happens:
- First start: OS boots & EC2 User Data script is run
- Following starts: OS boots
- Application starts, caches warm up

To alleviate some of this, we have EC2 Hibernate...
- In memory RAM state is preserved
- Instance boot is much faster (OS is not stopped/restarted)
- RAM state is written to a file in the root EBS volume
- Root EBS volume must be encrypted

Use cases:
- Long running processesing
- Saving the RAM state
- Services that take time to initialise


**Good to know**
- Supported instance families: C3, C3, C5, 13, M3, M4, R3, R4, T2, T3
- Instance RAM Size - must be less than 150GB
- Instance size - not supported for bare metal instances
- AMI - Amazon Linux 2, Linux AMI, Ubuntu, RHEL, CentOS, Win
- Root Volume - must e EBS, encrypted, not instance store, and large
- Available for On-Demand, Reserved, and Spot instances
- Hibernation meant to be no more than 60 days

# EC2 Instance Storage

## EBS Overview
**What is an EBS Volume?**
- An EBS (Elastic Block Store) Volume is a network drive you can attach to your instances while they run
- Allows your instances to persist data even after their termination
- They can only be mounted to one instance at a time
- Bound to a specific AZ - like EC2 instances - if we want one in another AZ we need to create it separately
- Free tier: 30 GB of free EBS storage of type General Purpose SSD or Magnetic per month

**Delete on Termination Attribute**
- Controls EBS behaviour when an EC2 instance terminates
- By default the root EBS volume is deleted (attribute enabled)
- By default any *other* attached EBS volume is not deleted

## EBS Snapshots
- MAke a bauackup (snapshot) of your EBS volume at a point in time
- Not necessary to detach volume to create a snapshot, but recommended
- Can copy snapshots across AZ or Region

**Snapshot Features**
EBS snapshot archive 
- Move la Snapshot to an "archive tier" that is 75% cheaper
- Takes 24 to 72 hours to restore from archive
Recycle bin for snapshots
- Set up rules to retain deleted snapshots (retention from 1 day to 1 year)
Fast Snapshot Restore (FSR)
- Force full initialisation of snapshot to have no latency on first use (£££)

## AMI Overview
Stands for Amazon Machine Image
- A customisation of an EC2 instance
- You add your own software, config, OS, monitoring etc
- Faster boot/configuration time because all your software is prepackaged
- AMI are built for a specific region (and can be copied across regions)
You can launch EC2 instances from:
- A public AMI (AWS provided)
- Your own AMI - make and maintain yourself
- An AWS Marketplace AMI - an AMI someone else made (and potentially sells)

**AMI Process (from an EC2 instance)**
- Start an EC2 instance and customise it
- Stop the instance (for data integrity)
- Build an AMI - this will also create EBS snapshots
- Launch instances from other AMIs

## EC2 Instance Store
- EBS volumes are network drives with good but limited performance
- If you need a high-performance disk, use EC2 Instance Store
They have:
- Better IO performance
- EC2 Instance store lose their storage if they're stopped (ephemeral)
- Good for buffer/cache/Scratch data/temporary content
- Risk of data loss of hardware fails
- Backups and replication are your responsibility

## EBS Volume Types
EBS Volumes come in 6 types:

| Type | Description |
|------|--------------|
| gp2 / gp3 (SSD) | General purpose SSD volume balancing price and performance for wide variety of workloads |
| io 1 / io 2  (SSD) | Highest performance SSD volume for mission critical low-latency or high-throughput workloads |
| st 1 (HDD) | Low cost HDD volume designed for frequently accessed, throughput intensive workloads |
| sc 1 (HDD) | Lowest cost HDD volume designed for less frequently accessed workloads |

- EBS Volumes characterised in size  | throughput | IOPS 
- When in doubt always consult AWS docs
- Only gp2/gp3 volumes and io 1 and io 2 can be used as boot volumes

**EBS Volume Types Use cases**
General purpose SSD:
- Cost effective storage, low latency
- System boot volumes, Virtual Desktops, Development and test environments
- 1GB-16TB
GP3:
- Baseline of 3000 IOPS and throughput of 125MiB/s
- Can increase IOPS up to 16000 and throughput up to 1000 MiB/s independently
GP2:
- Small GP2 volumes can burse IOPS to 3000
- Size of the volume and IOPS are linked, max is 16000
- 3 IOPS per GB means 5,334 GB is max
Provisioned IOPS (PIOPS) SSD
- Critical business applications with sustained IOPS performance - or applications that need more htan 16000 IOPS
- Great for database workloads (sensitive to storage perf and consistency)
io 1/ io 2:
- 4GB - 16TB
- Max PIOPS: 64,000 for Nitro EC2 instances & 23,000 for other
- Can increase PIOPS independently from storage size
- io2 have more durability and more IOPS per GB (at same price as io 1)
io2 Block Express:
- 4GB - 64TB
- Sub-millisecond latency
- Max PIOPS: 256,000 with an IOPS:GB ration of 1,000:1
- Supports EBS Multi-attach
HDDs:
- Cannot be a boot volume
- 125GB to 16TB
- Throughput optimised HDD (st 1)
- Big data, Data Warehouses, Log Processing
- Max throughput 500MiB/s - max IOPS 500
Cold HDD (sc 1):
- For data that is infrequently accessed
- Scenarios where lowest cost is important
- Max throughput 250MiB/s - Max IOPs 250

## EBS Multi-attach - io 1/ io2 family
- Attach the same EBS volume to multiple EC2 instances in the same AZ
- Each instance has full read/write perms to the high-performance volume
Use case:
   - Achieve higher application availability in clustered Linux applications 
   - Applications must manage concurrent write operations
- Up to 16 EC2 instances at a time
- Must use a file system that's cluster aware (not XFS, EXT4 etc)

## EBS Encryption
When you create an EBS volume you get the following:
- Data at rest encrypted inside the volume
- All data in transit moving between the instance and volume is encrypted
- All snapshots are encrypted
- All volumes created from the snapshot

- Encryption and decryption are handled transparently (nothing to do)
- Encryption has a minimal impact on latency
- EBS encryption leverages keys from KMS (AES-256)
- Copying an unencrypted snapshot allows encryption
- Snapshots of encrypted volumes are also encrypted

**Encryption: encrypt an unencrypted EBS volume**
- Create an EBS snapshot of the volume
- Encrypt the EBS snapshot (using copy)
- Create a new EBS volume from the snapshot (the volume will also be encrypted)
- Now you can attach the encrypted volume to the original instance

## Amazon Elastic File System (EFS)
- Managed NFS (network file system) that can be mounted on many EC2
- EFS works with EC2 instances in multi-AZ
- HA, scalable, expensive (3x gp2), pay per use

Use cases:
- Content Management
- Web serving
- Data sharing
- Wordpress

- Uses NFSv4.1 proto
- Uses a security group to control access to EFS
- Compatible with Linux based AMI (not Windows)
- Encryption at rest using KMS
- POSIX file system (Linux) that has a standard file API
- File system scales automatically (pay per use - no capacity planning)

**EFS - Performance & Storage Classes**
EFS Scale:
- 1000s of concurrent NFS clients, 10GB+/s throughput
- Grow to petabyte-scale network file system automatically
Performance Mode (set at EFS creation time):
- General purpose (default) - latency sensitive use cases
- Max IO - higher latency, throughput, highly parallel
Throughput Mode:
- Bursting: 1TB = 50MiB/s + burst of up to 100MiB/s
- Provisioned: set throughput regardless of storage size e.g. 1GiB/s for 1TB storage
- Elastic: automatically scales throughout up or down based on workloads (up to 3GiB/s for read and 1GiB/s for write). Good for unpredictable workloads

**Storage Classes**
Lifecycle management feature like Azure.

Two tiers:
- Standard: for frequently accessed files
- Infrequent (EFS-IA) meaning cost to retrieve, but low price to store. Can set EFS-IA with a Lifecycle Policy

Availability & Durability:
- Standard: Multi-AZ (great for prod)
- One Zone: great for dev - backup enabled by default, compatible with IA (EFS one-zone IA)
- over 90%  in cost savings

## EBS vs EFS - Elastic Block Storage
EBS:
- One instance (except multi-attach io 1/io2)
- are locked to the AZ level
- gp2: IO increases if disk size increases
- io 1: can increase IO independently
To migrate EBS volume across AZ:
- Take snapshot
- Restore snapshot to another AZ
- EBS backups use IO and you shouldn't run them while your application is handling a lot of traffic

- Root EBS volumes of instances get terminated by default if EC2 instance gets terminated (can be changed)
**Elastic File System**
- Mounting of 100s of instances across AZ
- EFS share website files (Wordpress)
- EFS has higher price than EBS
- Can leverage EFS-IA for cost savings
- Remember EFS vs EBS vs Instance Store

# HA & Scalability: ELB & ASG

## HA & Scalability
Scalability means that an application/system can handle greater loads by adapting. There are two kinds of scalability:
- Vertical
- Horizontal (elasticity)
Linked but different to HA

**Vertical**
- Increasing size of instance
- Scaling app vertically means moving from t2.micro to t2.large
- Vertical scaling common for non-distributed systems such as a DB
- RDS, ElastiCache are both services that can scale vertically
- Usually a limit to how much you can vertically scale (hardware)

**Horizontal**
- Means increasing number of instances/systems for your application
- Implies distributed systems
- Common for web apps
- Easy to horizontally scale thanks to things like EC2

**HA**
- Usually goes hand-in-hand with horizontal scaling
- HA means running your app/system in at least two data centers (AZ)
- Goal of HA is to survive data center loss
- HA can be passive (e.g. RDS Multi AZ)
- HA can be active (horizontal scaling)

**HA & Scalabilty for EC2**
- Vertical: Increase instance size (scale up/down)
- Horizontal (scale in/out) - Auto Scaling Group. LB
- HA: Run instances of same app across multi AZ (ASG multi-AZ, LB multi-AZ)

## Elastic Load Balancer (ELB) Overview
Load Balancers are servers that forward traffic to multiple servers (e.g. EC2 instances) downstream

Why use a Load Balancer`?
- Spread load across multiple instances
- Expose a single point of access (DNS) to your app
- Seamlessly handle failures of downstream instances
- Do regular health checks on your instances
- Provide SSL termination (HTTPS) for your websites
- Enforce stickiness with cookies
- HA across zones
- Separate public and private traffic

Why use an Elastic Load Balancer?
- Is a managed LB that AWS guarantees will be working
- AWS takes care of upgrades, maintenance and HA
- Only a small amount of config you can do
- Costs less to set up your own but a lot more effort
- Integrated into many AWS offerings/services such as:
   - EC2, EC2 ASG, Amazon ECS
   - AWS Certificate Manager (ACM), CloudWatch
   - Route 53, AWS WAF, AWS Global Accelerator

**Health Checks**
- Crucial for Load Balancers
- Enable LB to know if instances it forward traffic to are available to reply with requests
- Health check is done on a port (4567) and route (/health is common)
- If instance doesn't respond with 200, is deemed unhealthy

**Types of LB on AWS**
There are 4 types of managed LB:
- Classic LB (v1 - 2009) supporting HTTP, HTTPS, TCP, SSL (secure TCP). Recommended to not use
- Application (v2 - 2016) supporting HTTP, HTTPS, WebSocket
- Network (v2 - 2017) supporting TCP, TLS (secure TCP), and UDP
- Gateway (2020) that operates at L3 - IP protocol

Generally you should use the newer generation LBs as they provide more features. Some LBs can be set up as internal (private) or external (public).

**LB Security Groups**

Load Balancer Security Group:

| Type | Protocol | Port Range | Source | Description |
|-------|-----------|--------------|--------|--------------|
| HTTP | TCP | 80 | 0.0.0.0/0 | Allow HTTP from... |
| HTTPS | TCP | 443 | 0.0.0.0/0 | Allow HTTPs from... |

Application Security Group: Allow traffic only from LB:

| Type | Protocol | Port Range | Source | Description |
|------|-----------|--------------|--------|--------------|
| HTTP | TCP | 80 | sg-xxxxx | Allow traffic only... |

## Application LB (v2)
- Is an L7 LB (HTTPS)
- Load balancing to multiple HTTP apps across machines (target groups)
- Load balancing to multiple applications on the same machine (e.g. containers)
- Support for HTTP/2 and WebSocket
- Supports redirects (from HTTP to HTTPS for example)

Routing tables to different target groups (user defined routes in Azure):
- Routing based on path in URL
- Routing based on hostname in URL
- Routing based on Query String, Headers

ALB are:
- A great fit for microservices and containerised apps like Docker or Amazon ECS
- Has a port mapping feature to redirect to a dynamic port in ECS
- In comparison we would need multiple CLBs per app

Target groups:
- EC2 instances (can be managed by an Auto Scaling Group) - HTTP
- ECS tasks (managed by ECS itself) - HTTP
- Lambda functions - HTTP requests translated into a JSON event
- IP addresses - must be private IPs
- ALB can route to multiple target groups
- Health checks are at target group level

**Good to know**
- Fixed hostname (e.g. xxx.region.elb.amazonaws.com)
- Application servers don't see IP of client directly:
- True IP of client is inserted in header X-Forwarded-For
- Can also get port (X-Forwarded-Port) and Proto (X-Forwarded-Proto)

## Network Load Balancer (v2)
Network Load Balancers (L4) allow you to:
- Forward TCP and UDP traffic to your instances
- Handle millions of requests per second
- Less latency (around 100ms vs 400ms for an ALB)
- NLB has one static IP per AZ and supports assigning Elastic IP (helpful for whitelisting specific IP)
- NLB are used for extreme performance, TCP, or UDP traffic
- They are not included in the AWS free tier

**Network Load Balancer - Target Groups**
- EC2 Instances
- IP Addresses - must be private
- Application Load Balancer (NLB is in front of it)
- Health checks support TCP, HTTP, and HTTPs protos

## Gateway Load Balancer
- Deploy, scale, and manage a fleet of 3rd party network virtual appliances in AWS e.g. Firewalls, IDPS, Deep Packet Inspection Systems, Payload manipulation etc
- Operates at L3 (Network layer) - IP Packets
- Combines a Transparent Network Gateway - single entry/exit for all traffic and a Load Balancer that distributes traffic to your virtual appliances
- **Uses GENEVE protocol on port 6081**

**Gateway Load Balancer - Target Groups**
- EC2 Instances
- IP Addresses - must be private

## Sticky Sessions (Session Affinity)
- Is possible to implement stickiness so that the same client is always redirected to same instance behind LB
- Works for CLB, ALB, and NLB
- The "cookie" used for stickiness has an expiration date you control
- Enabling stickiness may introduce an imbalance to the load over the backend EC2 instances

**Cookie Names**
There are two types we can use - 

Application based cookies:
Custom cookie generated by the target (your application)
- Can include any custom attributes required by the application
- Cookie name must be specified individually for each target group
- Don't use AWSALB, AWSALBAPP or AWSALBTG (these names are reserved for use by the ELB)
Application cookie:
- Generated by the LB
- Cookie name is AWSALBAPP

Duration based cookies:
- Cookie generated by the LB
- Cookie name is AWSALB for ALB, AWSELB for CLB

## Elastic Load Balancer - Cross Zone Load Balancing

With Cross Zone Load Balancing, each load balancer instance distributes evenly across all registered instances in all AZ

Without Cross Zone Load Balancing, requests are distributed in the instances of the node of the Elastic Load Balancer

ALB:
- Enabled by default (can be disabled at the Target Group level)
- No charges for inter AZ data

NLB & GLB:
- Disabled by default
- You pay charges for inter AZ data if enabled

CLB:
- Disabled by default
- No charges for inter AZ data if enabled

## Elastic Load Balancer - SSL Certs
- SSL Cert allows traffic to be encrypted between your clients and LB to be encrypted in transit
- SSL refers to Secure Sockets Layer
- TLS refers to Transport Layer Security (newer version)
- TLS mainly used, but still referred to as SSL
- Public SSL certs are issued by CAs
- SSL certs have an expiration date that you set and must be renewed

- LB uses an X.509 certificate
- Can manage certs using ACM (AWS Certificate Manager)
- Can create and upload your own certificates as an alternative
HTTPS listener:
- Must specify a default certificate
- Can add an optional list of certs to support multiple domains
- Clients can use Server Name Indication (SNI) to specify hostname they reach
- Ability to specify a security policy to support older versions of SSL/TLS (legacy clients)

**SSL - Server Name Indication (SNI)**
- SNI solves the problem of loading multiple SSL certs onto one web server (to serve multiple sites)
- Is a newer protocol that requires the client indicate the hostname of the target server in the initial SSL handshake
- The server will find the correct cert or return the default one
- This only work for ALB & NLB (newer gen), and CloudFront - doesn't work for CLB

Classic Load Balancer (v1)
- Supports only one SSL cert
- Must use multiple CLB for multiple hostnames with multiple SSL certs

Application Load Balancer (v2)  and Network Load Balancer (v2)
- Supports multiple listeners with multiple SSL certs
- Uses SNI to make it work

## Elastic Load Balancer - Connection Draining
- Named Connection draining for CLB
- Named Deregistration delay for ALB & NLB
- Gives time to complete requests while instance is de-registering or unhealthy
- Stops sending new requests to the EC2 instance which is de-registering
- Can be set to between 1 and 3600 seconds (default is 300 seconds)
- Can be disabled (by setting value to 0)
- Set a low value if requests are short

## Auto Scaling Groups Overview
Matches to Virtual Machine Scale Sets (VMSS) in Azure!

Load on websites and applications can change. In the cloud it is possible to create and remove servers quickly. The goal of an Auto Scaling Group is to:
- Scale out (add EC2 instances) to match an increased load
- Scale in (remove EC2 instances) to match a decreased load
- Ensure we have a minimum and a maximum number of EC2 instances running
- Automatically register new instances to a load balancer
- Re-create an EC2 instance in case a previous one is terminated (e.g. if unhealthy)
- ASG are free (you only pay for the underlying EC2 instances)

**ASG Attributes**
Consists of a Launch Template:
- AMI + Instance Type
- EC2 User Data
- EBS Vols
- Security Groups
- SSH key pair
- IAM Roles for your EC2 instances
- Network + subnets information
- Load Balancer info

We can also define a min/max size as well as an initial capacity

**Auto Scaling - CloudWatch Alarms and Scaling**
- Possible to scale an ASG based on CloudWatch Alarms
- An alarm monitors a metric (like Average CPU, or a custom one you define)
- Metrics such as Average CPU are computed for the overall ASG instances
Based on the alarm we can create:
- Scale-out policies (increase no. of instances)
- Scale-in policies (decrease no. of instances)

## ASG - Dynamic Scaling Policies
Target Tracking Scaling:
- Most simple and easy to set up
- For example: I want the average ASG CPU to stay around 40%

Simple/Step Scaling:
- When a CloudWatch  alarm is triggered (e.g. CPU > 70%) then add 2 units
- When a CloudWatch alarm is triggered (e.g. CPU < 30%), remove 1 unit

Scheduled Actions:
- Anticipate scaling based on known usage patterns (e.g. increase min capacity to 10 at 5pm on Fridays)

**Predictive Scaling**
- Continuously forecast load and schedule scaling ahead

**Good metrics to scale on**

CPUUtilization: Average CPU util across your instances
RequestCountPerTarget: to make sure the number of requests per EC2 instances is stable
Average Network In/Out: if your application is network bound
Any custom metric: that you push using CloudWatch

**ASGs - Scaling Cooldowns**
- After a scaling activity happens, you are in the cooldown period (300 seconds by default)
- During cooldown period, ASG will not launch or terminate additional instances (to allow metrics to stabilise)
- Some advice: use a ready-to-use AMI to reduce config time in order to be serving requests faster and reduce cooldown period

# AWS Fundamentals: RDS + Aurora + ElastiCache

### Amazon RDS Overview
RDS stands for Relational Database Service
- Is a managed DB service using SQL as query language
- Allows you to create DBs in the cloud managed by AWS
- Supports Pg, MSQL, MariaDB, Oracle, MSSQL, Aurora (AWS proprietary DB)

### Advantage using RDS over DB on EC2

Because RDS is managed it means:
- Automated provisioning, OS Patching
- Continuous backups and restore to specific timestap (Point in Time Restore)
- Monitoring Dashboards
- Read replicas for improved read performance
- Multi AZ setup for DR
- Maintenence windows for upgrades
- Scaling capability (vertical and horizontal)
- Storage backed by EBS (gp2 or io 1)
- You cannot SSH into your instances!

### RDS Storage Auto Scaling
- Helps you increase storage on RDS DB instance automatically
- When RDS detects you are running out of free DB storage, it scales automatically
- Avoid manually scaling your database storage
- Have to set a Maximum Storage Threshold
Automatically modify storage if:
- Free storage is less than 10% of allocated storage
- Low-storage lasts at least 5 minutes
- 6 hours have passed since last modification
- Supports all RDS DB engines

# RDS Read Replicas vs Multi AZ

### RDS Read Replicas for read scalability
- Up to 15 Read Replicas
- Can be within an AZ, Cross AZ, or Cross region
- Replication is async so reads are eventually consistent
- Replicas can be promoted to their own DB
- Applications must update the connection string the leverage read replicas

### RDS Read Replicas - Use Cases
- You have a production DB that is taking on a normal load
- You want to run a reporting application to run some analytics
- You create a Read Replica to run the new workload there
- The production application is unaffected
- Read Replicas are used for SELECT statements only

### RDS Read Replicas - Network Cost
- In AWS there's network cost when data goes from one AZ to another
- For RDS Read Replicas in same region you don't pay that fee

### RDS Multi AZ (DR)
- Sync replication
- One DNS name - automatic app failover to standby
- Increase availability
- Failover in case of loss of AZ, loss of network, instance, or storage failure
- No manual intervention in apps
- Not used for scaling
- The Read Replicas can be set up as Multi AZ for DR

### RDS - Single AZ to Multi AZ
- Zero downtime operation (no need to stop DB)
- Just click "modify" for DB
Internally the following happens:
- Snapshot is taken
- A new DB is restored from the snapshot in a new AZ
- Synchronisation is established between the two DBs

# RDS Custom for Oracal & MSSQL

### RDS Custom
A managed Oracale and MSSQL DB with OS and DB customisation

RDS: Automates setup, operation, and scaling of DB in AWS

Custom: access to underlying DB and OS so that you can:
- Configure settings
- Install patches
- Enable native features
- Access underlying EC2 instance using SSH or SSM Session Manager

De-activate Automation Mode to perform customisation - better to take a snapshot before

RDS vs Custom:
- RDS: entire DB and OS managed by AWS
- RDS Custom: full admin access to underlying OS and DB

# Amazon Aurora
- Prporietary technology from AWS
- Pg & MSQL supported as Aurora DB (means drivers work as if Aurora was a Pg or MSQL DB)
- Aurora is "AWS cloud optimised" - 5x performance improvement over MSQL on RDS. Over 3x performance of Pg on RDS
- Aurora storage grows automatically in increments of 10GB up to 128TB
- Aurora can have up to 15 replicas and replication process is faster than MSQL (sub 10ms)
- Failover in Aurora instantaneous - HA
- Aurora costs more than RDS (20%) but more efficent

### Aurora HA & Read Scaling
6 copies of your data across 3 AZ:
- 4/6 needed for writes
- 3/6 needed for reads
- Self-healing with P2P replication
- Storage striped across 100s of vols

- One Aurora instance takes writes (master)
- Automated failover for master in less than 30 seconds
- Master + up to 15 Aurora Read Replicas serve reads
- Support for Cross Region Replication

### Aurora DB Cluster

Client with a:
- Writer endpoint (pointing to master)
- A reader endpoint (connection load balancing)
- Shared storage volume with all read replicas that auto-scales
- Any time client connects to reader endpoints, it gets connected to one of the read replicas
- Load balancing happens at the connection level, not the statement level

# Amazon Aurora Advanced Concepts

### Replica Autoscaling
- If the Reader endpoint is receiving too many requests, we can have other instances be substantiated automatically
- Share storage volume will also expand to correlate with it

### Custom Endpoints
- Define a subset of Aurora instances as Custom Endpoint
- Example: Run analytical queries on specific replicas
- Reader Endpoint is generally not used after defining custom endpoints (but is not removed)

### Aurora Serverless
- Automated database installation and auto-scaling based on actual usage
- Good for infrequent, intermittent or unpredictable workloads
- No capacity planning needed
- Pay per second can more cost effective
- Works on a Proxy Fleet (managed by Aurora)

### Aurora Multi-Master
- In case you want immediate failover for write node (HA)
- Every node does R/W - vs promoting a R/W as the new master

### Global Aurora
Aurora Cross Region Read Replicas:
- Useful for DR
- Simple to put in place
Aurora Global Database (recommended):
- 1 primary region (R/W)
- Up to 5 secondary (Read only) regions - replication lag less than 1 sec
- Up to 16 Read Replicas per secondary region
- Helps for decreasing latency
- Promoting another region (for DR) has an RTO of under 1 min
- Typically cross-region replication takes less than 1 sec

### Aurora Machine Learning
- Enables you to add ML-based predictions to your applications via SQL
- Simple, optimised, and secure integration between Aurora and AWS ML services
- Supported services are SageMaker (use with any ML model) and Comprehend (for sentiment analysis)
- Don't need ML experience
- Useful for fraud detection, ads targeting, sentiment analysis, or product recommendations

# RDS & Aurora - Backup & Monitoring

### RDS Backups
Automated backups:
- Daily full backup of DB (during backup window)
- Transaction logs backed up by RDS every 5 mins
- Ability to restore to any point in time (from oldest back up to 5 mins ago)
- 1 to 35 days of retention - set to 0 to disable automated backups
Manual DB snapshots:
- Manually triggered by user
- Retention of backup as long as you want

Cost saving trick: with a stopped RDS DB you still pay for storage. If you plan on stopping it for a long time, snapshot and restore instead

### Aurora Backups
Automated backups:
- 1 to 35 days (cannot be disabled)
- point-in-time recovery in that timeframe
Manual DB snapshots:
- Manually triggered by user
- Retention as long as you want

### RDS & Aurora Restore Options
- Restoring an RDS / Aurora backup or a snapshot creates a new database
- Restoring MSQL RDS database from S3:
   - Create a backup of your on-prem db
   - Store it on S3
   - Restore backup file onto new RDS instance running MSQL
- Restoring MSQL Aurora cluster from S3:
   - Create backup of on-prem db using Percona XtraBackup
   - Store backup file on S3
   - Restore backup file onto new Aurora cluster running MSQL

### Aurora Database Cloning
- Create a new Aurora DB Cluster from an existing one
- Faster than snapshot & restore
- Uses copy-on-write protocol
   - Initially new DB cluster uses same data volume as original (fast and efficient - no copying needed)
   - When updates are made to the new DB cluster data, additional storage is allocated and data is copied to be separated
- Very fast and cost effective
- Useful to create a "staging" DB from a "prod" DB without impacting Prod

# RDS Security
### RDS & Aurora Security
- At rest encryption:
   - DB master & replicas encryption using AWS KMS - must be defined at launch time
   - If master is not encrypted, read replicas cannot be encrypted
   - To encrypt an unencrypted database, go through a DB snapshot and restore as encrypted
- In-flight encryption: TLS ready by default, use AWS TLS root certs client-side
- IAM Auth: IAM roles to connect to DB instead of user/pass
- Security Groups: Control Network access to your RDS/Aurora DB
- No SSH available except on RDS custom
- Audit logs can be enabled and sent to CloudWatch for longer retention

## Amazon RDS Proxy
- Fully managed database proxy for RDS
- Allows apps to pool and share DB connections established with the database
- Improving DB efficiency by reducing the stress on DB resources (CPU, RAM) and minimize open connections and timeouts
- Serverless autoscaling, HA (multi-AZ)
- Reduced RDS & Aurora failover time by up to 66%
- Supports RDS (MSQL, Pg, MariaDB, MSSQL) and Aurora (MSQL, Pg)
- No code changes required for most apps
- Enforce IAM Auth for DB and securely store creds with AWS Secrets Manager
- RDS Proxy is never publicly accessible (must be accessed from VPC)

## ElastiCache Overview
- Same way RDS is to get managed Relational DBs
- ElastiCache is managed by Redis or Memcached
- CAches are in-mem DBs with very high performance, low latency
- Helps reduce load off of DB for read intensive workloads
- Helps make your application stateless
- AWS takes care of OS maintenance/patching, optimisations, setup, configuration, monitoring, failure recovery and backups
- Using ElastiCache involves heavy application code changes

### ElastiCache Solution Architecture - DB Cache
- Applications query ElastiCache. If not available, it gets it from RDS and stores it in ElastiCache for future use
- Helps relieve load in RDS
- Cache must have an invalidation strategy to make sure only the most current data is used

### ElastiCache Solution Architecture - User Session Store
- User logs into any of the applications
- Application writes session data into ElastiCache
- User hits another instance of our application
- Instance retrieves the data and the user is already logged in

### ElastiCache - Redis vs Memcached

**Redis (replication)**
- Multi-AZ with auto-failover
- Read replicas to scale reads and have HA
- Data Durability using AOF persistence
- Backup and restore features
- Supports Sets and Sorted Sets

**Memcached (sharding)**
- Multi-node for partitioning of data (sharding)
- No HA (replication)
- Non-persistent
- No backup and restore
- Multi-threaded architecture

### ElastiCache - Cache Security
- ElastiCache supports IAM Auth for Redis
- IAM policies on ElastiCache are only used for AWS API-level security
- Redis AUTH
   - Can set "password/token" when creating a Redis cluster
   - Extra level of security for your cache (on top of security groups)
   - Supports SSL in flight encryption
- Memcached
   - Supports SASL-based auth (advanced)

### Patterns for ElastiCache
- Lazy Loading: all the read data is cached, data can become stale in cache
- Write Through: Adds or updates data in cache when written to a DB (no stale data)
- Session Store: store temporary session data in cache (using TTL features)

### ElastiCache - Redis Use Case
- Gaming leaderboards (computationally complex)
- Redis Sorted sets (guarantee both uniqueness and element ordering)
- Each time a new element gets added, it's ranked in real time then added in correct order

# Route 53

### What is DNS?
- Translates human friendly host names into machine IP addresses
- DNS is backbone of internet
- Uses heirarchical naming structure (.com example.com www.example.com api.example.com)

### DNS Terminologies
- Domain Registrar: Amazon Route 53, GoDaddy etc
- DNS Records: A, AAAA, CNAME, NS etc
- Name Server: resolves DNS queries (Authoritative or Non-Authoritative)
- Zone File: contains DNS records
- Top Level Domain (TLD): .com, .us, .in, .gov etc
- Second Level Domain (SLD): amazon.com, google.com

### Amazon Route 53
- A HA, scalable, fully managed and Authoritative DNS (meaning the customer (you) can update the DNS records)
- Route 53 also a Domain Registrar
- Ability to check the health of your resources
- Only AWS service which provides 100% availability SLA

### Route 53 - Records
- How we want to route traffic for a domain
Each record contains:
   - Domain/subdomain Name
   - Record Type (e.g. A or AAAA)
   - Value (e.g. 12.34.56.78)
   - Routing Policy - how Route 53 responds to queries
   - TTL - amount of time the record cached at DNS Resolvers
- Route 53 supports the following DNS record types: A, AAAA, CNAME, NS, CAA, DS, MX, NAPTR, PTR, SOA, TXT, SPF, SRV

### Route 53 - Record Types
- A - maps a hostname to IPv4
- AAAA - maps a hostname to IPv6
- CNAME - maps a hostname to another hostname
   - Target is a domain name which must have an A or AAAA record
   - Can't create a CNAME record for the top node of a DNS namespace (Zone Apex)
   - Example: you can't create for example.com but you can create for www.example.com
- NS - Name Servers for the Hosted Zone
   - Control how traffic is routed for a domain

### Route 53 - Hosted Zones 
- A container for records that define how to route traffic to a domain and its subdomains
- **Public Hosted Zones**: contains records that specify how to route trafic on the internet (public domain names)
- **Private Hosted Zones**: contain records that specify how you route traffic within one or more VPCs (private domain names). You pay 50 cents per month per hosted zone

## Route 53 - Registering a domain
- Registered domains from left-hand menu
- Register new domain
- Go through availability check
- Fill in contact details
- Verify purchase
- Set auto-renewal (or not)
- Accept T&Cs

## Route 53 - Creating Records

Basically like any other provider...

## Route 53 - EC2 Setup
- 3 EC2 Instances in different regions
- Launch application load balancer in one region
- Select subnets
- Select security groups
- Forward to target group (create one, selecting instances - give it a name)
- Register the targets

## Route 53 - TTL

**High TTL - e.g. 24 hours**
- Less traffic on Route 53
- Possibly outdated records
**Low TTL - e.g. 60 seconds**
- More traffic on Route 53 (££)
- Records outdated for less time
- Easy to change records

Except for Alias records, TTL is mandatory for each DNS record!


## Route 53 CNAME vs Alias

**AWS Resources (Load Balancer, CloudFront)** 
Expose an AWS hostname (e.g lb 1-1234.us-east-2.elb.amazonaws.com and you want example.com)

**CNAME**
- Points a hostname to any other hostname
- Only for non-root domain (e.g. something.mydomain.com)

**Alias**
- Points to a hostname to an AWS Resource (app.example.com --> exex.amazonaws.com)
- Works for Root as well as non-root domain
- Free of charge
- Native health check

## Route 53 - Alias Records
- Maps a hostname to an AWS resource
- An extension to DNS functionality
- Automatically recognises changes in the resource's IP address
- Unlike CNAME, it can be used for top node of a DNS namespace (Zone Apex) e.g. example.com
- Alias record is always of type A/AAAA for AWS resources (IPv4/6)
- You can't set the TTL

## Route 53 - Alias Records Targets
- Elastic Load Balancers
- CloudFront Distributions
- API Gateway
- Elastic Beanstalk environments
- S3 websites
- VPC Interface Endpoints
- Global Accelerator accelerator
- Route 53 record in the same hosted zone
- **You can't set an alias record for an EC2 DNS name**

## Route 53 - Routing Policies 
- Define how Route 53 responds to DNS queries
- Not the same as LB routing which routes traffic
- DNS does not route any traffic - only responds to DNS queries
Route 53 supports the following routing policies:
- Simple
- Weighted
- Failover
- Geolocation
- Multi-value answer
- Geoproximity (using Route 53 traffic flow feature)

### Simple
- Typically route traffic to a single resource
- Can specify multiple values in the same record
- If multiple values are returned, a random one is chosen by the client
- When alias enabled, specify one AWS resource
- Cannot be associated with Health Checks

### Weighted
- Control the percentage of requests that go to each specific resource
- Assign each record a relative weight (traffic percentage is weight for a specific record / sum of weights or all records)
- DNS records must have the same name and type
- Can be associated with health checks
- Uses cases are load balancing between regions, testing new application versions etc
- Assign a weight of 0 to a record to stop sending traffic to a resource
- If all records have weight of 0, all records will be returned equally

### Latency
- Redirect to the resource that has the least latency closest to us
- Very helpful when latency for users is a priority
- Latency is based on traffic between users and AWS regions
- Can be associated with Health Checks (has a failover capability)

## Route 53 - Health Checks
- HTTP Health Checks are only for public resources
- Health Check --> Automated DNS Failover:
   1. Health checks that monitor an endpoint (application server, other AWS resource)
   2. Health checks that monitor other health checks (calculated health checks)
   3. Health checks that monitor CloudWatch alarms (full control) e.g. throttles of DynamoDB, alarms on RDS, custom metrics etc. Useful for private resources
- Health checks are integrated with CW metrics

### Health Checks - Monitor an Endpoint
- About 15 global health checkers will check the endpoint health
   - Health/Unhealthy Threshold - 3 (default)
   - Interval - 30 sec (can set to 10 sec - higher cost)
   - Supported protos: HTTP, HTTPS, TCP
   - If > 18% of health checkers report endpoint is health, Route 53 considers it healthy - otherwise deemed unhealthy
   - Ability to choose which locations you want route 53 to use
- Health checks pass only when the endpoint responds with 2xx or 3xx status codes
- Health checks can be set up to pass/fail based on the text in the first 5120 bytes of response
- Configure your router/firewall to allow incoming requests from Route 53 Health Checkers

### Route 53 - Calculated Health Checks
- Combines the results of multiple Health Checks into a single Health Check
- Can use OR, AND, or NOT
- Can monitor up to 256 Health Checks
- Specify how many of the health checks need to pass to make the parent pass
- Usage: perform maintenance to your website without causing all health checks to fail

### Health Checks - Private Hosted Zones
- Route 53 Health Checkers are outside the VPC
- The can't access private endpoints 
- Instead you can create a CloudWatch Metric and associate a CloudWatch Alarm. Then, create a Health Check that checks the alarm itself

## Routing Policies - Failover (Active-Passive)

1. Client sends DNS request 
2. Route 53 picks it up and routes it via primary EC2 instance (once health check has completed)
3. If health check comes back unhealthy, Route 53 directs it to the failover secondary DR EC2 instance

## Routing Policy - Geolocation
- Different from latency based!
- Routing is based on user location
- Specify location by continent, country or by US state - if there's overlap, most precise is selected
- Should create a "default" record (in case there's no match of location)
- Use cases: website localisation, restrict content distribution, load balancing
- Can be associated with health checks

## Routing Policy - Geoproximity
- Route traffic to your resources based on geographic location of users and resources
- Ability to shift more traffic to resources based on the defined bias
To change size of geographic region, specify bias values:
- To expand (1 to 99) - more traffic to the resource
- To shrink (-1 to -99) - less traffic to the resource
Resources can be:
- AWS resources (specify AWS region)
- Non-AWS resources (specify lat and long)
- Must use Route 53 Traffic Flow to use this feature

## Routing Policy - IP Based
- Routing based on client's IP addresses
- You provide a list of CIDRs for your clients and the corresponding endpoints/locations (user-ip-to-endpoint mappings)
- Use cases: optimise performance, reduce network costs
- Example: route end users from a particular ISP to a specific endpoint

## Routing Policy - Multi-value
- Use when routing traffic to multiple resources
- Route 53 returns multiple values/resources
- Can be associated with Health Checks (return only values for healthy resources)
- Up to 8 healthy records are returned for each multi-value query
- Multi-Value is **not** a substitute for having an ELB

## Third-party Domains & Route 53

### Domain Registrar vs DNS Service
- You buy or register your domain name with a Domain Registrar typically by paying annual fees
- Domain Registrar normally provides you with a DNS service to manage your DNS records
- Can use another DNS service if you wish
- E.g. purchase domain from GoDaddy and use Route 53 to manage DNS records

### Third-party Registrar with Amazon Route 53 
If you buy your domain on a third-party registrar you can still use Route 53 as DNS Service Provider:
1. Create a Hosted Zone in Route 53
2. Update NS Records on third-party website to use Route 53 Name Servers
- Domain Registrar != DNS Service
- Every Domain Registrar usually comes with some DNS features

# Classic Solutions Architecture Discussions

A way of understanding how all these technologies so far work together using the following sample case studies:
- whatisthetime.com
- myclothes.com
- mywordpress.com
- Instantiating applications quickly
- Beanstalk

## Stateless Web App: whatisthetime.com

### Background
- whatisthetime.com allows people to know what time it is
- Don't need a DB
- Want to start small and downtime is acceptable
- We want to fully scale vertically and horizontally for no downtime

### Starting simple
- We have a user and a public EC2 instance (micro.t2)
- User requests time from website, gets sent back
- We want to attach a static IP incase something happens to it - so we add an Elastic IP address

### Scaling vertically
- The app gets more popular and gains some more users
- Suddenly our micro.t2 instance isn't enough
- We need to scale it up to handle more load so we replace our t2.micro with an m5.large
- Stop the t2.micro instance, change instance type, carry on where we left off thanks to Elastic IP
- However, our users will have experienced some downtime whilst we swap the instances

### Scaling horizontally

- The app becomes even more popular so we want to scale horizontally
- To do this we add a few more m5.large instances with their own Elastic IP
- This is good because we have managed to absorb the demand, but it does mean that users need to know the particular Elastic IPs to reach our site...

So, let's take a different approach using **Route 53**...

- Instead of having users remember IPs, we remove our Elastic IPs and keep our 3 m5.large instances
- We set up Route 53 so that users query api.whatisthetime.com (as an A record with a TTL for 1 hour). 
- They can now access our application without having to remember any specific IPs
- However, if one of our instances is removed, some users will think our app is down because the 1 hour TTL is caching so they will not get a response till it expires

Let's make it a bit better using a **Load Balancer**...

- Our m5.large are now Private EC2 instances in an AZ
- We add a Load Balancer (same AZ) with Health Checks
- Our ELB is public facing with some security group rules so that the instances only get traffic from the ELB...
- Like before, our users can query Route 53, but this time it must be an Alias Record (not A) which points from Route 53 to the ELB
- Thanks to the ELB and Health Checks we won't have downtime as we add/remove instances - still, doing this manually is annoying
- To fix this, we can put our EC2 instances in an ASG that will scale in/out automatically based on demand

But what happens if there's a natural disaster in the AZ where we host our app...?

### Making our app multi-AZ
- We can specify our ELB + Health Checks are across AZ 1-3
- We can also span our ASG across AZ 1-3

If we want to go further we can:
- Set a minimum of 2 AZ and reserve capacity
- We know we want to have 2 instances running at all times, but we can make it cheaper if we used RIs
- If we really wanted to cut costs and don't mind some instances being taken back, we can even use spot instances

There are 5 pillars to consider for a well architected application:
- Cost
- Performance
- Reliability
- Security
- Operational excellence

## Stateful Web App: myclothes.com

### Background
- myclothes.com allows people to buy clothes online
- There's a shopping cart
- Website has hundreds of users at the same time
- We need to scale, maintain horizontal scalability, and keep our web app as stateless as possible
- Users should not lose their shopping cart
- Users should have their details in a DB

### Starting Point
- Users, Route 53, Multi-AZ LB, AZ 1-3 with instance in each
- However, at the moment if a user adds something their cart, but the next time they browse around the site they get directed to a different instance, their shopping cart will be lost (because the new instance doesn't have the cart)...

### Introducing Stickiness (Session Affinity)
- To fix this we can use Stickiness (Session Affinity) on our ELB
- This means that each request a particular user makes will always be routed to the same instance
- This fixes the immediate issue, but if that instance the requests are sticking to is terminated or goes down, the cart is lost again...

### Introducing User Cookies
- Rather than have the EC2 instance save the cart, let's store shopping cart contents in a cookie
- Every time it connects to the LB it will also mention it has the cookie with the cart contents - so it no longer matters which instances serves which requests
- Our EC2 instances are now stateless
- However it does mean that HTTP requests are getting heavier
- There are also some security implications (what if an attacker modifies a cookie?)
- Therefore... we must ensure that our EC2 instances are validating content they are receiving from the cookie
- And of course, the cookie must be less than 4KB

But what about a different approach?...

### Introducing Server Session
- Instead of sending a whole shopping cart in web cookies, we can just send a Session ID
- In the background we can have an ElastiCache and when we send the session ID, the EC2 instance will add the cart contents into the ElasticCache
- Now when a request goes to another instance, the ElastiCache can give it the Session ID to look up the content  and retrieve that session data
- For storing session data we can use Amazon DynamoDB as an alternative if we wish

### Storing User Data in a Database
- We talk to our EC2 instance, which is going to talk to an RDS instance
- The RDS instance can talk to each of our EC2 instances and pass them customer information

### Scaling Reads
- As we look at what our users do with our site, we notice that they do lots of reads (browsing products)
- We can make this more efficient by using an RDS Master and Read Replicas (up to 5)

### Scaling Reads (Alternative) with Lazy Loading
- A user talks to our EC2 instance
- The EC2 instance talks to the ElastiCache and says "Do you have what I'm looking for?" If it does, it gets sent back
- If it doesn't, ElastiCache will talk to the RDS and keep a copy for future use

### Multi-AZ - Surviving Disaster
- Same as before, but we make ElastiCache Multi-AZ (using Redis) and RDS Multi-AZ

### Security Groups
- For traffic coming into the load balancer we don't want to limit our customers, so we can leave it open to HTTP/HTTPS traffic
- On our LB itself, we can restrict traffic that reaches our EC2 instances
- Further on, it would be sensible to restrict traffic to only the EC2 instances for RDS and ElastiCache

## Stateful Web App: mywordpress.com

### Background
- Trying to create a fully scalable WP website
- We want that website to access and correctly display picture uploads
- Our user data and blog content should be stored in a MSQL DB

### RDS Layer
- Very similar to architecture we've seen before with Multi-AZ RDS behind EC2 instances that are spread across AZ
- If we really wanted to scale up, we could replace our multi-AZ RDS with Aurora MSQL Multi-AZ Read Replicas
- By using Aurora we get less operations and things are a bit more robust and quicker to scale

### Storing Images with EBS
- Works great for one instance, but we run into problems when scaling (because each EC2 would have its own EBS volume - causing confusion)
- Means we need to take a different approach with EFS...

### Storing Images with EFS
- We can use the exact same architecture as before, but this time, we have our Elastic File Storage attached
- The EFS will create Elastic Network Interfaces (ENI) for each of our AZs so that every EC2 instance can access it

## Instantiating Applications Quickly...
When launching a full stack (EC2, EBS, RDS) it can take time to:
- Install applications
- Insert initial (or recovery) data
- Configure everything
- Launch the application

But, we can use the cloud to speed these things up...

EC2 Instances:
- Use a Golden AMI: Install your applications, OS dependencies etc beforehand and launch your EC2 instance from it
- Bootstrap using User Data: For dynamic config, use User Data scripts
- Hybrid: mix Golden AMI and User Data (Elastic Beanstalk)
RDS Databases:
- Restore from snapshot: DB will have schemas and data ready
EBS Volumes:
- Restore from a snapshot: disk will already be formatted and have data

## Elastic Beanstalk

So far we have a pretty typical architecture:

- A Multi AZ ELB in a public subnet (user queries via Route 53)
- A private subnet containing our EC2 instances spread across AZs grouped in an ASG
- ElastiCache and RDS behind our instances in a Data Subnet

### Developer problems on AWS
- Managing Infra
- Deploying code
- Configuring DBs, LBs etc
- Scaling concerns

- Most web apps have same architecture (ALB + ASG)
- All devs want is for their code to run consistently across different applications and environments

### Beanstalk Overview
- Elastic Beanstalk is a dev centric view of deploying an application on AWS
- Uses all the components we've seen before (EC2, ASG, ELB, RDS etc)
- It's a Managed Service that:
   - Automatically handles capacity provisioning, load balancing, scaling, application health monitoring, instance config etc.
   - Only the application code is the responsibility of the developer
- We still have full control over the configuration
- Beanstalk is free but you pay for the underlying instances

### Elastic Beanstalk - Components

- Application: collection of Elastic Beanstalk components (environments, versions, configurations etc)
- Application Version: an iteration of your application code
- Environment:
   - Collection of AWS resources running an application version (only one version at a time!)
   - Tiers: Web Server Environment tier and Worker Environment tier
   - Can create multiple environments (dev, test, prod etc.)

Flow is: Create Application --> Upload Version --> Launch Environment --> Manage Environment

We can update it but creating a new version, and it becomes iterative in a loop of sorts

### Elastic Beanstalk - Supported Platforms
- Go
- Java SE
- Java with Tomcat
- .Net Core on Linux
- .Net on Windows Server
- Node.js
- PHP
- Python
- Ruby
- Packer Builder
- Single Container Docker
- Multi-Container Docker
- Preconfigured Docker

If the language you want to use is missing, you can write your own custom platform

### Web Server Tier vs. Worker Tier

**Web Environment**
- ELB
- AZs with security groups containing EC2s and an ASG

**Worker Environment**
- SQS Queue
- AZs with security groups containing EC2s and an ASG
- SQS message service
- Messages sent into SQS queue, EC2 instances are workers because they will pull messages from the SQS Queue to be processed
- Scale will be based on number of SQS messages
- We can push messages to SQS queue from another Web Server Tier

**DRAW DIAGRAMS LATER**

### Elastic Beanstalk Deployment Modes

**Single Instance**: Great for dev purposes
**HA with LB**: Great for production

# Amazon S3 Introduction

## S3 Overview
- One of the main building blocks of AWS
- Advertised as "infinitely scaling" storage
- Many websites use S3 as a backbone
- Many AWS services use S3 as an integration

### S3 Use Cases
- Backup and storage
- DR
- Archive
- Hybrid cloud storage
- Application hosting
- Media hosting
- Data lakes & big data analytics
- Software delivery
- Static website

### S3 - Buckets
- Allows people to store objects (files) in "buckets" (directories)
- Buckets must have a globally unique name (across all regions and accounts)
- Buckets are defined at the regional level
- S3 looks like a global service but buckets are created in a region
- Naming convention:
   - No uppercase, no underscore
   - 3-63 chars long
   - Not an IP
   - Must start with a lowercase letter or a number
   - **Must not** start with the prefix xn--
   - **Must not** end with the suffix -s3alias

### Amazon S3 - Objects
- Objects (files) have a Key
- The key is the full path e.g. s3://my-bucket/my_file.txt
- The key is composed of prefix + object name
- No concept of "directories" within buckets although the UI will make you think otherwise
- Object values are the content of the body
   - Max object size is 5TB (5000GB)
   - If uploading more than 5GB must use "multi-part upload"
- Metadata (list of text key / value pairs - system or user metadata)
- Tags (Unicode key / value pair - up to 10) - useful for security/lifecycle
- Version ID (if versioning is enabled)

### Amazon S3 Security - Bucket Policy

**User-based**:
- IAM policies - which API calls should be allowed for a specific user from IAM
**Resource-based**:
- Bucket policies - bucket wide rules from S3 console (allows cross account)
- Object ACL - finer grain (can be disabled)
- Bucket ACL - less common (can be disabled)

**An IAM principal can access an S3 object if:**
- **The user IAM permissions ALLOW it OR the resource policy ALLOWS it**
- **There is NO explicit DENY**

- Encryption: encrypts objects in S3 using encryption keys

### S3 Bucket Policies
- JSON based policies
   - Resources. buckets and objects
   - Effect: Allow/Deny
   - Actions: Set of API to Allow or Deny
   - Principle: The account or user to apply the policy to

Use S3 bucket policy to:
- Grant public access to the bucket
- Force objects to be encrypted at time of upload
- Grant access to another account (cross account)

### S3 Static Website Hosting
- S3 can host static websites and have them accessible on the internet
- If you get a 403 forbidden error, make sure the bucket policy allows public reads

## Amazon S3 Versioning
- Can version files in S3
- Enabled at bucket level
- Same key overwrite will change the version
- It is best practice to version buckets
   - Protect against unintended deletes (ability to restore a version)
   - Easy roll back to previous version
- Any file not versioned prior to enabling versioning will have version "null"
- Suspending versioning does not delete the previous versions

## S3 Replication (CRR & SRR)

- Must enable versioning in source and destination buckets
- Cross Region Replication (CRR)
- Same Region Replication (SRR)
- Buckets can be in different AWS accounts
- Copying is asynchronous
- Must give proper IAM permissions to S3

Use cases: 
- CRR - compliance, lower latency access, replication across accounts
- SRR - log aggregation, live replication between production and test accounts

**Notes**
- After you enable replication, only new objects are replicated
- If you want to replicate existing objects you can use S3 Batch Replication (it will also replicate objects that failed replication initially)
- For DELETE operations:
   - Can replicate delete markers from source to target (optional setting)
   - Deletions with a version ID are not replicated (to avoid malicious deletes)
- There is no "chaining" of replication which means:
   - If bucket 1 has replication into bucket 2, which has replication into bucket 3 - objects created in bucket 1 are not replicated to bucket 3

## S3 Storage Classes

The following storage classes are available:

**S3 Standard - General Purpose:**
- 99.999% availaibility
- Used for frequently accessed data 
- Low latency and high throughput
- Can sustain 2 concurrent facility failures

**S3 Standard - Infrequent Access (IA):**
- For data less frequently accessed but requires rapid access when needed
- Lower cost than S3 Standard
- 99.9% Availability
- Use cases: DR, backups

**S3 One Zone Infrequent Access:**
- High durability (99.9%^9) in a single AZ - data lost when AZ destroyed
- 99.5% availability
- Use cases: secondary backup copies of on-prem data, or data you can recreate

**S3 Glacier Instant Retreival:**
- Millisecond retreival - great for data accessed once a quarter
- Minimum storage duration of 90 days

**S3 Glacier Flexible Retreival:**
- Expedited (1-5 minutes), Standard (3 to 5 hours), Buk (5-12 hours) - free
- Minimum storage duration of 90 days

**S3 Glacier Deep Archive:**
- Standard (12 hours), Bulk (48 hours)
- Minimum storage duration of 180 days

**S3 Intelligent Tiering:**
- Small monthly monitoring and auto-tiering fee
- Moves objects automatically between tiers based on usage
- No retreival charges in S3 Intelligent Tiering
- Frequent access (automatic): default tier
- Infrequent access (automatic): objects not accessed for 30 days
- Archive Instant Access (automatic): objects not accessed for 90 days
- Archive Access (optional): configurable from 90 days to 700+ days
- Deep Archive access (optional): config from 180 days to 700+ days

It's possible to move between classes manually or by using S3 Lifecycle configurations

### S3 Durability and Availability
**Durability**
- High durability (99^9 %) of objects across multiple AZ
- If you store 10,000,000 objects with S3 you can on average expect to lose a single object once every 10,000 years
- Same for all storage classes
**Availability**
- Measures how readily available a service is
- Varies depending on storage class
- Example: S3 standard has 99.99% availability = not available 53 minutes of the year

### S3 Storage Classes Comparison

| |Standard|Intelligent-Tiering|Standard-IA|One Zone-IA|Glacier Instant Retrieval|Glacier Flexible Retrieval| Glacier Deep Archive|
|-----------|--------------------|-------------|--------------|--------------------------|-----------------|----------------|-------------------|
|Durability |99%^9|99%^9|99%^9|99%^9|99%^9|99%^9|99%^9|
|Availability|99.9%|99.9%|99.9%|99.5%|99.9%|99.9%|99.9%|
|Availability SLA|99.9%|99%|99%|99%|99%|99.9%|99.9%|
|Availability Zones|>=3|>=3|>=3|1|>=3|>=3|>=3|
|Min. storage duration charge|None|None|30|30|90|90|180|
|Min Billable object size|None|None|128KB|128KB|128KB|40KB|40KB|
|Retrieval fee|None|None|Per GB| Per GB|Per GB|Per GB|Per GB|

# Advanced S3

## Lifecycle Rules (with S3 Analytics)
- You can transition objects between storage classes
- For infrequently accessed objects, move them to Standard IA
- For archive objects that you don't need fast access to, move to Glacier or Glacier Deep Archive
- Moving objects can be automated with Lifecycle Rules

### S3 Lifecycle Rules

**Transition Actions** - Configure objects to transition to another storage class
- Move objects to Standard IA class 60 days after creation
- Move to Glacier for archiving after 6 months

**Expiration actions** - configure objects to expire (delete) after some time
- Access log files can be set to delete after 365 days
- Can be used to delete old versions of files (if versioning is enabled)
- Can be used to delete incomplete Multi-part uploads

- Rules can be created for a certain prefix
- Rules can be created for certain objects Tags

### Storage Class Analysis
- Helps you decide when to transition objects to the right storage class
- Recommendations for Standard and Standard IA - does not work for One-zone IA or Glacier
- Report is updated daily
- 24 to 48 hours to start seeing data analysis

## S3 - Requester Pays
- In general bucket owners pay for all S3 storage and data transfer costs associated with their bucket
- With Requester Pays, the requester instead of the bucket owner pays the cost of the request and the data downloaded from it
- This is helpful when you want to share large datasets with other accounts
- The requester must be authenticated in AWS (cannot be anonymous)

## S3 Event Notifications

- S3:ObjectCreated, S3:ObjectRemoved, S3:ObjectRestore, S3:Replication
- Object name filtering possible (e.g. *.jpg)
- Use case: generate thumbnails of images uploaded to S3
- Can create as many S3 events as you like and send them to whatever target you like (e.g. SNS, SQS, Lambda Func)

### S3 Event Notifications - IAM Perms
- For Event Notifications to work we need to have IAM permissions
- If S3 is sending it to an SNS Topic (for example) we need to attach an SNS access policy to it so that the bucket can send messages directly
- If S3 sends it to SQS we need to create an SQS resource access policy and attach it like before

### S3 Event Notifications with Amazon EventBridge
- All events pass through here
- We can attach rules which means we can pick where we send these events further on to for their final destination
- We also get advanced filtering options with JSON rules (metadata, object size, name)
- Multiple destinations - eg step functions, kinesis streams, firehose
- EventBridge capabilities - Archive, replay events, reliable delivery

## S3 Performance

- S3 automatically scales to high request rates, latency of 100-200ms
- Your application can achieve at least 3,500 PUT/COPY/POST/DELETE or 5,500 GET/HEAD requests per second per prefix in a bucket
- There are no limits to the number of prefixes in a bucket
- For example (object path --> Prefix):
   - bucket/folder1/sub1/file --> /folder1/sub1/
   - bucket/folder1/sub2 --> /folder1/sub2/
- If you spread reads across all four prefixes evenly you can achieve 22,000 requests per second for GET/HEAD

### Multi-part upload
- Recommended for files > 100MB
- A must for files > 5GB
- Can help parallelise uploads (speed up transferes)

### S3 Transfer Acceleration
- Increase transfer speed by transferring file to an AWS edge location which will forward the data to the S3 bucket in the target region
- Compatible with multi-part upload

### S3 Byte Range Fetches
- Parallelise GETs by requesting specific byte ranges
- Better resilience in case of failures
- Can be used to speed up downloads
- Also can be used to retrieve only partial data (e.g. head of a file)

## S3 Select & Glacier Select
- Retrieve less data using SQL by performing server-side filtering
- Can filter by rows and columns (simple SQL statements)
- Less network transfer, less CPU cost client-side
- Amazon says it's up to 400% faster

## S3 Batch Operations
- Perform bulk operations on existing S3 objects with a single request e.g.:
   - Modify object metadata & properties
   - Copy objects between S3 buckets
   - Encrypt un-encrypted objects
   - Modify ACLs, tags
   - Restore objects from S3 Glacier
   - Invoke Lambda function to perform custom action on each object
- A job consists of a list of objects, the action to perform, and optional parameters
- S3 Batch Operations manages, retries, tracks progress, sends completion notifications, generates reports etc
- You can use S3 Inventory to get object lists and use S3 Select to filter your objects

# Amazon S3 Security

### Object Encryption
You can encrypt objects in S3 buckets using one of 4 methods...

**Server-Side Encryption (SSE):**
- Server-Side Encryption with Amazon S3 Managed Keys (SSE-S3) - enabled by default
- Encrypts S3 objects using keys handled, managed, and owned by AWS
- Encryption type is AES-256
- Must set header "x-amz-server-side-encryption":"AES256"

**Server-Side Encryption with KMS Keys stored in AWS KMS (SSE-KMS):**
- Leverage AWS Key Management Service (AWS KMS) to manage encryption keys
- KMS advantages: user control + audit key usage using CloudTrail
- Must set header "x-amz-server-side-encryption":"aws:kms"

There are some downsides however...
- If you use SSE-KMS you may be impacted by KMS limits
- When you upload it calls the GenerateDataKey KMS API
- When you download it calls the Decrypt KMS API
- Count towards the KMS quota per second (55,00, 10000, 30000 req/s based on region)
- You can request a quota increase using the Service Quotas Console

**Server-side Encryption with Customer Provided Keys (SSE-C):**
- For when you want to manage your own encryption keys
- Server-side encryption using keys full managed by the customer outside of AWS
- S3 does not store the encryption key you provide
- HTTPS must be used
- Encryption key must be provided in HTTP headers for every request made

**Client-Side Encryption:**
- Use client libraries such as Amazon S3 Client-Side Encryption Library
- Clients must encrypt data themselves before sending to Amazon S3
- Clients must decrypt data themselves when retreiving from Amazon S3
- Customer fully manages the keys and encryption cycle

### S3 Encryption in Transit (SSL/TLS)
- S3 exposes two endpoints - HTTP (not encrypted), HTTPS (encrypted)
- HTTPS recommended
- HTTPS mandatory for SSE-C
- Most clients would use HTTPS by default

### S3 - Force Encryption in Transit
- Use aws:SecureTransport 
- In your bucket policy add it as a condition (bool)

## S3 Default Encryption

### Default Encryption vs Bucket Policies
- SSE-S3 encryption is automatically applied to new objects stored in S3 bucket
- Optionally you can "force encryption" using a bucket policy and refuse any API call to PUT an S3 object without encryption headers (SSE-KMS or SSE-C)

## Cross Origin Resource Sharing (CORS)
- Origin = scheme (proto) + host (domain) + port
- As an example, example.com (implied port is 443 for HTTPS, 80 for HTTP)
- Web browser based mechanism to allow requess to other origins while visiting the main origin
- Same origin: http://example.com/app1 and http://example.com/app2
- Different origins: http://www.examploe.com and http://other,example.com
- Requests won't be fulfilled unless the other origin allows for the requests using CORS Headers (e.g. Access-Control-Allow-Origin)

### Amazon S3 CORS
- If a client makes a cross-origin request on our S3 bucket we need to enable the correct CORS headers
- Popular exam question!
- Can allow for a specific origin or for * (all origins)

## MFA Deletion
MFA will be required to:
- Permanently delete an object version
- Suspend versioning on the bucket
MFA won't be required to:
- Enable versioning
- List deleted versions

- To delete, versioning must be enabled on the bucket
- Only the bucket owner (root account) can enable/disable MFA delete
- Can be found under bucket properties

## S3 Access Logs
- For audit purpose you may want to log all access to S3 buckets
- Any request made to S3 from any account, authorized or denied - will be logged into another S3 bucket
- That data can be analysed using data analysis tools
- The target logging bucket must be in the same AWS region
- Log format is at https://docs.aws.amazon.com/AmazonS3/latest/dev/LogFormat.html

### S3 Access Logs: Warning
- Do not set your logging bucket to be the monitored bucket
- It will create a logging loop and your bucket will grow exponentially!

## Pre-Signed URLs
- Generate pre-signed URLs using the S3 Console, AWS CLI, or SDK
- URL expiration:
   - S3 Console - 1 min up to 720 mins (12 hours)
   - AWS CLI - configure expiration with --expires-in parameter in seconds (default 3600 secs, max 604800 secs which is around 168 hours)
   - Users given a pre-signed URL inherit the permissions of the user that generated the URL for GET/PUT
- Examples:
   - Allow only logged-in users to download a premium video from your S3 bucket
   - Allow an ever-changing list of users to download files by generating URLs dynamically

## Glacier Vault Lock & S3 Object Lock
- Adopt a WORM (Write Once Read Many) model
- Create a Vault Lock Policy
- Lock the policy for future edits (can no longer be changed or deleted)
- Helpful for compliance and data retention

### S3 Object Lock 
- Versioning must be enabled
- WORM again
- Block an object version deletion for a specified amount of time (not a lock policy)

Retention mode - Compliance:
- Object versions can't be overwritten or deleted by any user, including hte root user
- Objects retention modes can't be changed and retention periods can't be shortened

Retention mode - Governance:
- Most users can't overwrite or delete an object version or alter its lock settings
- Some users have special permissions to change the retention or delete the object

Retention period: protect the object for a fixed period, it can be extended

Legal hold:
- protect the object indefinitely, independent from retention period
- can be freely placed and removed using the s3:PutObjectLegalHold IAM permission

## S3 Access Points

Access Points simplify security management for S3 Buckets
Each access point has:
- its own DNS name (Internet origin or VPC origin)
- an access point policy (similar to bucket policy) - manage security at scale

### Access Points - VPC Origin
- We can define the access point to be accessible only from within the VPC
- You must create a VPC Endpoint to access the Access Point (Gateway or Interface endpoint)
- The VPC endpoint policy must allow access to the target bucket and Access Point

## S3 Object Lambda
- Use AWS Lambda functions to change the object before it is retrieved by the caller application
- Only one S3 bucket is needed, on top of which we create S3 Access Point and S3 Object Lambda Access Points
Uses cases:
- Redacting personally identifiable information for analytics or for non-production environments
- Converting across data formats such as converting XML to JSON
- Resizing and watermarking images on the fly using caller-specific details such as user who requested object

# CloudFront & AWS Global Accelerator

## AWS CloudFront
- CDN
- Improves read performance, content cache at edge
- Improves UX
- 216 Points of Presence (edge locations)
- DDoS protection due to integration with Shield (AWS WAF)

### CloudFront Origins
- S3 Bucket
   - For distributing files and caching them at edge
   - Enhanced security with CloudFront Origin Access Control (OAC)
   - OAC is replacing Origin Access Identity (OAI)
   - CloudFront can be used as an ingress (to upload files to S3)
- Custom Origin (HTTP)
   - Application LB
   - EC2 instance
   - S3 website (as long as bucket enabled as static site)
   - Any HTTP backend you want

### CloudFront vs S3 Cross Region Replication

**CloudFront**:
- Global Edge Network
- Files cached for a TTL of roughly a day
- Great for static content that must be available everywhere
**S3 Cross Origin Replication**:
- Must be set up for each region you want replication to happen in
- Files updated in near real time
- Read only
- Great for dynamic content that needs to be available at low-latency in few regions

### CloudFront - EC2 or ALB as an Origin

**EC2 flow**

Users --> Edge Location --> Allow Public IP of Edge Locations (http://d78uri9nf7uskq.cloudfront.net/tools/list-cloudfront-ips) --> EC2 Instances (must be public)

**ALB flow**

Users --> Edge Location Public IPs --> Allow Public IP of Edge Locations --> ALB in security group (must be public) --> Allow Security Group of Load Balancer --> EC2 instances in security group (can be private)

### CloudFront Geo Restriction
- Can restrict who can access your distribution
- Best to use an allowlist so that only they can access content if their IP is from a country on the approved list
- The "country" is determined using a 3rd party geo-ip database

## CloudFront - Price Classes
- CloudFront Edge Locations are all around the world
- Cost of data out per edge location varies

This means you have a few choices. You can reduce the number of edge locations for cost reduction. There are three price classes:
- Price Class All: all regions - best performance (most expensive)
- Price Class 200: most regions - excludes most expensive
- Price Class 100: only the least expensive regions

## CloudFront - Cache invalidation
- If you update the backend, CloudFront doesn't know about it and content only gets refreshed after TTL has expired
- You can force an entire or partial cache refresh by performing a CloudFront cache invalidation
- Can invalidate all files or certain paths

## AWS Global Accelerator

### Global users for an application
- You have deployed an application that has global users who want to access it
- They go over the public internet which can add latency due to many hops
- We wish to go as fast as possible through the AWS network to minimise latency

### Unicast IP vs Anycast IP
- Unicast: one server holds one IP
- Anycast: all servers hold same IP and client is routed to nearest one

### AWS Global Acclerator
- Leverage AWS internal network to route your application
- 2 Anycast IP are created for your application
- Anycast IP sends traffic directly to Edge Locations
- Edge locations send the traffic to your application

- Works with Elastic IP, EC2 Instances, ALB, NLB, public or private
- Consistent performance
   - Intelligent routing to lowest latency and fast regional failover
   - No issue with client cache (because IP doesn't change)
   - Internal AWS network
- Health Checks
   - Global Accelerator performs a health check of your applications
   - Helps make your application global (failover less than 1 minute)
   - Great for DR
- Security
   - Only 2 external IPs need whitelisting
   - DDoS protection due to AWS Shield

### AWS Global Accelerator vs CloudFront
- Both use AWS global network and edge locations around world
- Both services integrate with AWS shield for DDoS protection

**CloudFront**:
- Improves performance for both cacheable content (such as images or videos)
- Dynamic content (such as API acceleration and dynamic site delivery)
- Content is served at the edge

**Global Accelerator**:
- Improves performance for a wide range of applications over TCP or UDP
- Proxying packets at the edge to applications running in one or more AWS Regions
- Good fit for non-HTTP use cases such as gaming (UDP), IoT (MQTT) or VoIP
- Good for HTTP use cases that require static IP addresses
- Good for HTTP use cases that required deterministic, fast regional failover

# AWS Storage Extras

## AWS Snow Family Overview
- Offline devices to perform data migrations
- If it takes more than a week to transfer over the network - use them

**Snowball Edge**
- Physical data transport solution: move TBs or PBs of data in or out of AWS
- Pay per data transfer job
- Provide block storage to S3 compatible object storage
- **Storage Optimised**: 80TB of HDD capacity for block volume and S3 compatible object storage
- **Compute Optimised**: 42TB of HDD or 28TB NVMe capacity
- Use cases: large data cloud migrations, DC decommission, DR

**Snowcone & Snowcone SSD**
- Small portable computing anywhere. Rugged and secure - good for harsh environments
- Light (4.5 pounds)
- Device used for edge computing, storage, and data transfer
- **Snowcone**: 8TB of HDD storage
- **Snowcone SSD**: 14TB of SSD storage
- Use snowcone where snowball doesn't fit (e.g. space constrained env)
- Must provide own batteries and calbes
- Can be sent back to AWS offline, or connected to internet and use AWS DataSync to transfer data

**Snowmobile**
- Transfer exabytes of data (1EB = 1,000PB = 1,000,000TB)
- Each snowmobile has 100PB of capacity (use multiple in parallel)
- High security, temp controlled, GPS. 24/7 video surveillance
- Better than snowball if you're transferring more than 10PB

### AWS Snow Family for Data Migrations

| | Snowcone & Snowcone SSD | Snowball Edge Storage Optimised | Snowmobile |
|-|--------------------------------|---------------------------------------|---------------|
| Storage Capacity | 8TB HDD 14 TB SSD | 80TB usable | < 100 PB |
| Migration Size | Up to 24TB, online and offline | Up to petabytes, offline | Up to exabytes, offline |
| DataSync agent | Pre-installed | | |
| Storage Clustering | | Up to 15 nodes | |

### Snow Family - Usage Process

1. Request Snowball devices from the AWS console for delivery
2. Install the snowball client / AWS OpsHub on your servers
3. Connect the snowball to your servers and copy files using the client
4. Ship back the device when you're done (goes to the right AWS facility)
5. Data loaded into an S3 bucket
6. Snowball completely wiped

### What is edge computing?
- Process data while it's being created on an edge location
- A truck on the road, a ship on the sea, a mining station underground etc

These locations may have:
- Limited / no internet access
- Limited / no easy access to computing power

We can set up a Snowball edge / Snowcone device to do edge computing
Use cases:
- Preprocess data
- ML
- Transcoding media streams
- Eventually if needed we can ship back the device back to AWS for transferring data

### Snow Family - Edge Computing

**Snowcone & Snowcone SSD (smaller)**
- 2 CPUs, 4GB memory, wired or wireless access
- USB-C power using a cord or optional battery

**Snowball Edge - Compute Optimised**
- 104 vCPUs, 416GB RAM
- Optional GPU (useful for video processing or ML)
- 28TB NVMe or 42TB HDD usable storage

**Snowball Edge - Storage Optimised**
- Up to 40 vCPUs, 80GB RAM, 80TB storage
- Object storage clustering available

All: Can run EC2 instances & AWS Lambda functions (using AWS IoT greengrass)
Long-term deployment options: 1 and 3 years discounted pricing

### AWS OpsHub
- Historically to use Snow Family devices was CLI only
- Today can use AWS OpsHub (equivalent to Azure Storage Explorer) to manage snow family device:
   - Unlocking and configuring single or clustered devices
   - Transferring files
   - Launching and managing instances running on Snow Family devices
   - Monitor device metrics (storage capacity, active instances on your device)
   - Launch compatible AWs services on your devices (e.g. EC2, DataSync, NFS)

## Architecture: Snowball into Glacier
- Snowball **cannot** import to Glacier directly
- Need to use S3 first in combination with an S3 lifecycle policy

## Amazon FSx

### FSx Overview
- Launch 3rd party high performance file systems on AWS
- Full managed service
Offerings are:
- FSx for Lustre
- FSx for NetApp ONTAP
- FSx for Windows File Server
- FSx for OpenZFS

**FSx for Windows File Server**
- full managed Windows file system share drive
- Supports SMB and Windows NTFS
- Microsoft Active Directory integration, ACLS, user quotas
- CAn be mounted on Linux EC2 instances
- Supports Microsoft's Distributed File System (DFS) Namespaces (group files across multiple FS)
- Scales up to 10s of GB/s, millions of IOPS, 100s PB of data
- Storage options are SSD or HDD
- Can be accessed from on-prem infra (VPN or Direct Connect - aka ExpressRoute)
- Can be configured to be Multi-AZ
- Data backed up daily to S3

**FSx for Lustre**
- a type of parallel distributed file system for large scale computing
- Name Lustre derived from Linux and cluster
- Machine Learning, High Performance Computing (HPC)
- Video Processing, Financial Modelling etc
- Scales up to 100s GB/s, millions of IOPS, sub-ms latency
- Storage options are SSD (low latency, IOPS intensive workloads, small and random file operations) or HDD (throughput intensive workloads, large and sequential file operations)
- Seamless integration with S3
   - Can "read S3" as file system (through FSx)
   - Can write output back to S3 (also through FSx)
- Can be used from on-prem (VPN or Direct Connect)

**FSx for NetApp ONTAP**
- Managed NetApp ONTAP on AWS
- File System compatible with NFS, SMB, iSCSI
- Move workloads running on ONTAP or NAS to AWS
- Works with Lin/Win/Mac/VMware Cloud on AWS/Amazon Workspaces & App Stream 2.0/Amazon EC2 ECS and EKS
- Storage shrinks and grows automatically
- Snapshots replication, low cost, compression and data de-duplication
- Point-in-time instantaneous cloning (helpful for testing new workloads)

**Amazon FSx for OpenZFS**
- Managed OpenZFS file system on AWS
- File System compatible with NFS (v3, v4, v4.1, v4.2)
- Move workloads running on ZFS to AWS
- Works with same as ONTAP
- Up to 1,000,000 IOPS with < 0.5ms latency
- Snapshots, compression and low cost
- Point-in-time instantaneous cloning (helpful for testing new workloads)

### FSx System Deployment Options
- Scratch File System
   - Temporary storage
   - Data not replicated (doesn't persist if file server fails)
   - High burst (6x faster, 200MBps per TB)
   - Usage: short term processing, optimise costs
- Persistent File System
   - Long-term storage
   - Data replicated within same AZ
   - Replace failed files within minutes
   - Usage: long-term processing, sensitive data

## Storage Gateway Overview
- AWS pushing for "hybrid cloud"
Can be due to:
- long cloud migrations
- security requirements
- compliance requirements
- IT strategy
- S# is a proprietary storage technology so how do you expose S3 data on-prem?
- AWS Storage Gateway...

### AWS Storage Cloud Native Options
- Block (EBS, EC2 Instance Store)
- File (EFS, FSx)
- Object (S3, Glacier)

### AWS Storage Gateway
- Bridge betwen on-prem data and cloud data
Use cases:
- DR
- Backup and restore
- Tiered storage
- on-prem cache and low latency file access

Types of Storage Gateway:

S3 File Gateway:
- Configured S3 buckets accessible using NFS and SMB proto
- Most recently used data is cached in file gateway
- Supports S3 Standard, Standard IA, One Zone IA, Intelligent Tiering
- Transition to S3 Glacier using a Lifecycle Policy
- Bucket access using IAM roles for each File Gateway
- SMB protocol has integration with AD for user auth

FSx File Gateway:
- Native access to Amazon FSx for Windows File Server
- Local cache for frequently accessed data
- Windows native compatibility (SMB, NTFS, AD)
- Useful for group file shares and home directories

Volume Gateway:
- Block storage using iSCSI proto backed by S3
- Backed by EBS snapshots which can help restore on-prem volumes
- Cached volues: low latency access to most recent data
- Stored volumes: entire data set on prem, scheduled backups to S3

Tape Gateway:
- Some companies have backup processes using physical tapes
- With tape gateway companies use same process but in cloud
- Virtual Tape Library (VTL) backed by S3 and Glacier
- Back up data using existing tape-based processes (and iSCSI interface)
- Works with leading backup software vendors

### Storage Gateway - Hardware Appliance
- Using Storage Gateway means you need on-prem virtualisation
- Otherwise you can use a Storage Gateway Hardware Appliance
- Can buy it on amazon
- Works with File Gateway, Volume Gateway and Tape Gateway
- HAs required CPU, memory, network and SSD cache resources
- Helpful for daily NFS backups in small data centers

## AWS Transfer Family
- Fully managed service for file transfers into and out of S3 or EFS using FTP
Supported protocols:
- AWS Transfer for FTP
- AWS Transfer for FTPS
- AWS Transfer for SFTP

- Managed infra, scalable, reliable, HA (multi-AZ)
- Pay per provisioned endpoint per hour +data transfers in GB
- Store and manage user's credentials within the service
- Integrates with existing auth providers (AD, LDAP, Okta, Amazon Cognito, custom)
- Usage: sharing files, public data sets, CRM, ERP

## AWS DataSync
Move a large amount of data to and from:
- On prem / other cloud to AWS (NFS, SMB, HDFS, S3, API) - needs agent
- AWS to AWS (different storage services) - no agent needed
Can sync to:
- S3 (any storage classes including Glacier)
- Amazon EFS
- Amazon FSx (Windows, Lustre, NetApp, OpenZFS)
- Replication taks can be scheduled hourly, daily, weekly
- File perms and metadata preserved
- One agent task can use 10Gbps, can set a bandwidth limit 

## Storage Comparison

- S3: Object Storage
- S3 Glacier: Object Archival
- EBS volumes: network storage for your EC2 instance (high IOPS)
- EFS: Network File System for Linux instances, POSIX filesystem
- FSx for Windows: Network File System for Windows servers
- FSx for Lustre: High Performance Computing Linux file system
- FSx for NetApp ONTAP: High OS Compatibility
- FSx for OpenZFS: Managed ZFS file system
- Storage Gateway: S3 & FSx Fiile Gateway, Volume Gateway (cache & stored), Tape Gateway
- Transfer Family: FTP, FTPS, SFTP interface on top of Amazon S3 or Amazon EFS
- DataSync: Scheduled data sync from on-prem to AWS or AWS to AWS
- Snowcome/Snowball/Snowmobile: move large amount of data to cloud physically
- Database: for specific workloads, usually with indexing and querying

# AWS Integration and Messaging

### Introduction

- When we start deploying multiple applications they will need to be able to communicate with one another
- There are two patterns of application communication (synchronous and asynchronous)
- Synchronous between applications can be a problem if there are sudden spikes in traffic
- In these cases it can be better to decouple your applications using:
   - SQS: queue model
   - SNS: pub/sub model
   - Kinesis: real-time streaming model
   - Each of the above can scale independently from our application

### Amazon SQS - Queues

Flow is:

Producer --> Message sent --> SQS Queue --> Polled messages --> Consumer

- Oldest offering (over 10 years old)
- Fully managed service used to decouple applications

Attributes:
- Unlimited throughput, unlimited number of messages in queue
- Default retention of messages: 4 days, maximum of 14 days
- Low latency (<10ms on publish and read)
- Limitation of 256KB per message sent

- Can have duplicate messages (at least once delivery, occasionally)
- Can have out of order messages (best effort)

### SQS - Producing Messages
- Produced to SQS using SDK (SendMessage API)
- Message is persisted in SQS until a consumer deletes it
- Message retention: default 4 days, up to 14 days

Example: send order to be processed
- Order ID
- Customer ID
- Any other attributes

### SQS - Consuming Messages
- Consumers (running on EC2 instances, servers, or AWS Lambda)
- Poll SQS for messages (receive up to 10 at a time)
- Process the messages (example: insert the message into an RDS DB)
- Delete the messages using the DeleteMessage API

### SQS - Multiple EC2 Instance Consumers
- Consumers receive and process messages in parallel
- At least once delivery
- Best-effort messaging order
- Consumers delete messages after processing them
- We can scale consumers horizontally to improve throughput of processing

### SQS with Auto Scaling Groups
- Similar to the above, but we can set a CloudWatch Metric of Queue Length
- Whenever the queue goes over a certain length, it should set off a CloudWatch Alarm which will in turn increase the capacity of the ASG by X amount

## SQS Security

Encryption:
- In-flight encryption using HTTPS API
- At rest encryption using KMS keys
- Client-side encryption if the client wants to perform encryption/decryption itself

Access controls:
- IAM policies to regulate access to SQS API

SQS Access Policies:
- Similar to S3 bucket policies
- Useful for cross account access to SQS queues
- Useful for allowing other services (SNS, S3) to write to an SQS queue

### SQS - Message Visibility Timeout
- After message is polled by a consumer it becomes invisible to other consumers
- By default the message visibility timeout is 30 seconds - meaning it has 30 seconds to be processed
- After the message visibility timeout is over, the message is "visible" in SQS
- If a message is not processed within the visibility timeout it will be processed twice
- However, if a consumer knows it needs a bit more time, it could call the ChangeMessageVisbility API to get more time
- If visibility timeout is high (hours) and the consumer crashes, re-processing will take time
- If it is set too low (seconds) we may get duplicates

### SQS - Long Polling
- When a consumer requests messages from the queue it can optionally "wait" for messages to arrive if there are currently none
- Long Polling decreases the number of API calls made to SQS while increasing the efficiency and latency of your application
- Wait time can be between 1 and 20 seconds (20 preferable)
- Long Polling is preferable to short polling
- Long polling can be enabled at the queue level or at the API level using WaitTimeSeconds

### SQS - FIFO Queue
- FIFO = First In First Out
- Limited throughput: 300 messages/s without batching, 3000 mesages/s with
- Exactly-once send capability (by removing duplicates)
- Messages are processed in order by the consumer

## SQS with ASGs
- If load is too big, some transactions may be lost

### SQS as a buffer to database writes

Request hits Enqueue message (in ASG) --> Message is sent (SendMessage) --> SQS Queue receives it --> ReceiveMessage --> Dequeue message (in ASG) --> insert into DB | Message deleted from Enqueue message queue

- This pattern only works if the client does not need confirmation that the write has been happening

### SQS to decouple between application tiers
- Very common architecture
- For exam, think SQS any time you see decoupling, sudden spike load or timeouts

## Simple Notification Service (SNS)
- "Event producer" only sends message to one SNS topic
- As many "event receivers" (subscriptions) as we want to listen to the SNS topic notifications
- Each subscriber to the topic will get all the messages (note: new feature to filter messages)
- Up to 12,500,00 subscriptions per topic
- 100,000 topics limit

### SNS integration with AWS services
Many AWs services can send data directly to SNS for notifications such as:
- CloudWatch Alarms
- AWS Budgets
- Lambda
- ASG
- S3 Bucket (events)
- DynamoDB
- CloudFormation (state changes)
- AWS DMS (New Replic)
- RDS Events

### AWS SNS - how to publish
- Topics published using SDK:
   - Create a topic
   - Create a subscription (or many)
   - Publish to the topic

Direct publish (for mobile apps SDK):
- Create a platform application
- Create a platform endpoint
- Publish to the platform endpoint
- Works with Google GCM, Apple APNS, Amazon ADM

### SNS - Security

Encryption:
- In-flight encryption using HTTPS API
- At-rest encryptoin using KMS keys
- Client-side encryption if the client wants to perform encryption/decryption itself

Access Controls:
- IAM Policies to regulate access to the SNS API

SNS Access Policies:
- Similar to S3 bucket policies
- Useful for cross-account access to SNS topics
- Useful for allowing other services (S3) to write to an SNS topic

## SNS & SQS Fan Out Pattern
- Push once in SNS, receive in all SQS queues that are subscribers
- Full decoupled - no data loss
- SQS allows for: data persistence, delayed processing, and retries of work
- Ability to add more SQS subscribers over time
- Make sure your SQS queue access policy allows for SNS to write
- Cross-region delivery: works with SQS queues in other regions

### Application: S3 Events to multiple queues
- For the same combination of event type (e.g. object create) and prefix (e.g. images/) you can only have one S3 event rule
- If you want to send the same S3 event to many SQS queues, use fan-out

### Application: SNS to Amazon S3 through Kinesis Data Firehose (KDF)

Buying Service --> SNS topic --> Kinesis Data Firehose --> Amazon S3 and or any supported KDF destination

### Amazon SNS - FIFO Topic
Similar features as SQS FIFO:
- Ordering by Message Group ID (all messages in same group are ordered)
- Deduplication using Deduplication ID or Content Based Deduplication
- Can only have SQS FIFO queues as subscribers
- Limited throughput (same throughput as SQS FIFO)

Mix SNS FIFO and SQS FIFO if you need fan out + ordering + deduplication

### SNS - Message Filtering
- JSON policy used to filter messages sent to SNS topics subscriptions
- If a subscription doesn't have a filter policy then it receives every message

## Kineses Overview
- Makes it easy to collect, process, and analyse large streaming data in real-time
- Ingest real-time data such as: Application logs, Metrics, website clickstreams, IoT telemetry data
- **Kinesis Data Streams**: capture, process and store data streams
- **Kinesis Data Firehose**: load data streams into AWS data stores
- **Kinesis Data Analytics**: analyse data streams with SQL or Apache Flink
- **Kinesis Video Streams**: capture, process, and store video streams

### Kinesis Data Streams
- Retention between 1 - 365 days
- Ability to reprocess (replay) data
- Once data is inserted into Kinesis it can't be deleted (immutability)
- Data that shares the same partition goes to the same shard (ordering)
- Producers: AWS SDK, Kinesis Producer Library (KPL), AWS SDK
- Consumers:
   - Write your own: Kinesis Client Library (KCL), AWS SDK
   - Managed: AWS Lambda, Kinesis Data Firehose, Kinesis Data Analytics

### Kinesis Data Streams - Capacity Modes

Provisioned:
- You choose the number of shards provisioned, scale manually or using API
- Each shard gets 1MB/s in (or 1000 records per second)
- Each shard gets 2MB/s out (classic or enhanced fan-out consumer)

On-demand:
- No need to provision or manage the capacity
- Default capacity provisioned (4MB/s in or 4000 records per second)
- Scales automatically based on observed throughput peak during last 30 days
- Pay per stream per hour & data in/out per GB

**Kinesis Data Streams Security**
- Control access / auth with IAM policies
- Encryption in flight using HTTPs endpoints
- Encryption at rest using KMS
- You can implement encryption/decryption of data on client side (harder)
- VPC Endpoints available for Kinesis to access within VPC
- Monitor API calls using CloudTrail

## Kinesis Data Firehose Overview

Takes data from producers:
- Applications
- Client
- SDK, KPL,
- Kinesis Agent
- Kinesis Data Streams
- Amazon CloudWatch
- AWS IoT

Records of up to 1MB are sent to Kinesis Data Firehose. At this point, data is (optionally) transformed with a Lambda function. Batch writes then happen to various destinations:

3rd party: such as Datadog, splunk, or New Relic
AWS: S3, Redshift (Copy through S3), OpenSearch
Custom: HTTP endpoint if you have your own API set up

All or failed data can also be backed up to an S3 bucket

- Pay for data going through Firehose
- Near real time:
   - 60 seconds latency minimum for non-full batches
   - Or minimum 1MB of data at a time
- Supports many data formats, conversions, transformations, compression
- Supports custom data transformations using AWS Lambda

### Kinesis Data Streams vs Firehose

|Kinesis Data Streams|Kinesis DataFirehose|
|-----------------------|----------------------|
|Streaming service for ingest at scale| Load streaming data into S3/Redshift/OpenSearch/3rd party/Custom HTTP|
|Write custom code (producer/consumer)|Fully managed|
|Real-time (~200ms)|Near real-time buffer (min 60sec)|
| Manage scaling (shard splitting/merging)| Automatic scaling|
|Data storage for up to 1 year| No data storage|
|Supports replay capability|Doesn't support replay capability|

## Data Ordering for Kinesis vs SQS FIFO

### Ordering data into Kinesis
- Foreign key (partition key) is sent with data e.g. data_id
- Means that same key will always go to same shard

### Ordering data into SQS
- For SQS standard there is no ordering
- For SQS FIFO if you don't use a group ID, messages are consumed in the order they are sent with only one consumer
- You want to scale the number of consumers but you want messages to be grouped when they are related to each other
- If so, use a group ID (similar to partition key in Kinesis)

Assuming 100 trucks and 5 Kinesis shards, 1 SQS FIFO:

KDS:
- On average will have 20 trucks per shard
- Trucks will have their data ordered within each shard
- Maximum amount of consumers in parallel we can have is 5
- Can receive up to 5MB/s of data

SQS FIFO:
- Only have one SQS FIFO queue
- Will have 100 group ID
- Can have up to 100 consumers (due to 100 group ID)
- Have up to 300 messages per second (or 3000 if using batch)

## SQS vs SNS vs Kinesis

|SQS|SNS|Kinesis|
|----|----|---------|
|Consumer "pull data"|Push data to many subscribers|Standard: pull data (2MB per shard)|
|Data deleted after consumed|Up to 12,500,00 subscribers|Enhanced fan-out: push data (2MB per shard per consumer)|
|Can have as many workers (consumers) as needed|Data not persisted (lost if not delivered)|Possibility to replay data|
|No need to provision throughput|Pub/Sub|Meant for real-time big data, analytics & ETC|
|Ordering guarantees only on FIFO queues|Up to 100,000 topics| Ordering at shard level|
|Individual message delay capability| No need to provision throughput| Data expires after X days|
| | Integrates with SQS for fan-out architecture |Provisioned mode or on demand|
| | FIFO capability for SQS FIFO | | 

### Amazon MQ
- SQS, SNS are "cloud native" services: proprietary protocols from AWS
- Traditional applications running from on-prem may use open protos such as MQTT, AMQP, STROMP, Openwire, WSS
- When migrating to cloud instead of re-engineering the application to use SQS and SNS we can use Amazon MQ
- Amazon MQ is a managed message broker service for RabbitMQ and ActiveMQ
- Amazon MQ doesn't "scale" as much as SQS/SNS
- Amazon MQ runs on servers, can run in multi-AZ with failover
- Amazon MQ has both queue feature (~SQS) and topic features (~SNS)

Amazon MQ can be HA due to the possibility of having multiple in different AZs. So long as both are connected to EFS (so data is backed up), failover can happen properly.

# Containers on AWS: ECS, Fargate, ECR & EKS

### Docker
- Software development platform to deploy apps
- Apps are packaged in containers that can be run on any OS
- Apps are run the same regardless of where they're run
- Use cases: microservices architecture, lift and shift apps from on-prem to AWS cloud
- Can have multiple containers on an EC2 instance

**Storage of Docker containers**
- Stored in Docker Repos
- Docker Hub (hub.docker.com) - public repo
- Amazon ECR (Elastic Container Registry) - private repos or public repos - gallery.ecr.aws

**Docker Containers Management on AWS**
- Amazon Elastic Container Service (ECS) - Amazon's own container platform
- Amazon Elastic Kubernetes Service (EKS) - Amazon's managed Kubernetes (Open source)
- AWS Fargate - Amazon's own serverless container platform that works with ECS and EKS
- Amazon ECR - Store container images

## Amazon ECS

### EC2 Launch Type
- ECS = Elastic Container Service
- Launch Docker containers on AWS = Launch ECS Tasks on ECS Clusters
- EC2 Launch Type means you must provision and maintain the infra (EC2 instances)
- Each EC2 Instance must run the ECS Agent to register in the ECS Cluster
- AWS takes care of starting/stopping containers

### ECS - Fargate Launch Type
- Launch Docker containers on AWS
- Do not need to provision infra (no EC2 instances to manage)
- All serverless - only need to create task definitions
- AWS just runs ECS Tasks for you based on CPU/RAM you need
- To scale just increase number of tasks

### ECS - IAM Roles for ECS

EC2 Instance Profile (EC2 Launch Type only):
- Used by the ECS agent
- Makes API calls to ECS service
- Sends container logs to CloudWatch Logs
- Pull docker image from ECR
- Reference sensitive data in Secrets Manager or SSM Parameter Store

ECS Task Role:
- Allows each task to have a specific role
- Use different roles for the different ECS services you run
- Task Role is defined in the task definition

### ECS - Load Balancer Integrations
- Application Load Balancer supported and works for most use cases
- Network Load Balancer recommended only for high throughput/high performance use cases, or to pair it with an AWS Private Link
- Classic Load Balancer supported but not recommended (no advanced features - no Fargate)

### ECS - Data Volumes (EFS)
- Mount EFS file systems onto ECS tasks
- Works for both EC2 and Fargate launch types
- Tasks running in any AZ will share same data in the EFS file system
- Fargate + EFS = Serverless
- Use cases: persistent multi-AZ shared storage for your containers
- Note that S3 cannot be mounted as a file system!

## Amazon ECS - Autoscaling
- Automatically increase/decrease the designed number of ECS tasks
- Amazon ECS Auto Scaling uses AWS Application Auto Scaling
   - ECS Service Average CPU Utilisation
   - ECS Service Average Memory Utilisation - scale on RAM
   - ALB Request count per target - metric coming from ALB
- **Target tracking** - scale based on target value for a specific CloudWatch metric
- **Step scaling** - scale based on a specified CloudWatch alarm
- **Scheduled scaling** - scale based on a specified date/time (predictable changes)
- ECS Service Auto Scaling (task level) != EC2 Auto Scaling (EC2 instance level)
- Fargate Auto scaling is much easier to set up because serverless

### EC2 Launch Type - Auto Scaling EC2 Instances
- Accommodate ECS Service Scaling by adding underlying EC2 Instances
- Auto Scaling Group Scaling:
   - Scale your ASG based on CPU Utilisation
   - Add EC2 instances over time
- EC2 Cluster Capacity Provider:
   - Used to automatically provision and scale the infra for your ECS Tasks
   - Capacity Provider paired with an Auto Scaling Group
   - Add EC2 Instances when you're missing capacity (CPU, RAM)

## Amazon ECS - Solutions Architectures

### ECS tasks invoked by Event Bridge

COME BACK AND CREATE DIAGRAMS HERE

### ECS tasks invoked by Event Bridge Schedule

COME BACK AND CREATE A DIAGRAM HERE

### ECS - SQS Queue Example

Diagram...

### ECS - Intercept Stopped Tasks using EventBridge

Diagram...

## Amazon ECR
- Elastic Container Registry
- Store and manage Docker images on AWS
- Private and Public repo
- Full integrated with ECS, backed by S3
- Access controlled through IAM (permission errors --> policy)
- Supports image vulnerability scanning, versioning, image tags, image lifecycle

## Amazon EKS Overview
- A way to launch managed Kubernetes clusters on AWS
- Kubernetes is an open-source system for automatic deployment, scaling, and management of containerised (usually Dockerised) application
- Alternative to ECS, similar goal but different API
- EKS supports EC2 if you want to deploy worker nodes or Fargate to deploy serverless containers
- Use case: if company is already using Kubernetes on-prem or in another cloud and wants to migrate to AWS
- Kubernetes is cloud agnostic

### Amazon EKS - Node Types

Managed Node Groups:
- Creates and manages Nodes (EC2 instances) for you
- Nodes are part of an ASG managed by EKS
- Supports on-demand or spot instances

Self managed nodes:
- Nodes created by you and registered to EKS cluster and managed by an ASG
- Can use prebuilt AMI - Amazon EKS Optimised AMI
- Supports on demand or spot instances

AWS Fargate:
- No maintenance required; no nodes managed

### Amazon EKS - Data Volumes

- No need to specify StorageClass manifest in your EKS cluster
- Leverages a Container Storage Interface compliant driver
- Support for:
   - EBS
   - EFS (works with Fargate)
   - FSx for Lustre
   - FSx for NetApp ONTAP

## AWS App Runner
- Fully managed service that makes it easy to deploy web applications and APIs at scale
- No infra experience needed
- Start with your source code or container image
- Automatically build and deploy the web app
- Automatic scaling, HA, LB, encryption
- VPC access support
- Connect to database, cache, and message queue service
- Use cases: web apps, APIs, microservices, rapid production deployments

# Serverless Overviews from a Solution Architect Perspective

## Serverless Introduction
- Serverless is a new paradigm in which devs don't have to manage servers anymore
- They only need to deploy code
- Serverless was pioneered by AWS Lambda but now also includes anything that's managed - DBs, messaging, storage etc
- Serverless does not mean there are no servers, it just means you don't manage/provision/see them

### Serverless in AWS
- Lambda
- DynamoDB
- Cognito
- API Gateway
- S3
- SNS & SQS
- Kinesis Data Firehose
- Aurora Serverless
- Step Functions
- Fargate

## Lambda Overview

### Why AWS Lambda?

Compared to an EC2 Instance that are:
- Virtual servers in the cloud
- Limited by RAM and CPU
- Continuously running
- Scaling means intervention to add/remove servers

AWS Lambda on the other hand are:
- Virtual functions - no servers to manage
- Limited by time - short executions
- Run on-demand
- Scaling is automated

### Benefits of Lambda

Easy pricing:
- Pay per request and compute time
- Free tier of 1,000,000 Lambda requests and 400,000GBs of compute time

- Integrated with the whole AWS suite of services
- Integrated with many programming languages
- Easy monitoring through AWS CloudWatch
- Easy to get more resources per functions (up to 10GB RAM)
- Increasing RAM will also improve CPU and network

### AWS Lambda language support
- Node.js 
- Python
- Java (Java 8 compatible)
- C# (.NET Core)
- Golang
- C#/PS
- Ruby
- Custom Runtime API (community supported e.g. Rust)

Lambda container image must implement the Lambda Runtime API

### Main AWS Lambda Integrations
- API Gateway
- Kinesis
- DynamoDB
- S3
- CloudFront
- CloudWatch Events - EventBridge
- CloudWatch Logs
- SNS
- SQS
- Cognito

### AWS Lambda Pricing

Can find overall pricing at aws.amazon.com/lambda/pricing

- Pay per calls:
   - First 1,000,000 requests are free
   - $0.20 per 1 million requests after that
- Pay per duration (in increment of 1ms): 
   - 400,000GB  seconds of compute time per month free
   - == 400,000 seconds if function is 1GB RAM
   - == 3,200,000 seconds if function is 128MB RAM
   - After that, $1 for ever 600,000 GB seconds

## Lambda Limits (per region)

Execution:
- Memory allocation: 128MB - 10GB (1MB increments)
- Maximum execution time: 900 seconds (15 minutes)
- Environment variables (4KB)
- Disk capacity in the "function container" (in /tmp): 512MB to 10GB
- Concurrency executions: 1000 (can be increased)

Deployment:
- Lambda function deployment size (compressed .zip): 50MB
- Size of uncompressed deployment (code + dependencies): 250MB
- Can use the /tmp directory to load other files at startup
- Size of environment variables also 4KB

## Lambda at Edge & CloudFront Functions

Use cases:
- Website security and privacy
- Dynamic web application at the edge
- SEO
- Intelligently route across origins and data centers
- Bot mitigation at the edge
- Real time image transformation
- A/B testing
- User Authentication and Authorisation
- User Prioritisation
- User Tracking and Analytics

### CloudFront Functions
- Lightweight functions written in JS
- For high-scale, latency- sensitive CDN optimisations
- Sub-ms startup times, millions of requests/s
- Used to change Viewer requests and responses:
   - Viewer Request: after CloudFront receives a request from a viewer
   - Viewer Response: before CloudFront forwards the response to the viewer
- Native feature of CloudFront (manage code entirely within CloudFront)

### Lambda at Edge
- Lambda functions written in NodeJS or Python
- Scales to 1000s of requests/s
- Used to change CloudFront requests and responses: 
   - Viewer Request - after CloudFront receives a request from a viewer
   - Origin Response - after CloudFront receives the response from the origin
   - Viewer Response - before CloudFront forwards the response to the viewer
- Author your functions in one AWS reagion (e.g. us-east-1) then CloudFront replicates to its locations

### CloudFront Functions vs Lambda@Edge

| |CloudFront Functions|Lamda@Edge|
|-|------------------------|------|
| |Runtime Support|JavaScript|Node.js, Python|
|# of Requests|Millions per second|Thousands per second|
|CloudFront Triggers|Viewer Req/Resp|Viewer Req/REsp, Origin Req/Resp|
|Max. Execution Time|<1ms|5-10 seconds|
|Max Memory|2MB|128MB up to 10GB|
|Total Package Size|10KB|1MB-50MB|
|Network & FS Access|No|Yes|
|Access to request body|No|Yes|
|Pricing|Free tier availalbe, 1/6th price of @Edge|No free tier, charged per request & duration|


### CloudFront Functions vs. Lambda@Edge - Use Cases

CloudFront Funtions:
- Cache key normalisation
   - Transform req attributes (headers, cookies, query strings, URL) to create an optimal Cache Key
- Header manipulation
   - Insert/modify/delete HTTP headers in the request or response
- URL rewrites or redirects
- Request authentication and authorisation
   - Create and validate user-generated tokens (e.g. JWT) to allow/deny requests

Lambda@Edge:
- Longer execution time (several ms)
- Adjustable CPU or memory
- Your code depends on 3rd party libraries (e.g. AWS SDK to access other AWS services)
- Network access to use external services for processing
- File system access or access to the body of HTTP requests

## Lambda in VPC

### Lambda by Default
- By default your Lambda function is launched outside your own VPC (in an AWS owned VPC)
- Therefore it cannot access resources in your VPC (RDS, ElastiCache, internal ELB etc)

### Lambda in VPC
- You must define the VPC ID, the subnets, and security groups
- Lambda will create an ENI (Elastic Network Interface) in your subnets

### Lambda with RDS Proxy
- If Lambda functions directly access your DB they may open too many connections under high load

RDS Proxy:
- Improves scalability by pooling and sharing DB connections
- Improves availability by reducing the failover time and preserving connections by 66%
- Improve security by enforcing IAM authentication and storing credentials in Secrets Manager

**! The Lambda function must be deployed in your VPC because the RDS Proxy is never publicly accessible**

## RDS - Invoking Lambda & Event Notifications

### Invoking Lambda functions from RDS & Aurora
- Invoke Lambda functions from within your DB instance
- Allows you to process data events from within a DB
- Supported for RDS for Pg and Aurora MSQL
- Must allow outbound traffic to your Lambda function from within your DB instance (Public, NAT, GW, VPC endpoints)
- DB instance must have the required permissions to invoke the Lambda function (Lambda Resource-based Policy & IAM Policy)

### RDS Event Notifications
- Notifications that tell information about the DB instance itself (created, stopped, started)
- You don't have any info about the data itself
- Subscribe to the following event categories:
   - DB instance
   - DB snapshot
   - DB Parameter Group
   - DB Security Group
   - RDS Proxy
   - Custom Engine Version
- Near real time events (up to 5 mins)
- Send notifications to SNS or subscribe to events using EventBridge

## Amazon DynamoDB
- Fully managed and HA with replication across multiple AZ
- NoSQL DB - not relational - with transaction support
- Scales to massive workloads - distributed DB
- Millions of requests per second, trillions of rows, 100s of TB of storage
- Fast and consistent in performance (single-digit ms)
- Integrated with IAM for security, auth, and administration
- Low cost and auto-scaling capabilities
- No maintenance or patching, always available
- Standard & Infrequent Access (IA) Table Class

### DynamoDB Basics
- DynamoDB is made of Tables
- Each table has primary key (must be decided at creation time)
- Each table can have an infinite number of items (rows)
- Each item has attributes - can be added over time and can be null
- Maximum size of an item is 400KB
- Data types supported are:
  - Scalar Types - string, number, binary, boolean, null
  - Document types - list, map
  - Set Types - string set, number set, binary set
- In DynamoDB you can rapidly evolve schemas

### DynamoDB - Read/Write Capacity Modes

Control how you manage your table's capacity (read/write throughput)

Provisioned mode:
- You specify the number of reads/writes per second
- You need to plan capacity beforehand
- Pay for provisioned Read Capacity Unites (RCU) and Write Capacity Units (WCU)
- Possibility to add auto-scaling mode for RCU & WCU

On-demand mode:
- Read/writes automatically scale up/down with your workloads
- No capacity planning needed
- Pay for what you use, more expensive (£££)
- Great for unpredictable workloads or sudden steep spikes

## Dynamo DB - Advanced Features

### DynamoDB Accelerator (DAX)
- Fully managed, HA, seamless in-memory cache for DynamoDB
- Helps solve congestion by caching
- Microseconds latency for cached data
- Doesn't require application logic modification (compatible with existing DynamoDB APIs)
- 5 minute TTL for cache (default)

### DynamoDB - Stream Processing
- Ordered stream of item-level modifications (create/update/delete) in a table

Use cases:
- React to changes in real-time (welcome email to users)
- Real-time usage analytics
- Insert into derivative tables
- Implement cross-region replication
- Invoke AWS Lambda on changes to your DynamoDB table

**DynamoDB Streams**
- 24 hour retention
- Limited number of consumers
- Process using AWS Lambda Triggers or DynamoDB Stream Kinesis adapter

**Kinesis Data Streams (newer)**
- 1 year retention
- High number of consumers
- Process using AWS Lambda, Kinesis Data Analytics, Kinesis Data Firehose, AWS Glue Streaming ETL

### DynamoDB Global Tables
- Make a DynamoDB table accessible with low latency in multiple regions
- Active-Active replication
- Applications can read and write to the table in any region
- Must enable DynamoDB Streams as a pre-requisite

### DynamoDB TTL
- Automatically delete items after an expiry timestamp
- Use cases: reduce stored data by only keeping current items, adhere to regulatory obligations, web session handling etc

### DynamoDB - Backups for DR
- Continuous backups using point-in-time recovery (PITR)
   - Optionally enable for the last 35 days
   - PITR to any time within the backup window
   - Recovery process creates a new table

On-demand backups
- Full backups for long-term retention until explicitly deleted
- Doesn't affect performance or latency
- Can be configured and managed in AWS Backup (enables cross-region copy)
- Recovery process creates new table

### DynamoDB - Integration with S3

Export to S3 (must enable PITR)
- Works for any point of time in last 35 days
- Doesn't affect read capacity of your table
- Perform data analysis on top of DynamoDB
- Retain snapshots for auditing
- ETL on top of S3 data before importing back into DynamoDB
- Export DynamoDB JSON or ION format

Import from S3:
- Import CSV, DynamoDB, JSON, or ION format
- Doesn't consume any write capacity
- Creates a new table
- Import errors are logged in CloudWatch Logs

## AWS API Gateway Overview
- AWS Lambda + API Gateway: No infra to manage
- Support for WebSocket protocol
- Handle API versioning
- Handle different environments (dev, test, prod)
- Handle security (AuthN and AuthZ)
- Create API keys, handle request throttling
- Swagger/Open API import to quickly define APIs
- Transform and validate requests and responses
- Generate SDK and API specifications
- Cache API responses

### API Gateway - Integrations High Level

Lambda function:
- Invoke Lambda function
- Easy way to expose REST API backend by AWS Lambda

HTTP:
- Expose HTTP endpoints in backend
- Example: internal HTTP API on prem, ALB
- Why? Add rate limiting, caching, user auth, API keys etc

AWS Service:
- Expose any AWS API through the API Gateway
- Example: start an AWS Step Function workflow, post a message to SQS
- Why? Add auth, deploy publicly, rate control

### API Gateway - Endpoint Types

Edge-Optimised (default): for global clients
- Requests are routed through the CloudFront Edge locations (improves latency)
- The API Gateway still lives in only one region

Regional:
- For clients within the same region
- Could manually combine with CloudFront (more control over caching strategies and distribution)

Private:
- Can only be accessed from your VPC using an interface VPC endpoint (ENI)

### API Gateway - Security

Username auth through:
- IAM Roles (useful for internal applications)
- Cognito (identity for external users e.g. mobile)
- Custom Authoriser (your own logic)

Custom Domain Name HTTPS security through integration with AWS Cert Manager (ACM):
- If using Edge-Optimised endpoint, then certificate must be in us-east-1
- If using regional endpoint, the cert must be in the API gateway region
- Must set up CNAME or A-alias record in Route53

## AWS Step Functions
- Build serverless visual workflow to orchestrate your Lambda functions
- Features: sequence, parallel, conditions, timeouts, error handling etc
- Can integrate with EC2, ECS, On-prem servers, API Gateway, SQS queues etc
- Possibility of implementing human approval feature
- Use cases: order fulfillment, data processing, web applications, any workflow

## Amazon Cognito
- Give users an identity to interact with a web or mobile applications

Cognito User Pools:
- Sign in functionality for app users
- Integrate with API Gateway & ALB

Cognito Identity Pools (Federated Identity):
- Provide AWS credentials to users so they can access AWS resources directly
- Integrate with Cognito User Pools as an identity provider

Cognito vs IAM: "hunders of users", "mobile users", "authenticate with SAML"

### Cognito User Pools - User Features
- Create a serverless database of users for your web and mobile apps
- Simple login: username (or email) and password combo
- Password reset
- Email & phone verification
- MFA
- Federated identities: users from Facebook, Google, SAML

Cognito User Pools integrate with API Gateway and ALB

### Cognito Identity Pools (Federated Identities)
- Get identities for "users" so they can obtain temporary AWS credentials
- Users source can be Cognito User Pools, 3rd part logins etc
- Users can then access AWS services directly or through API Gateway
- The IAM policies applied to the credentials are defined in Cognito
- They can be customised based on the user_id for fine grained control
- Default IAM roles for authenticated and guest users

## Serverless Solution Architecture Discussions

### Mobile Application
- Serverless REST API; HTTPS, API Gateway, Lambda, DynamoDB
- Using Cognito to generate temporary creds with STS to access S3 bucket with restricted policy. App users can directly access AWS resources this way. Pattern can be applied to DynamoDB, Lambda
- Caching the reads on DynamoDB using DAX
- Caching the REST requests at the API Gateway level
- Security for authN and authZ with Cognito, STS

### Serverless hosted website

Background:
- Website should scale globally
- Blogs are rarely written, but often read
- Some of the website is purely static files, the rest is a dynamic REST API
- Caching must be implemented where possible
- Any new users that subscribe should receive a welcome email
- Any photo uploaded to the blog should have a thumbnail generated

- Static content distributed using CloudFront with S3
- REST API was serverless, didn't need Cognito because it's public
- Leveraged a Global DynamoDB table to serve the data globally (could have used Aurora Global DB)
- Enabled Dynamo DB streams to trigger a Lambda function
- Lambda function had an IAM role which could use SES
- SES was used to send emails in a serverless way
- S3 can trigger SQS/SNS/Lambda to notify of events

### Microservices Architecture

Background:
- We want to switch to a microservice architecture
- Many services interact with each other directly using a REST API
- Each architecture for each microservice may vary in form and shape
- We want a microservice architecture so we can have a leaner development lifecycle for each service

**Discussion on Microservices**
- You are free to design each microservice the way you want
- Synchronous patterns: API Gateway, Load Balancers
- Asynchronous patterns: SQS, Kinesis, SNS, Lambda triggers (S3)

Challenges with microservices:
- repeated overhead for creating each new microservice
- issues with optimising server density/utilisation
- complexity of running multiple versions of multiple microservices simultaneously
- proliferation of client-side code requirements to integrate with many separate services

Some of the challenges solved by serverless patterns:
- API Gateway, Lambda scale automatically and you pay per usage
- You can easily clone API, reproduce environments
- Generated client SDK through swagger integration for API Gateway

## Software updates distribution

### Software updates offloading
- We have an application on an EC2 that distributes software updates once in a while
- When a new software update is out we get a lot of requests and the content is distributed in mass over the network which is costly
- We don't want to change our application but want to optimise our cost and CPU - how do we go about it?

We can use CloudFront because:
- No changes in architecture
- Will cache software update files at the edge
- Software update files are not dynamic, they're static
- Our EC2 instances aren't serverless, but CloudFront is and will scale for us
- Our ASG will not scale as much as we'll save tremendously in EC2
- We'll also save in availability and network bandwidth cost etc
- Easy way to make an existing application more scalable and cheaper

# Databases in AWS

### Choosing the right DB
- We have lots of managed DBs in AWS to choose from
- Questions to choose the right DB based on your architecture:
   - Read heavy, write heavy, or balanced workload? Throughput needs? Will it change? Does it need to scale or fluctuate during the day?
   - How much data to store and for how long? Will it grow? Average object size? How are they accessed?
- Data durability? Source of truth for the data?
- Latency requirements? Concurrent users?
- Data model? How will you query the data? Joins? Structured? semi-structured?
- Strong schema? More flexibility? Reporting? Search? RDBMS/NoSQL?
- License costs? Switch to Cloud Native DB such as Aurora?

### Database Types

- RDBMS = SQL/OLTP: RDS, Aurora - great for joins
- NoSQL - no joins, no SQL: DynamoDB (JSON), ElastiCache (key/value pairs), Neptune (graphs), DocumentDB (for MongoDB), Keyspaces (for Apache Cassandra)
- Object Store: S3 for big objects, Glacier for backups/archives
- Data Warehouse = SQL analytics/BI: Redshift (OLAP), Athena, EMR
- Search: OpenSearch (JSON) - free text, unstructured searches
- Graphs: Amazon Neptune - displays relationships between data
- Ledger: Amazon Quantum Ledger DB
- Time series: Amazon Timestream

#### RDS
- Managed Pg/MSQL/Oracle/SQL Server/MariaDB/Custom
- Provisioned RDS Instance size and EBS Volume Type & Size
- Auto-scaling capability for storage
- Support for read replicas and multi-AZ
- Security through IAM, Security Groups, KMS, SSL in transit
- Automated backup with PITR (up to 35 days)
- Manual DB snapshot for longer-term recovery
- Managed and Scheduled maintenance (with downtime)
- Support for IAM Auth, integration with Secrets Manager
- RDS Custom for access to and customize the underlying instance (Oracle & SQL server)
- Use case: store relational datasets, perform SQL queries, transactions

#### Amazon Aurora
- Compatible API for Pg/MSQL, separation of storage and compute
- Storage: data is stored in 6 replicas, across 3AZ - highly available , self-healing, auto-scaling
- Compute: Cluster of DB Instance across multiple AZ, auto-scaling of read replicas
- Cluster: Custom endpoints for writer and reader DB instances
- Same security/monitoring/maintenance features as RDS
- Know the backup and restore options for Aurora
- **Aurora serverless** - for unpredictable/intermittent workloads, no capacity planning
- **Aurora Multi-Master** - for continuous writes failover (high write availability)
- **Aurora Global**: up to 16 DB Read instances in each region, < 1 second storage replication
- **Aurora ML**: Performing ML using SageMaker & Comprehend on Aurora
- **Aurora DB Cloning** new cluster from existing one, faster than restoring a snapshot
- Use case: same as RDS, but with less maintenance/more flexibility/more performance and features

#### ElastiCache
- Managed Redis/Memcached (similar offering as RDS, but for caches)
- In-memory data store, sub ms latency
- Select an ElastiCache instance type (e.g. cache.m6.large)
- Support for clustering (Redis) and Multi AZ, read replicas (sharding)
- Security through IAM, Security Groups, KMS, Redis Auth
- Backup/snapshot/PITR feature
- Managed and scheduled maintenance
- Requires some application code changes to be leveraged
- Use case: Key/value store, Frequent reads, less writes, cache results for DB queries, store session data for websites, cannot use SQL

#### DynamoDB
- AWS proprietary technology - managed serverless NoSQL DB - ms latency
- Capacity modes: provisioned with optional autoscaling, on demand
- Can replace ElastiCache as key/value store (storing session data using TTL)
- HA & Multi-AZ by default, read and writes are decoupled, transaction capability
- DAX cluster for read cache, microsecond read latency
- Security, authN and autZ done through IAM
- Event processing: DynamoDB Streams to integrate with Lambda or Kinesis Data Streams
- Global table feature: active-active
- Automated backups to 35 days with PITR or on demand backups
- Export to S3 without using RCU within the PTIR window, import from S3 without using WCU
- Use cases: Serverless application development (small documents of 100s KB), distributed serverless cache

#### S3
- key/value store for objects
- Great for bigger objects, not so great for many small objects
- Serverless, scales infinitely, max object size is 5TB, versioning capability
- Tiers: Standard, Infrequent Access (IA), Intelligent, Glacier + lifecycle policy
- Features: Versioning, Encryption, replication, MFA-Delete, Access logs
- Security: IAM, Bucket Policies, ACL, Access Points, Object Lambda, CORS, Object/Vault lock
- Encryptoin: SSE-S3, SSE-KMS, SSE-C, client side, TLS in transit, default encrytpion
- Batch operations on objects using S3 Batch, listing files using S3 Inventory
- Performance: multi-part upload, S3 Transfer acceleration, S3 Select
- Automation: S3 Event Notifications (SNS, SQS, Lambda, EventBridge)
- Use cases: static files, key value store for big files, website hosting

#### DocumentDB
- Aurora is an "AWS-implementation" of Pg/MSQL
- DocumentDB is same for MongoDB (which is a NoSQL DB)
- MongoDB used to store, query, and index JSON data
- Similar "deployment concepts" as Aurora
- Full managed, HA, with replication across 3 AZ
- DocumentDB storage automatically grows in increments of 10GB up to 64TB
- Automatically scales to workloads with millions of requests per second

#### Amazon Neptune
- Fully managed graph DB
- A popular graph dataset would be a social network:
   - Users have friends
   - Posts have comments
   - Comments have likes from users
   - Users share and like posts
- HA across 3 AZ with up to 15 read replicas
- Build and run applications working with highly connected datasets - optimised for these complex and hard queries
- Can store up to billions of relations and query the graph with ms latency
- HA with replications across multiple AZs
- Great for knowledge graphs (e.g. Wikipedia), fraud detection, social networking

#### Amazon Keyspaces (for Apache Cassandra)
- Apache Cassandra is an open source NoSQL distributed DB
- A managed Appache Cassandra-compatible DB service
- Serverless, scalable, highly available , fully managed by AWS
- Automatically scale tables up/down based on the application's traffic
- Tables are replicated 3 times across multiple AZ
- Uses Cassandra Query Language (CQL)
- Single-digit ms latency at any scale, 1000s of requests per second
- Capacity: on-demand mode or provisioned mode with auto-scaling
- Encryption, backup, PITR up to 35 days
- Use cases: store IoT device info, time series data

#### Amazon QLDB
- Stands for "Quantum Ledger Database"
- Ledger is a book recording financial transactions
- Fully managed, serverless, HA, replication across 3 AZ
- Used to review history of all changes made to your application data over time
- Immutable system: no entry can be removed or modified, cryptographically verifiable
- 2-3x better performance than common ledger blockchain frameworks, manipulate data using SQL
- Difference with Amazon Managed Blockchain: no decentralisation component in accordance with financial regulations

#### Amazon Timestream
- Fully managed, fast, scalable, serverless timeseries database
- Automatically scales up and down to adjust capacity
- Store and analyse trillions of events per day
- 1000s times faster & 1/10th of the cost of relational DBs
- Scheduled queries, multi-measure records, SQL compatibility
- Data storage tiering: recent dat, kept in memory and historical data kept in cost-optimised storage
- Built in time series analytics functions (helps identify patterns in your data in near real time)
- Encryption in transit and at rest
- Use cases: IoT apps, operational applications, real-time analytics

# Data and Analytics

### Athena
- Serverless query service to analyse data stored in S3
- Uses standard SQL language to query files (built on Presto)
- Supports CSV, JSON, ORC, Avro, and Parquet
- Pricing is $5 per TB of data scanned
- Commonly used with Amazon Quicksight for reporting/dashboards
- Use cases: BI/analytics/reporting and analysis, query VPC flow logs, ELB logs, CloudTrail logs etc.
- Exam tip: analyse data in S3 using serverless SQL = use Athena

#### Amazon Athena - Performance Improvement 

- Use columnar data for cost savings (less scan)
   - Apache Parquet or ORC recommended
   - Huge performance improvement
   - Use Glue to convert your data to Parquet or ORC
- Compress data for smaller retreivals (bzip2, gzip, lz4, snapp, zlip, zstd)
- Partition datasets in S3 for easy querying on virtual columns
- Use larer files (> 128MB) to minimise overhead

#### Amazon Athena - Federated Query
- Allows you to run SQL queries across data stored in relational, non-relational, object, and custom data sources (AWS or on-prem)
- Uses Data Source Connectors that run on AWS Lambda to run Federated Queries (e.g. CloudWatch Logs, DynamoDB, RDS)
- Store the results in S3

## Redshift

### Redshift Overview
- Redshift based on Pg, but not used for OLTP
- It's OLAP - online analytical processing (analytics and data warehousing)
- 10x better performance than other data warehouses, scale to PBs of data
- Columnar storage of data instead of row based) & parallel query engine
- Pay as you go based on the instances provisioned
- Has a SQL interface for performing queries
- BI tools such as Quicksight or Tableau integrate with it
- vs Athena: faster for queries/joins/aggregations thanks to indexes

### Redshift Cluster
- Leader node: for query planning, results aggregation
- Compute node: for performing the queries, send results to leader
- You provision node size in advance
- You can use reserved instances for cost savings

### Redshift - Snapshots and DR
- Redshift has Multi AZ mode for some clusters
- Snapshots are point in time backups of a cluster, stored internally in S3
- You can restore a snapshot into a new cluster
- Automated: every 8 hours, every 5GB, or on a schedule - set retention
- Manual: snapshot is retained until you delete it
- You can configure Amazon Redshift to automatically copy snapshots (automated or manual) of a cluster to another AWS region
- Large inserts are much better when loading data into Redshift

### Redshift Spectrum
- Query data that is already in S3 without loading it
- Must have a Redshift cluster available to start the query
- The query is then submitted to thousands of Redshift Spectrum nodes

## OpenSearch (ElasticSearch)
- Successor to Amazon ElasticSearch
- In DynamoDB, queries only exist by primary keys or indexes
- With Opensearch you can search any field - even partial matches
- It's common to use OpenSearch as a compliment to another DB
- Two mode: managed cluster or serverless cluster
- Does not natively support SQL (can be enabled via plugin)
- Ingestion from Kinesis Data Firehose, AWS IoT, and CloudWatch Logs
- Security through Cognito & IAM, KMS encryption, TLS
- comes with OpenSearch Dashboards (visualisation)

## Elastic Map Reduce (EMR)
- Helps creating Hadoop clusters (big data) to analyse and process vast amounts of data
- Clusters can be made of hundreds of EC2 instances
- EMR comes bundled with Apache Spark, HBase, Presto, Flink
- EMR takes care of all the provisioning and configuration
- Auto-scaling and integrated with Spot instances
- Use cases: data processing, machine learning, web indexing, big data

### Node types and purchasing
- Master Node: Manage the cluster, coordinate, manage health- long running
- Core Node: run tasks and store data - long running
- Task Node (optional): just to run tasks - usually spot

Purchasing options:
- On-demand: reliable, predictable, won't be terminated
- Reserved (min 1 year): cost savings (EMR will automatically use if available)
- Spot instances: cheaper, can be terminated, less reliable
- Can have long-running clusters, or transient temporary cluster

## QuickSight
- Serverless machine learning powered business intelligence to create interactive dashboards
- Fash, automatically scalable, embedable, with per-session pricing

Use cases:
- Business analytics
- Building visualisations
- Perform ad-hoc analysis

- Integrated with RDS, Aurora, Athena, Redshift, S3
- In memory computation using SPICE engine if data is imported into QuickSight
- Enterprise edition: possibility to set up Column-Level security (CLS)

### QuickSight Integrations (data sources)

AWS Services:
- RDS
- Aurora
- Redshift
- Athena
- S3
- OpenSearch
- Timestream

SaaS:
- Salesforce
- JIRA

On-prem Databases (JDBC)

Imports:
- XLSX
- CSV
- JSON
- .TSV
- ELF & CLF log format

### QuickSight - Dashboard & Analysis
- Define usres (standard versions) and Groups (enterprise version) - these users and groups only exist within Quicksight, not IAM!
- A dashboard is:
   - A read only snapshot of analysis that you can share
   - preserves the configuration of the analysis (filtering, parameters, controls, sort)
   - You can share the analysis or the dashboard with users or groups
   - To share a dashboard, it must first be published
   - Users who see the dashboard can also see the underlying data

## AWS Glue
- Managed extract, transform, and load (ETL) service
- Useful to prepare and transform data for analytics
- full serverless service

S3 bucket or Amazon RDS DB --> Glue ETL --> Redshift Data Warehouse

### Convert data into Parquet format

S3 PUT --> S3 Bucket --> Import CSV --> Glue ETL --> Parquet --> Output S3 Bucket --> Analyse --> Amazon Athena

Also have event notifications on S3 PUT --> Lambda function (EventBridge works as an alternative)

### Glue - things to know at a high level
- Glue Job Bookmarks - prevent re-processing old data
- Glue Elastic views:
   - Combine and replicate data across multiple data stores using SQL
   - No custom code, Glue monitors for changes in the source data - serverless
   - Leverages a "virtual table" (materialised view)
   - Glue DataBrew: clean and normalise data using pre-bulit transformation
   - Glue Studio: new GUI to create, run and monitor ETL jobs in Glue
   - Glue Streaming: ETL (built on Apache Spark Structured Streaming): compatible with Kinesis Data Streaming, Kafka, MSK (managed Kafka)

## AWS Lake Formation
- Data lake = central place to have all your data for analytics purposes
- Fully managed service that makes it easy to set up a data lake in days
- Discover, cleanse, transform and ingest data into your Data Lake
- Automates many complex manual steps (collecting, cleansing, moving, cataloging data) and de-duplicate (using ML Transforms)
- Combine structured and unstructured data in the data lake
- OOTB source blueprints: S3, RDS, Relational and NoSQL DB
- Fine-grained access control for your applications (row and column level)
- Bulit on top of AWS Glue
- **Lake formation takes care of acccess control with column level security so only those who need to see what is necessary do no have access to more than that**

## Kinesis Data Analytics

### Kinesis Data Analytics for SQL applications

Sources:
- Kinesis Data Sreams
- Kinesis Data Firehose

SQL Statements --> Kinesis Data Analytics for SQL aps <-- Reference Data in S3

Sinks:
- Kinesis Data Streams --> AWS Lambda --> Anywhere OR  Applicatoins --> anywhere
- Kinesis Data Firehose --> S3 OR Redshift (Copy via S3) OR other Firehose destinations

- Real time analytics on Kinesis Data Streams & Firehose using SQL
- Add reference data from S3 to enrich streaming data
- Full managed, no servers to provision
- Automatic scaling
- Pay for actual consumption rate
Output:
- Kinesis Data Streams: create streams out of real-time analytics queries
- Kinesis Data Firehose: send analytics query results to destinations
Use cases:
- time series analytics
- Real-time dashboards
- Real time metrics

### Kinesis Data Analytics for Apache Flink
- Use Flink (Java, Scala, or SQL) to process and analyse streaming data
- Run any Apache Flink application on a managed cluster on AWS
   - Provisioning compute resources, parallel computation, automatic scaling
   - Application backups (checkpoints and snapshots)
   - Use any Apache Flink programming features
   - Flink does not read from Firehose (use Kinesis Analytics for SQL instead)

### Amazon Managed Streaming for Apache Kafka (Amazon MSK)
- Alternative to Amazon Kinesis
- Fully managed Apache Kafka on AWS
- Allows you to create, update, delete clusters
- MSK creates and manages Kafka brokers nodes and zookeeper nodes for you
- Deploy the MSK cluster in your VPC, multi-AZ (up to 3 for HA)
- Automatic recovery from common Apache Kafka failures
- Data stored on EBS volumes for as long as you want
- MSK Serverless
   - Run Apache Kafka on MSK without managing the capacity
   - MSK automatically provisoins resources and scales compute and storage

### Kinesis Data Streamsa vs Amazon MSK

|Kinesis Data Streams|Amazon MSK|
|-----------------------|---------------|
|1MB message size limit|1MB default, configure for higher (e.g. 10MB)|
|Data Streams with shards|Kafka topics with Partitions|
|Shard splitting & merging|Can only add partitions to a topic|
|TLS in-flight encryption|Plaintext or TLS in-flight encryption|
|KMS at rest encryption|KMS at rest encryption|

### Amazon MSK Consumers

Amazon MSK to:
- Kinesis Data Analytics for Apache Fink
- AWS Glue Streaming ETL Jobs (powered by Apache Spark Streaming)
- Lambda
- Or applications running on EC2 ECS or EKS

## Big Data Ingestion Pipeline
- We want the ingestion pipeline to be fully serverless
- We want to collect data in real time
- We want to transform the data
- We want to query the transformed data using SQL
- The reports created using the queries should be in S3
- We want to load that data into a warehouse and create dashboards

IoT Devices  (in real time) --> Amazon Kinesis Data Streams --> Amazon Kinesis Data Firehose (every 1 min) (--> <-- AWS Lambda) --> Ingestion Bucket (S3) --> SQS (optional) -- AWS Lambda --> triggers Athena --> Reporting bucket (also S3) --> QuickSignt or Redshift

### Big Data Ingestion Pipeline discussion

- IoT Core allows you to harvest data from IoT devices
- Kinesis great for real-time data collection
- Firehose helps with data delivery to S3 in near real time (1 min)
- Lambda can help Firehose with data transformations
- Amazon S3 can trigger notifications to SQS
- Lambda can subscribe to SQS (we could have connector S3 to Lambda)
- Athena is a serverless SQL service and results stored in S3
- Reporting bucket contains analysed data and can be used by reporting tool such as AWS QuickSight, Redshift etc

# Machine Learning

## Rekognition Overview
- Find objects, people, text, scenes in images and videos using ML
- Facial analysis and facial search to do user verification, people counting
- Create a database of "familiar faces" or compare against celebs

Use cases:
- Labeling
- Content Moderation
- Text detection
- Face Detection and Analysis (gender, age range, emotions)
- Face search and verification
- Celeb recognition
- Pathing (e.g. for sports game analysis)

### Rekognition - Content Moderation
- Detect content that is inappropriate, unwanted, or offensive (images and videos)
- Used in social media, broadcast media, advertising, and ecommerce
- Set a minimum confidence threshold for items that will be flaged
- Flag sensitive content for manual review in Amazon Augmented AI (A2I)
- Help comply with regulations

## Transcribe Overview
- Automatically convert speech to text
- Uses a deep learning process called automatic speech recognition (ARS) to convert speech to text quickly and accurately
- Automatically remove PII using redaction
- Supports Automatic Language Identification for multi-lingual audio
Use cases:
- transcribe customer service calls
- Automate closed captioning and subtitles

## Polly Overview
- The opposite of transcribe
- Turn text into lifelike speech using deep learning
- Allows you to create applications that talk

### Lexicon & SSML
- Customise the pronounciation of words with Pronounciation lexicons (stylised words and acronyms)
- Upload the lexicons and use them in the SynthesizeSpeech operation
- Generate speech from plain text or from documents marked up with Speeh Synthesis Markup Language (SSML) - enables more customisation
   - emphasizing specific words or phrases
   - phonetic pronounciation
   - newscaster style speaking

## Amazon Translate
- Natural and accurate language translation
- Amazon Translate allows you to localise content such as website and applications for international users and translate large volumes of text efficiently

## Lex + Connect Overview
Amazon Lex (same tech that powers Alexa):
- Automatic speech recognition (ASR) to convert speech to text
- Natural Language Understanding to recognise the intent of text, callers
- Helps build chat and call centre bots

Amazon Connect:
- Receive calls, create contact flows, cloud-based virtual contact center
- Can integrate with other CRM or AWS
- No upfront payments, 80% cheaper than traditional contact center solutions

## Comprehend Overview
- For Natural Language Processing - NLP
- Fully managed and serverless service
- Uses machine learning to find insights and relationships in text
   - Language of text
   - Extracts key phrases, places, people, brands or events
   - Understands how positive or negative text is
   - Analyses text using tokenisation and parts of speech
   - Automatically organises a collection of text files by topic
Sample use cases:
- Analyse customer interactoins (emails) to find what leads to a positive or negative experience
- Create and group articles by topics that Comprehend will uncover

## Comprehend Medical Overview
Amazon Comprehend Medical detects and returns useful information in unstructured clinical text:
- Physician's notes
- Discharge summaries
- Test results
- Case notes

- Uses NLP to detect PHI with DetectPHI API
- Store your documents in S3, analyse real time data with Kinesis Data Firehose or use Amazon Transcribe to transcribe patient narratives into text that can be analysed by Amazon Comprehend Medical

## SageMaker
- Fully managed service for devs/data scientists to build ML models
- Typically difficult to do all the processes in one place + provision servers
- ML process (simplified): predicting your exam score

## Forecast Overview
- Fully managed service that uses ML to deliver highly accurate forecasts
- Example: predict future sales of a raincoat
- 50% more accurate than looking at the data itself
- Reduce forecasting time from months to hours
- Uses cases: Product demand planning, financial planning, resource planning

## Kendra Overview
- Fully managed document search service powered by ML
- Extract answers from within a document
- Natural language search capabilities
- Learn from user interactions/feedback to promote preferred results (incremental learning)
- Ability to manually fine-tune search results

## Personalise Overview
- Fully managed ML service to build apps with real time personalised recommendations
- Example: personalised product recommendations
- Same technology used by Amazon.com
- Integrates into existing websites, applications, SMS etc
- Implement in days not months
- Use cases: retails stores, media, entertainment

## Textract
- Automatically extracts text, handwriting, and data from any scanned documents using AI and ML
- Extract data from forms and tables
- Read and process any type of document (PDF, images)
Uses cases:
- Financial Services (e.g. invoices, financial reports)
- Healthcare (e.g. medical records, insurance claims)
- Public sector (tax forms, ID docs, passports)

# AWS Montioring & Audit: CloudWatch, CloudTrail & Config

### CloudWatch Metrics
- CloudWatch provides metrics for every service in AWS
- Metric is a variable to monitor (CPUUtilization, Networkln)
- Metrics belong to namespaces
- Dimension is an attribute of a metric (instance id, environment etc)
- Up to 30 dimensions per metric
- Metrics have timestamps
- Can create CloudWatch dashboard of metrics
- Can create CloudWatch Custom Metrics (for RAM, as an example)

### CloudWatch Metric Streams
- Continually stream CloudWatch metrics to a destination of your choice will near real-time delivery and low latency
   - Amazon Kinesis Data Firehose (and then destinations)
   - 3rd party service provider such as DataDog, New Relic, or Splunk
- Option to filter metrics to only stream a subset of them

### CloudWatch Logs
- Log groups: arbitrary name, usually representing an application
- Log stream: instances within application/log files/containers
- Can define log expiration policies (never expire, or 1 day to 10 years)
- CloudWatch Logs can send logs to:
   - S3 (exports)
   - Kinesis Data Streams
   - Kinesis Data Firehose
   - AWS Lambda
   - OpenSearch
- Logs are encrypted by default
- Can set up KMS based encryption with your own keys

### CloudWatch Logs - Sources
- SDK, CloudWatch Logs Agent, CloudWatch Unified Agent
- Elastic Beanstalk: collection of logs from application
- ECS: collection from containers
- AWS Lambda: collection from function logs
- VPC Flow Logs: VPC specific logs
- API Gateway
- CloudTrail based on filter
- Route53: Log DNS queries

### CloudWatch Log Insights
- Search and analyse log data stored in CloudWatch Logs
- E.g. find specific IP inside log
- Provides purpose built query language
   - Automatically discovers fields from AWS services and JSON log events
   - Fetch desired event fields, filter based on conditions, calculate aggregate statistics, sort events etc.
   - Can save queries and add them to CloudWatch dashboards
   - Can query multiple log groups in different AWS accounts
   - Query engine, not real-time engine

### CloudWatch Logs - S3 Export
- Log data can take up to 12 hours to become available for export
- API is called CreateExportTask
- Not near-real time or real time, use log subscriptions instead...

### CloudWatch Log Subscriptions
- Get real time log events from CloudWatch Logs for processing and analysis
- Send to Kinesis Data Streams, Kinesis Data Firehose, or Lambda
- Subscription Filter - filter which logs are events delivered to your destination
- Cross-account subscription: send log events to resources in a different AWS account (KDS, KDF)

## CloudWatch Logs for EC2
- By default, no longs from your EC2 machine will go to CloudWatch
- Need to run a CloudWatch agent on EC2 to push log files
- Make sure IAM perms are correct
- The CloudWatch log agent can be set up on-prem

### CloudWatch Logs Agent & Unified Agent
For virtual servers (EC2 instances, on-prem servers)
   - CloudWatch Logs Agent
   - Old version of agent
   - Can only send to CloudWatch Logs

CloudWatch Unified Agent:
- Collect additional system level metrics like RAM, processes etc.
- Collect logs to send to CloudWatch logs
- Centeralised config using SSM Parameter Store

### CloudWatch Unified Agent Metrics
- Collected directly on your Linux server/EC2 instance
- CPU (active, guest, idle, system user)
- Disk metrics (free, used, total), Disk IO (reads, writes, bytes, iops)
- RAM (free, inactive, used, total, cached)
- Netstat (number of TCP and UDP connections, packets, bytes)
- Processes (total, dead, idle, running)
- Swap space (free, used, used %)
- Reminder: OOTB metrics for EC2 - disk, cpu, network

## CloudWatch Alarms
- Alarms used to trigger notifications for any metric
- Various options (sampling, % max, min, etc)
- Alarm states: OK, INSUFFICIENT_DATA, ALARM
- Period: length of time in sec to eval metric, high resolution custom metrics: 10s, 30s, or multiples of 60s

### CloudWatch Alarm Targets
- Stop, Terminate, Reboot, or Recover an EC2 instance
- Trigger an autoscaling action
- Send notification to SNS

### CloudWatch Alarms - Composite Alarms
- CloudWatch Alarms are on a single metric
- Composite alarms are monitoring the states of multiple other alarms
- AND and OR conditions
- Helpful to reduce alarm noise by creating complex composite alarms

### EC2 Instance Recovery
Status Check:
- Instance status = check the EC2 VM
- System status = check the underlying hardware
- Recovery: same private, public, elastic IP, metadata, placement group

### CloudWatch Alarm: good to know
- Alarms can be created based on CloudWatch Logs Metrics Filters
- To test alarms and notifications, set the alarm state to Alarm using CLI: 

```shell
aws cloudwatch set-alarm-state --alarm-name "myalarm" --state-value ALARM --state-reason "testing purposes"
```

## EventBridge Overview (formerly CloudWatch Events)
- Schedule: cron jobs (scheduled scripts)
- Event Patterm: Event rules to react to a service doing something
- Trigger Lambda functions, send SQS/SNS messages...

### Amazon EventBridge
- Event buses can be accessed by other AWS accounts using Resource-based policies
- You can archive events (all/filter) sent to an event bus (indefinitely, or set period)
- Ability to replay archived events

### Amazon EventBridge - Schema Registry
- EventBridge can analyse events in your bus and infer the schema
- Schema Registry allows you to generate code for your application that will know in advance how data is structured in the event bus
- Schema can be versioned

### EventBridge- Resource based policy
- Manage perms for a specific Event Bus
- Example: allow/deny events from another AWS account or region
- Use case: aggregate all events from your AWS org in a single AWS account or region

## CloudWatch Insights & Operational Visibility

### CloudWatch Container Insights
- Collect, aggregate, summarise metrics and logs from containers
- Available for containers on ECS, EKS, Kube  platforms on EC2, and Fargate (both ECS and EKS)
- In EKS and Kube, CloudWatch insights is using a containerised version of the CloudWatch agent to discover containers

### CloudWatch Lambda Insights
- Monitoring and troubleshooting solution for serverless applications running on AWS Lambda
- Collects, aggregates, and summarises system-level metrics including CPU time, memory, disk, and network
- Collects, aggregates, and summarises diagnostic info such as cold starts and Lambda worker shut downs
- Lambda Insights is provided as a Lambda Layer

### CloudWatch Contributor Insights
- Analyse log data and create time series that display contributor data
- Helps find top talkers and understand who or what is impacting system performance
- Works for any AWS generated logs
- Can build rules from scratch or use sample rules AWS created - leverages your CloudWatch logs
- CloudWatch provides built-in rules you can use to analyse metrics from other AWS services

### CloudWatch Application Insights
- Provides automated dashboards that show potential problems with monitored applications to help isolate ongoing issues
- Your applications run on EC2 instances with select technologies only (Java, .NET, MS IIS Web Server, DBs)
- Can use other AWS resources such as EBS, RDS, ELB, ASG, Lambda, SQS, DynamoDB, S3 bucket, ECS, EKS, SNS, API Gateway
- Powered by SageMaker
- More visibility into your app health to reduce time taken to troubleshoot and repair
- Findings +alerts send to EventBridge and SSM OpsCenter

### CloudWatch Insights and Operational Visibility

**CloudWatch Container Insights**:
- ECS, EKS, Kube on EC2, Fargate need agent for Kube
- Metrics and logs

**CloudWatch Lambda Insights**:
- Detailed metrics to troubleshoot serverless apps

**CloudWatch Contributors Insight**:
- Find Top-N contributors through CloudWatch logs

**CloudWatch App Insights**:
- Automatic dashboard to troubleshoot your app and related AWS services

## CloudTrail Overview
- Provides governance, compliance, and audit for your AWS account
- Enabled by default
- Get history of events/API calls made within your AWS account by console, SDK, CLI, or AWS services
- Can put logs from CloudTrail into CloudWatch Logs or S3
- A trail can be applied to all regions (default) or single region
- If a resource is deleted in AWS, look at CloudTrail first

### CloudTrail Events

**Management Events**:
- Operations performed on resources in your AWS account e.g. configuring security (IAM AttachRolePolicy), configuring rules for routing data (EC2 CreateSubnet)
- By default trails configed to log management events
- Can separate Read events (that don't modify resources) from write events

**Data Events**:
- By default are not logged (high vol operations)
- S3 object-level activity (e.g. GetObject, DeleteObject, PutObject) - can separate R/W
- AWS Lambda function execution activity (Invoke API)

**CloudTrail Insights**:
- Enable to detect unusual activity in your account e.g. inaccurate resource provisioning, hitting service limits, bursts of IAM actions, or gaps in maintenance
- Analyses normal management events to create baseline
- Continuously analyses write events to detect unusual patterns like anomalies in CloudTrail console, event sent to S3, EventBridge event generated

### CloudTrail Events Retention
- Events stored for 90 days
- To keep events longer, log them to S3 and use Athena

## CloudTrail - EventBridge Integration

User calls DeleteTable API to DynamoDB --> API call logged and intercepted by CloudTrail --> Event continues on to EventBridge --> Alert sent to SNS

### EventBridge + CloudTrail

User assumes IAM role --> API call logged (intercepted by CloudTrail) -->  event generated by EventBridge --> Notification via SNS

User edits SG inbound rules on EC2 --> API call logged (intercepted by CloudTrail) --> event generated by EventBridge --> Notification via SNS

## AWS Config - Overview
- Helps with auditing and recording compliance of your AWS resources
- Helps record configurations and changes over time
- Can receive alerts (SNS notifications) for any changes
- Is a per-region service
- Can be aggregated across regions and accounts
- Can store config data in S3, analysis with Athena

### Config Rules
- Can use AWS managed config rules (over 75)
- Can make custom config rules (defined in AWS Lambda)
- Rules can be evaled/triggered for each config change and/or at regular time intervals
- AWS Config rules do not prevent actions from happening (there's no deny)
- Pricing: no free tier, $0.003 per config item recorded per region, $0.001 per config rule per eval per region

### Config Rules - Remediations
- Automate remediation of non-compliant resources using SSM Automation Documents
- Use AWS managed automation documents or create custom ones (can also create ones that involve Lambda)
- Can set remediation retries if resource is still non-compliant after auto-remediation

### Config Rules - Notifications
- Use EventBridge to trigger notifications when AWS resources are non-compliant

## CloudTrail vs CloudWatch vs Config

**CloudWatch**:
- Performance monitoring (metrics, CPU, network) and dashboards
- Events and alerting
- Log Aggregation & analysis

**CloudTrail**:
- Record API calls made within your Account by everyone
- Can define trails for specific resources
- Global service

**Config**:
- Record config changes
- Evaluate resource rules against compliance rules
- Get timeline of changes and compliance

In the context of an Elastic Load Balancer:

**CW**:
- Monitoring incoming connections metric
- Visualise error codes as % over time
- Make dashboard to get idea of LB performance

**Config**:
- Track security group rules for LB
- Track config changes for LB
- Ensure SSL cert always assigned to LB (compliance)

**CloudTrail**:
- Track who made any changes to LB with API calls

## IAM - Advanced

### AWS Organisations
- Global service
- Allows management of multiple AWS accounts
- Main account is management account - other accounts are members (can only be part of one org)
- Consolidated billing across all accounts with single payment method
- Pricing benefits from aggregated usage (vol discount for EC2, S3)
- Shared reserved instances and Savings plan discounts across accounts
- API available to automate AWS account creation

Advantages:
- Multi account vs one account Multi VPC
- Use tagging standards for billing purposes
- Enable CloudTrail on all accounts, end logs to central S3 account
- Send CloudWatch Logs to central logging account
- Establish cross account roles for admin purposes
Security: Service Control Policies:
- IAM policies applied to OU or accounts to restrict users and roles
- Do not apply to management account (has full admin)
- Must have an explicit allow - does not allow anything by default - like IAM

## IAM - Advanced Policies

### IAM Conditions
- Can use things such as aws:SourceIp to restrict the client from which the API calls are being made
- Or we can use things like aws:RequestedRegion to restrict the region API calls are being made to

### IAM Roles vs Resource Based Policies
Cross account:
- attach a resource based policy to a resource (e.g. S3 bucket policy)
- OR using a role as a proxy

- When you assume a role (user, application, or service), you give up your original permissions assigned to the role
- When using a resourced-based policy, the principal doesn't have to give up permissions

### Amazon EventBridge - Security
- When a rule runs, it needs permissions on the target
- Resource based policy: Lambda, SNS, SQS, CloudWatch Logs, API Gateway
- IAM role: Kinesis stream, Systems Manager Run Command, ECS task etc

**SNS, SQS, Lambda are for resource based policies, Kinesis data streams are using an IAM role.

## IAM - Policy Evaluation Logic

### Permission Boundaries
- IAM Permission Boundaries are supported for users and roles (not groups)
- Advance feature to use a managed toplicy to set the maximum permissions an IAM entity can get
- Can be used in combinations of AWS Orgs SCP
Use cases:
- Delegate responsibilities to non administrators within their permission boundaries, for example create new IAM users
- Allow developers to self-assign policies and manage their own permissions, while making sure they can't "escalate" their privileges
- Useful to restrict one specific user (instead of a whole account using Orgs & SCP)

## IAM Identity Center

- SSO for your org on AWS
- Business cloud applications
- SAML2 enabled applications
- EC2 Windows instances
- Identity providers
  - Built-in identity store in IAM Identity Center
  - 3rd party: AD, OneLogin, Okta

### Fine-grained permissions and assignments

Multi-account Perms:
- Manage access across AWS accounts in your AWS org
- Permission Sets - a collection of one or more IAM Policies assigned to users and groups to define AWS access

Application assignments:
- SSO access to many SAML 2.0 business apps
- Provide required URLs, certifications and metadata

Attribute-Based-Access-Control (ABAC):
- Fine-grained permissions based on user's attributes stored in IAM Identity Center Indentity Store
- Example: cost center, title, locale
- Use case: Define permissions once, then modify AWS access by changing the attributes

## AWS Directory Services

AWS Managed Microsoft AD
- Create your own AD in AWS, manage users local, supports MFA
- Establish "trust" connections with your on-prem AD

AD Connector
- Directory Gateway (proxy) to redirect to on-prem AD, supports MFA
- Users managed on the on-prem AD

Simple AD
- AD-compatible managed directory on AWS
- Cannot be joined with on-prem AD

## AWS Control Tower
- Easy way to set up and govern a secure and compliant multi-account AWS environment based on best practices
- AWS Control Tower users AWS Organisations to create accounts

Benefits:
- Automate the set up of your environment in a few clicks
- Automate ongoing policy management using guardrails
- Detect policy violations and remediate them
- Montior compliance through an interactive dashboard

### AWS Control  Tower - Guardrails
- Provides ongoing governance for your Control Tower environment (AWS accounts)
- Preventive Guardrail - using SCPs (e.g. restrict regions across all accounts)
- Detective Guardrail - using AWS config (identify untagged resources)

# AWS Security & Encryption - KMS, SSM Parameter Store, CloudHSM, Shield, WAF

## Encryption 101

### Encryption in flight (SSL)
- Data encrypted before sending and decrypted after receiving
- SSL certificates help with encryption (HTTPS)
- Encryption in flight ensures no MITM can happen

### Server side encryption at rest
- Data encrypted after being received by server
- Data decrypted before being sent
- It is stored in an encrypted form thanks to key
- Encryption/decryption keys must be managed somewhere and the server must have access to it

### Client side encryption
- Data is encrypted by the client and never decrypted by the server
- Data will be decrypted by a receiving client
- The server should not be able to decrypt the data
- Could leverage Envelope Encryption

## AWS KMS Overview
- Any time you hear "encryption" for an AWS service, most likely KMS
- AWS manages encryption keys for us
- Fully integrated with IAM for authorization
- Easy way to control access to your data
- Able to audit KMS Key usage using CloudTrail
- Seamlessly integrated into most AWS services
- Never store your secrets in plain text!
- KMS Key encryption also available via API calls
- Encrypted secrets can be stored in environment variables

### KMS Key Types

Symmetric (AES-256):
- Single encryption key that is used to encrypt and decrypt
- AWS services that are integrated with KMS use Symmetric CMKs (Customer Master Key)

Asymmetric (RSA & ECC key pairs):
- Public (Encrypt) and Private (Decrypt) pair
- Used to encrypt/decrypt or sign/verify operations
- Public key downloadable, but can't access private key unencrypted
- Use case: encryption outside of AWS by users who can't call the KMS API

### AWS KMS (Key Management Service)

Types of KMS Keys:
- AWS owned (free); SSE-S3, SSE-SQS, SSE-DDB (default key)
- AWS Managed Key (free): (aws/service name e.g. aws/rds)
- Customer managed keys created in KMS: $1/month + pay for API calls to KMS (0.003 per 1000 calls)

Automatic key rotation:
- AWS managed KMS key: automatic every year
- Customer managed KMS: (must be enabled) automatic every year
- Imported KMS key: manual rotation possible using alias

**! KMS Keys are scoped per region - if you're copying snapshots across regions, after copying the snapshot is re-encrypted with a different KMS Key which AWS does for you**

### KMS Key Policies
- Control access to KMS keys similar to S3 bucket policies
- Difference: you cannot control access without them

Default KMS Key policy:
- Created if you don't provide a specific policy
- Complete access to the key to the root user = entire AWS account

Custom KMS Key Policy:
- Define users, roles that can access the KMS key
- Define who can administer the key
- Useful for cross-account access of your KMS key

### Copying snapshots across accounts

1. Create snapshot encrypted with your own KMS key (customer managed)
2. Attach a KMS Key Policy to authorise cross-account access
3. Share encrypted snapshot
4. (in target) create a copy of the snapshot, encrypt it with a CMK in your account
5. Create a volume from the snapshot

## KMS Multi-region keys
- same key but ARN has region prefix
- Identitical keys in different AWS regions that can be used interchangeably 
- Multi-region keys have the same Key ID, key material, automatic rotation
- Encrypt in one region, decrypt in other regions
- No need to re-encrypt or making cross region api calls
- KMS multi-region are NOT global (Primary + replicas)
- Each multi-region key is managed independently
- Use cases: global client-side encryption, encryption on Global DynamoDB, Global Aurora

### DynamoDB Global Tables and KMS Multi-region keys client side encryption

- We can encrypt specific attributes client-side in our DynamoDB table using the Amazon DynamoDB Encryption client
- Combined with Global Tables, the client-side encrypted data is replicated to other regions
- If we use a multi-region key, replicated in the same region as the DynamoDB Global table, then clients in these regions can use low-latency API calls to KMS in their region to decrypt the data client side
- Using client-side encryption we can protect specific fields and guarantee only decryption if the client has access to an API key

### Global Aurora and KMS Multi-region keys client side encryption
- We can encrypt specific attributes client-side in our Aurora table using the AWS Encryption SDK
- Combined with Aurora Global Tables, the client-side encrypted data is replicated to other regions
- If we use a multi-region key replicated in the same region as the Global Aurora DB then clients in these regions can use low-latency API calls to KMS in their region to decrypt the data client-side
- Using client-side encryption we can protect specific fields and guarantee only decryption if the client has access to an API key, we can protect specific fields even from DB admins

## S3 Replication with Encryption - Considerations
- Unencrypted objects and objects encrypted with SSE-S3 are replicated by default
- Object encrypted with SSE-C (customer provided key) are never replicated
- For objects encrypted with SSE-KMS you need to enable the option
   - Specify which KMS Key to encrypt the objects within the target bucket
   - Adapt the KMS Key Policy for the target key
   - An IAM Role with kms:Decrypt for the source KMS key, kms:Encrypt for target KMS key
   - Might get KMS throttling errors - ask for a service quotas increase
   - Can use multi-region KMS keys but currently treated as independent keys by S3 (object will still be decrypted and then encrypted)

## AMI Sharing Process Encrypted via KMS

1. AMI in source account encrypted with KMS key from source agent
2. Must modify image attribute to add a launch permission which corresponds to the specified target AWS account
3. Must share KMS keys used to encrypt the snapshot the AMI references, with the target account/IAM role
4. IAM role/user in target account must have permissions to describeKey, ReEncrypted, CreateGrant, Decrypt
5. When launching an EC2 instance from the AMI, optionally the target account can specify a new KMS key in its own account to re-encrypt the volumes

## SSM Parameter Store Overview
- Secure storage for configuration and secrets
- Optional seamless encryption using KMS
- Serverless, scalable, durable, easy SDK
- Version tracking of configurations/secrets
- Security through IAM
- Notifications with Amazon EventBridge
- Integration with CloudFormation

### SSM Parameter Store Hierarchy
- /my-department
   - my-app/
      - dev/
         - db-url
         - db-password
     - prod/
        - db-url
        - db-password
    - other-app/
- /other-department/
- /aws/reference/secretsmanager/secret_ID_in_secrets_manager
- /aws/service/ami-amazon-linux-latest/amzn-2-ami-hvm-x86_64-gp2 (public)

### Standard and advanced parameter tiers

| |Standard|Advanced|
|-|---------|-----------|
|Total no. params allowed (per AWS acc and region)|10,000|100,000|
|Maximum size of a param value|4KB|8KB|
|Param policies available|No|Yes|
|Cost|No additional charge|Charges apply|
|Storage pricing|Free|0.005 per advanced param per month|

### Parameters Policies (for advanced params)
- Allow to assign a TTL to a parameter to force updating or deleting sensitive data such as passwords
- Can assign multiple policies at a time

## AWS Secrets Manager Overview
- Newer service meant for storing secrets
- Capability to force rotation of secrets every X days
- Automate generation of secrets on rotation (uses Lambda)
- Integration with RDS (MSQL, Pg, Aurora)
- Secrets encrypted using KMS
- Mostly meant for RDS integration

### AWS Secrets Manager - Multi-Region Secrets
- Replicate secrets across multiple AWS regions
- Secrets Manager keeps read replicas in sync with the primary secret
- Ability to promote a read replica Secret to standalone secret
- Use cases: multi-region apps, DR, multi-region DB

## AWS Certificate Manager (ACM)
- Easily provisoin, manage, and deploy TLS certificates
- Provide in-flight encryption for websites (HTTPS)
- Supports both public and private TLS certs
- Free of charge for public TLS certs
- Automated TLS cert renewal
- Integrations with:
   - ELB
   - CloudFront Distribution
   - APIs on API Gateway
- Cannot use ACM with EC2 (can't be extracted)

### ACM - Requestion Public Certs

1. List domain names to be included in cert
   - FQDN
   - Wildcard?
2. Select Validation method: DNS or email
   - DNs validation preferred (uses CNAME e.g. in Route53)
   - Email validation will send emails to contact addresses in WHOIS DB
3. Wait a few hours for verification to happen
4. Public cert will be enrolled for automatic renewal
   - ACM automatically renews ACM generated certs 60 days before expiry

### ACM - Importing Public Certs

- Option to generate the certificate outside of ACM and then import it
- No auto renewal, must import a new cert before expiry
- ACM sends daily expiration events starting at 45 days prior to expiration (# of days can be configed, events are seen in EventBridge)
- AWS Config has a managed rule named acm-certiicate-expiration-check to check for expiring certs (configurable number of days)

### ACM - Integration with API Gateway
- Create a custom domain name in API Gateway
Edge-optimised (default): for global clients
- Requests routed through CloudFront edge locations
- API gateway still lives in 1 region
- TLS cert must be in same region as CloudFront (us-east-1)
- Then set up CNAME or A-Alias (better) in R53
Regional
- For clients within same region
- TLS cert must be imported on API Gateway in same region as API stage
- Set up CNAME or A-alias (better) in R53

## Web Application Firewall (WAF)
- Protects your web applications from common web exploits (Layer 7)
- Layer 7 is HTTP (vs Layer 4 that is TCP/UDP)
Deploy on:
- ALB
- API Gateway
- CloudFront
- AppSync GraphQL API
- Cognito User Pool

Define Web ACL rules:
- IP set: up to 10,000 IPs - use multiple rules for more IPs
- HTTP headers, HTTP body, or URI strings protects from common attacks like SQLi or XSS
- Size constraints - geomatch (block countries)
- Rate-based rules (to count occurrences of events) - for DDoS protection

- Web ACL are regional except for CloudFront
- A rule group is a reusable set of rules that you can add to a web ACL

### WAF - Fixed IP while using WAF with LB
- WAF does not support the network load balancer (L4)
- Can use Global Accelerator for fixed IP and WAF on the ALB

## Shield - DDoS Protection

AWS Shield Standard:
- Free service activated for every AWS customer
- Provides protection from attacks sch as SYN/UDP floods, reflection attacks etc

AWS Shield Advanced:
- Optional DDoS mitigation service (3k per month)
- Protect against more sophisticated attacks on EC2, ELB, CloudFront, Global Accelerator, and R53
- 24/7 access to AWS DDoS response team
- Protect against higher fees during usage spikes due to DDoS
- Shield Advanced automatic application layer DDoS mitigation automatically creates, evaluates, and deployes AWS WAF rules to mitigate layer 7 attacks

## AWS Firewall Manager
- Manage rules in all accounts of an AWS org
- Security policy: common set of security rules:
  - WAF rules (ALB, API-G, CloudFront)
  - AWS Shield Advanced (ALB, CLB, NLB, E-IP, CloudFront)
  - Security groups for EC2, ALB, and ENI resources in VPC
  - AWS Network Firewall (VPC level)
  - R53 Resolver DNS Firewall
  - Policies created at regional level
  - **Rules appplied to new resources as they are created (good for compliance) across all future accounts in your org**

### WAF vs Firewall Manager vs Shield
- WAF, Shield, and Firewall manager are used together for comprehensive protectoin
- define your web acl rules in WAF
- For granular protection of your resources, WAF alone is correct choice
- If you want to use AWS WAF across accounts, accelerate WAF configuration, or automate the protection of new resources then use Firewall Manager with WAF
- Shield Advanced adds additional features on top of WAF such as dedicated support from Shield Response team and advanced reporting
- If you're prone to frequent DDoS, consider purchasing Shield Advanced

## Amazon GuardDuty
- Intelligent Threat discovery to protect your AWS account
- Uses ML algorithms, anomaly detection, 3rd party data
- One click to enable (30 day trial), no need to install software
Input data includes:
- CloudTrail event logs - unusual API calls, unauthorised deployments
- cloudTrail Management Events - create VPC subnet, create trail
- CloudTrail S3 data events  - get object, list object, delete object
- VPC flow logs - unusual internet traffic or IPs
- DNS logs - compromised EC2 instances
- Optional features: EKS audit logs, RDS & Aurora, EBS, Lambda, S3

- Can set up EventBridge rules to be notified in case of findings
- EventBridge rules can target AWS Lambda or SNS
- Can protect against Crypto attacks (has dedicated finding)

### Amazon Inspector
- Automated security assessments
- For EC2 instances:
   - Leveraging the SSM agent
   - Analyse against unintended network access
   - Analyse the running OS against known vulns
- For container images push to ECR
   - Assessment of images as they are pushed
- For Lambda funtions:
   - Identifies software vulns in function code and package dependencies
   - Assessment of functions as they are deployed
- Reporting & integrations with AWS security hub
- Send findings to EventBridge

### What does Amazon Inspector Evaluate?
- Remember: only for EC2 instances, container images, and lambda functions
- Continuous scanning of infra, only when needed
- Package vulns (EC2, ECR & Lambda) - DB of CVE
- Network reach-ability (EC2)
- A risk score is associated with all vulns for prioritisation

## Amazon Macie
- A fully managed data security and privacy service that uses machine learning and pattern matching to discover and protect your sensitive data in AWS
- Macie helps identify and alert you to sensitive data like PII in S3 buckets

# Networking - VPC

## CIDR, Private IP vs Public IP
- Classless inter-domain routing - a method for allocating IPs
- Used in security group rules and AWS networking in general
- Help define an IP range

### Understanding CIDR - IPv4
- A CIDR consists of two components:
   - Base IP (Represents an IP contained in the range)
   - Subnet mask (defines how many bits can change in the IP) e.g. /0 /24 /32
Can take two forms:
- /8 --> 255.0.0.0
- /16 --> 255.255.0.0
- /24 --> 255.255.255.0
- /32 --> 255.255.255.255

### Understanding CIDR - Subnet Mask
- the subnet mask allows part of the underlying IP to get additional next values from the base IP

192.168.0.0 /32 --> Allows for 1 IP (2^0) --> 192.168.0.0
192.168.0.0 /31 --> Allows for 2 IP (2^1) --> 192.168.0.0 -> 193.168.0.1

and so on and so on

**Quick memo**:
 /32 - no octet can change
 /24 - last octet can change
 /16 - last 2 octets can change
 /8 - last 3 octets can change

### Public vs Private IP (IPv4)
- The Internet Assigned Numbers Authority (IANA) established certain blocks of IPv4 addresses for the user of private (LAN) and public (internet) addresses

Private IP can only allow certain values:
- 10.0.0.0 - 10.255.255.255 (10.0.0.0/8) <-- in big networks
- 172.16.0.0 - 172.31.255.25 (172.16.0.0/12) <-- AWS default VPC in that range
- 192.168.0.0 - 192.168,255,255 (192.168.0.0/16) <-- home networks
- All rest of IP addresses on internet are public

## Default VPC Walkthrough
- All new AWS accounts have a default VPC
- New EC2 instances are launched into the default VPC if no subnet is specified
- Default VPC has internet connectivity and all EC2 instances inside it have public IPv4 addresses
- We also get a public and private IPv4 DNS name

### VPC in AWS - IPv4
- VPC = Virtual Private Cloud
- Can have multiple VPCs in an AWS region (max 5 per region - soft limit)
- Max. CIDR per VPC is 5 (1 for each)
   - Min size is /28 (16 IP)
   - Max size is /16 (65536 IP)
- Because VPC is private, only the Private IPv4 ranges are allowed (see above)
- Your VPC CIDR should not overlap with your other networks (e.g. corp network)

## Subnet Overview

### VPC - Subnet (IPv4)
- AWS reserves 5 IPs (first 4 and last 1) in each subnet that cannot be assigned to an EC2 instance:
Assuming CIDR block is 10.0.0.0/24, reserved are:
- 10.0.0.0 - Network address
- 10.0.0.1 - reserved for VPC router
- 10.0.0.2 - reserved for DNS
- 10.0.0.255 - Network Broadcast

Just like Azure

Exam tip - if you need 29 IPs for EC2 instances you can't choose subnet size of /27! You need to choose /26

## Internet Gateway
- Allows resources (e.g. EC2 instances) in a VPC to connect to the internet
- Scales horizontally, HA, redundant
- Must be created separately from VPC
- One VPC can only be attached to one IGW and vice versa
- Internet Gateways on their own do not allow internet access - route tables need to be edited

## Bastion Hosts
- We can use a Bastion Host to SSH into our private EC2 instances
- The bastion is in the public subnet which is then connected to all other private subnets
- Bastion Host security group must allow inbound from the intenret on port 22 from restricted CIDR - e.g. public CIDR of your corp
- Security group of EC2 instances must allow the security group of the bastion host or the private IP of the bastion host

## NAT Instance
- NAT = Network Address Translation
- Allows EC2 instances in private subnets to connect to the internet
- Must be launched in a public subnet
- Must disable EC2 setting: Source/Destination check
- Must have Elastic IP attached
- Route Tables must be configured to route traffic from private subnets to the NAT instance

### Comments
- Pre-configed Linux AMI is available but reached end of standard support on Dec 31st 2020
- Not HA/resilient OOTB - need to create ASG in multi-az + resilient user-data script
- Internet traffic bandwith depends on EC2 instance type
- Must manage security groups and rules:
   - Inbound: 
   - allow HTTP/S traffic coming from private subnets
   - Allow SSH from home network (acess provided via internet gateway)
   - Outbound:
   - Allow HTTP/S traffic from internet

## NAT Gateway
- AWS managed NAT, higher bandwidth, HA, no admin
- Pay per hour for usage and bandwidth
- NATGW is created in a specific AZ, uses E-IP
- Can't be used by EC2 instance in the same subnet (only from other)
- Requires IGW (Private subnet --> NATGW --> IGW)
- 5Gbps of bandwith with automatic scaling up to 45 Gbps
- No security groups to manage/required

### NAT Gateway with HA
- NAT Gateway is resilient within a single AZ
- Must create multiple NAT Gateways in multiple AZs for fault-tolerance
- No cross-AZ failover needed because if an AZ goes down it doesn't need NAT

## NACL & Security Groups
- NACL are like a firewall which control traffic from and to subnets
- One NACL per subnet, new subnets are assigned the default NACL
You define NACL rules:
   - Rules have a number (1-32766), higher presidence with lower number
   - First rule match drives decisoin
   - Last rule is an asterisk and denies a request in case of no rule match
   - AWS recommends adding rules by incrememt of 100
- Newly created NACLs will deny everything
- NACL are a great way of blocking a specific IP at subnet level

### Default NACL
- Accepts everything inbound/outound with the subnets it's associated with
- Do not modify default NACL - create custom ones

### Ephemeral Ports
- For any two endpoints to establish a connection they must use ports
- Clients connect to a defined port and expect a response on an ephemeral port
- Different OS use different port ranges:
   - IANA & Win: 10 --> 49152 - 65535
   - Many Lin kernels --> 32769 - 60999

### Security Group vs NACLS

|Security Group|NACL|
|---------------|------|
|Operates at instance level|Operates at subnet level|
|Supports allow rules only|Supports allow and deny rules|
|Stateful: return traffic automatically allowed, regardless of rules|Stateless: return traffic must be explicitly allowed (think ephemeral ports)|
|All rules evaled before deciding whether to allow traffic|Rules evaled in order (lowest to highest) when deciding whether to allow traffic - first match wins|
|Applies to an EC2 instance when specified by someone|Automatically applies to all EC2 instances in the subnet it is associated with|

## VPC Peering
- Privately connect two VPCs using AWS network
- Make them behave as if they were in the same network