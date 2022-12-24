# AWS Solution Architect Certification Notes

These are my note I took from take the A Cloud Guru AWS Certified Solutions Architect - Associate (SAA-C03). Hope this helps someone!

Table of Content 
1. AWS Fundamentals
2. Identity and Access Management (IAM)
3. Simple Storage Service (S3)
4. Elastic Compute Cloud (EC2)
5. Elastic Block Storage (EBS) and Elastic File System (EFS)
6. Databases
7. Virtual Private Cloud (VPC) Networking
8. Route 53
9. Elastic Load Balancers
10. Monitoring
11. High Availability and Scaling
12. Decoupling Workflows
13. Big Data



# 1. AWS Fundamentals
AWS Global infrastructure contain both regions and availability zones.

Region is a geographical area and each region consists of 2 or more Availability Zones.

Availability Zones - is the location of one data center that are physically separated from other data centers. Each availability zones will have redundant power, networking and connectivity.

<img width="299" alt="image" src="https://user-images.githubusercontent.com/55508777/209054099-30a69338-304e-4ee6-84ce-caadf0a2e682.png">

Edge Locations are endpoints for AWS that are used for cashing content. There are many more edge locations than Regions. Typically, this consists of CloudFront, Amazon's content delivery network.

The Shared Responsibility Model:
<img width="787" alt="image" src="https://user-images.githubusercontent.com/55508777/209054181-d96ac403-98b3-4b63-a4f3-7ecb552bc60e.png">

Encryption is a shared responsibility from AWS and the customer.

- Good was the differentiate the responsibilities are if I can do the task from the AWS Management Console, then it is my responsibility, if not is the AWS responsibility.  

Compute is how information if processed.
- EC2 - virtual machines
- Lambda - serverless function where you don’t have to worry about servers all you have to worry about is your code.
- Elastic Beanstalk - provisioning engine for automated the deployment of applications.

Storage place to store data.
- S3 - aws simple storage solution.
- Elastic Block Store (EBS) - virtual hard disk that is attached to our VM's.
- Elastic File Server - ways of storing files centrally 
- FSx
- Storage Gateway

Databases a spreadsheet in the cloud. It a reliable way to store and retrieve information.
- RDS - Relational Database Services.
- DynamoDB - Non relational database. 
- Redshift - database wear housing technology. 

Networking - A way for our compute, storage and database to communicate and even a place for them to live.
- VPC - virtual data centers in the cloud.
- Direct Connect - a way to connect on prem database to AWS
- Route 53 - a way of doing Domain Name Service (DNS). Registering domain names and pointing them at our web servers.
- API Gateway - serverless way of replacing web servers.
- AWS Global Accelerator - accelerating audiences to application within AWS

AWS Whitepaper READ -> https://docs.aws.amazon.com/wellarchitected/latest/framework/welcome.html

Six Pillars of the Well-Architected Framework:
- Operational Excellence - running and monitoring systems to deliver business values and continually improving processes and procedures.
- Performance Efficiency - making sure that IT sources are getting used efficiently.
- Security - Protecting your information systems.
- Cost Optimization - avoid unnecessary costs.
- Reliability - does not crash from unexpected load.
Sustainability - minimizing the environmental impacts. 

# Identity and Access Management (IAM)
**IAM** - allows you to manage users and their level of access to the AWS console.

Root account is the email address you used to sign up for AWS. The root account has full administrative access to AWS. It is very important to secure this account.

How to secure root account?
- Turn on Multi-factor auth (MFA)
- Create an admin group for your administrators and assign the appropriate permissions to this group.
- Create user accounts for your admins
- Add your users to the admin group

How do we control permissions using IAM? 
- We assign permissions using policy docs, which are made up of JSON.

- IAM happens globally. It is not restricted to a region or zone.

**Users** - a physical person 

**Groups** - functions such as admin, developers. This contains users.

**Roles** - Internal usage within AWS.

- It is best practise for users to inherit permissions from groups.
- One user should always equal one physical person.

The principle of least privilege - only assign a user the minimum amount of privileges they need to do their job.

IAM Federation you can combine your existing user account with AWS. For example, when you log on to your PC (Usually using Microsoft AD), you can use the same credentials to login to AWS if you set up federation. 
- Identity Federation - uses the SAML standard, which his Active Directory.

- Access key Id and secret access keys are not the same as username and password.

Access key ID and Secret Access Keys are used for programmatic access to AWS services.
- Only get to view these once. So don’t lose them.
- Always set a password rotations. You can create and customize your own policies for these.

An deny will always override an allow!

# Simple Storage Service (S3)

S3- is a simple storage service for the cloud. It does object storage.
• You can upload any file type
• You can not run OS or databases from S3
• You get unlimited storage
• Object can be up to 5 TB in size
 
S3 Buckets- store files in buckets (similar to folders)
 
• S3 bucket name needs to be globally unique because the name space in shared globally.
 
Examples S3 URLs:
<img width="440" alt="image" src="https://user-images.githubusercontent.com/55508777/209055379-32551552-013f-46e3-8cdc-50dbfbbe2dea.png">

• When you upload a file to S3 bucket you will receive a HTTP 200 code if successful.
 
Key-Value Store:
• Key - the name of the object (e.g., Chan.jpg)
• Value - The data itself, which is made of a sequence of bytes.
• Version ID - important for storing multiple versions of the same object 
• Metadata - Data about the data you are storing (e.g., content-type, last-modified, etc.)

- S3 is a safe place because data is spread across multiple devices and facilities to ensure availability and durability.

Durability - is your files going to be lost at some point.

Tiered storage - S3 offers a range of storage classes designed for different use cases.

S3 Storage classes:

S3 Standard: Designed for frequent access.
- High availability and Durability.
- Suitable for workload and is the default storage class.
- Use case include websites, content distribution, mobile and gaming applications.

S3 Standard-Infrequent Access (S3 Standard-IA): designed for infrequently accessed data, but requires rapid access when needed.
- You pay to access to data. There is a low per-GB storage price and a per-GB retrieval fee.
- Use cases are great for long-term storage, backups and as a data store for disaster recovery files.

S3 One Zone-Infrequent Access: like S3 Standard-IA, but data is stored only in a single availability zone.
- Costs 20% less than regular S3 Standard-IA
- Great for long-lived, infrequently accessed, non-critical data.

S3 Intelligent-Tiering: automatically moves your data to the most cost-effective tier based on how frequently you access each object. 

3 Glacier Options: you pay each time you access your data. Use only for archiving data. Glacier is cheap storage. Optimized for data that is very infrequently accessed.
- Glacier Instant Retrival - Provides long-term data archiving with instant retrieval time for your data.
- Glacier Flexible Retrieval - Ideal storage class for archive data that does not require immediate access but needs the flexibility to retrieve large sets of data at no cost, such as backup or disaster recovery use cases. Can ne minutes or up to 12 hours.
- Glacier Deep Archive - cheapest storage class and designed for customers that retain data sets for 7-10 years or longer to meet customer needs and regulatory compliance requirements. The standard retrieval time is 12 hours, and the bulk retrieval time is 48 hours.

<img width="803" alt="image" src="https://user-images.githubusercontent.com/55508777/209055488-e4dda60d-d5b7-4f93-a224-8003c106e509.png">

<img width="803" alt="image" src="https://user-images.githubusercontent.com/55508777/209055496-64893eff-5cd6-4354-8010-d229f0567cb3.png">

Lifecycle Management - define rules to automatically transition objects to a cheaper storage tier or delete objects that are no longer required after a set period of time. The maximizing cost effectiveness.

- Lifecycle management can be used with versioning as well to move different versions of object to different storage tiers. This can be applied to current versions and previous versions as well. 

Versioning all versions of an object are stored an can be retrieved, including deleted objects.

Advantages of Versioning:
- Backup can be a great backup tool
- Cannot be disabled once enabled, versioning cannot be disabled - only. Suspended.
- Lifecycle Rules can be integrated with lifecycle rules.
- Supports MFA - can support multi-factor auth. To protect all your S3 data and its version from being deleted, MFA can be used to give the ability to delete objects.  

- Previous versions will not be able to be viewed. Until manually made public. 

Securing Your Data:
- Server-side encryption - you can set default encryption on a bucket to encrypt all new objects when they are stored in the bucket.
- Access Control List (ACLs) - Define which AWS accounts or groups are granted access and the type of access. You can attach S3 ACLs to individual objects within a bucket.
- Bucket Policies - S3 bucket policies specify what actions are allowed or denied (e.g., allow user Alice to PUT but not DELETE objects in the bucket.)  

Types of Encryption:
- Encryption in Transit: this occurs when sending objects to and from our bucket.
○ SSL/TLS
○ HTTPS
- Encryption at REST: Server-side encryption: this occur when the object is in S3.
○ SSE-S3: S3-managed keys, using AES 256-bit encryption
○ SSE-KMS: AWS Key Management Service-managed keys
○ SSE-C: Customer-provided keys
- Encryption at REST: Client-Side Encryption
○ You encrypt the files yourself before you upload them to S3

Enforcing Server-Side Encryption: 
- Console select the encryption setting on your S3 bucket. The easiest way is just a checkbox in the console.
- Bucket Policy you can also enforce encryption using a bucket policy. 
○ You can create bucket policies that deny any S3 put requests that does not include any encrypted objects.
§ A bucket policy can deny all PUT requests that don’t include the x-amz-server-side-encryption parameter in the request header.

Strong Read-After-Write Consistency:
- After a successful write of a new object or an overwrite of an existing object, any subsequent read requests immediately receives the latest version of the object.
- Strong consistency for list operations, so after a write, you can immediately perform a listing of the objects in a bucket with all changes reflected. 

Object ACLs work on an individual object level

Bucket Policy work on an entire bucket level.

- S3 operates globally.
○ Bucket can be put to a AWS region, but the namespace is global.

- Buckets are private by default: when you create an S3 bucket, it is private by default (including all objects within it.) You have to allow public access on both the bucket and its objects in order to make the bucket public.

- Objects ACLS, you can make individual objects public using object ACLs.
- Bucket policies, you can make entire buckets public using bucket policies.

- ARN is a unique ID for an AWS resource such as S3 or EC2

- Static website -> S3
○ No dynamic content

- S3 scale automatically with demand.

S3 Object Locks

S3 Object Lock: to store using the write once, read many (WORM) model. It can help prevent objects from being deleted or modified for a fixed amount of time or indefinitely to meet regulatory standards. 

- Object lock can be individual objects or applied across the bucket as a whole. 

Governance mode, users cant overwrite or delete an object version or alter its lock settings unless they have special permissions. With this mode you protect objects against being deleted by most users, but you can still grant come users permission to alter the retention settings or delete the object if necessary.

Compliance Mode: a protected object version cant be overwritten or deleted by any user, including the root user. When objects is locked incompliance mode, its retention mode cant be changed and its retention period cant be shortened. Compliance mode ensures an object version cant be overwritten or deleted for the duration of the retention period. 

Retention Periods protects an object version for a fixed amount of time.
- Wen you place a retention period on an object version, AWS S3 stores a timestamp in the object metadata to indicate when the retention period expires.
-  After the retention period expires, the object version can be overwritten or deleted unless you also placed a legal hold on the object version.

Legal Hold: like a retention period, a legal hold prevents an object version from being overwritten or deleted. However legal hold does not have an associated retention period and remains in effect until removed. 
- Legal holds can be freely placed and removed by any user who has s3:PutObjectLegalHold permissions.

Glacier Vault Lock: allows you to easily deploy and enforce compliance controls for individual S3 Glacier vaults with a vault lock policy. You can specify control, such as WORM, in a vault lock policy and lock the policy from future edits. Once locked, the policy can no longer be changed.

Optimizing S3 Performance: 

S3 Prefixes - is the folders inside our S3 buckets. Does not include the object name or file type as follows: 

<img width="716" alt="image" src="https://user-images.githubusercontent.com/55508777/209055842-137d0399-b41d-4e81-86dc-946e4346d654.png">

- The more prefixes you have the better the performance will be for S3 for your application. 

Limitation - the SSE-KMS encrypt takes time when you upload a file, you will call GenerateDataKey in the KMS API. When you downloads a file, you will call Decrypt in the KMS API.
- The limits are region specific. 

Multipart Uploads: parallelize uploads (increases efficiency). Recommended for files over 100MB and required for files over 5 GB 

<img width="468" alt="image" src="https://user-images.githubusercontent.com/55508777/209055903-59d2d89a-4fb5-42cc-9113-9e40f03dfa99.png">

S3 Byte-Range Fetches: parallelize downloads by specifying byte ranges. If there's a failure in the download, its only for a specific byte range.

<img width="555" alt="image" src="https://user-images.githubusercontent.com/55508777/209055966-24bd7649-1957-45d1-a704-b88ddb881b32.png">

Backing up Data with S3 Replication:

S3 Replication is replicating objects from one bucket to another. Versioning must be enabled on both the source and destination buckets 
- Objects in an existing bucket are not replicated automatically. Once replication is turned on, all subsequent updated objects will be replicated automatically.
- Delete marks  are not replicated by default. Deleting individual versions or delete marker will not be replicated.

Cross region replication = S3 Replication 

#Elastic Compute Cloud (EC2)

EC2 - secure, resizable compute capacity in the cloud. Is a VM hosted in the cloud.
- Only  pay for what you use.

Pricing Options:
- On-demand - Pay by the hour or the second depending on the type of instance you run.
○ Flexible - low cost and flexibility of EC@ without any upfront payment or long-term commitment
○ Short-Term - Applications with short-term, spiky or unpredictable workloads that cannot be interrupted.
○ Testing the waters- Application being developed or tested for the first time on EC2
- Reserved capacity for 1 or 3 years. Up to 72% discount on the hourly charge.
○ Predictable Usage - application with stead state or predictable usage.
○ Specific Capacity Requirements - Application that require reserved capacity. 
○ Pay up front - you can make upfront payments to reduce the total computing costs even further.
○ Standard RIs - up to 72% off the on-demand price.
○ Convertible RIs - Up to 54% off the on-demand price. Has the option to change to a different RI type of equal or greater value. 
○ Scheduled RIs - Lunch within the time window you define. Match your capacity reservation to a predictable recurring schedule that only requires a fraction of a day, week or month 
○ Reserved instance operates at a regional level. i.e. when you reserve an instance from Canada Central, it can only be reserved in Canada. 
- Spot purchase unused capacity at a discount of up to 90%. Prices fluctuate with supply and demand.
○ Applications that have flexible start and end time.
○ Application that are only feasible at very low compute prices
- Dedicated a physical EC2 server dedicated for your use. The most expensive option. 
○ Compliance - regulatory requirements that may not support multi-tenant virtualization. i.e. other companies cannot use the same AWS servers or hardware.
○ Licensing - great for licensing that does not support multi-tenant or cloud deployment.
○ On-demand - can be purchased on-demand
○ Reserved - can ne purchases as a reservation for up to 70% off the on-demand price.
○ Any question that talks about special licensing requirements choose Dedicated Host
		

AWS Pricing Calculator - can be used to calculate the cost of  AWS services.

AWS Command Line: command line interface to work with AWS resources 
- Secret Access Key -  you will only see this once! If you lose it, you can delete the access key ID and secret access key and regenerate them. You will need to run "aws configure" command again.
- Don’t Share Key Pairs - Each develop should have their own access key ID and secret access key. Just like passwords, they should not be shared. 
- Supports Linux, Windows and MacOS

- Create IAM groups and assign your users to groups. Group permissions are assigned using IAM policy documents.

IAM Role - is an identity you can create in IAM that has specific permissions. A role is similar to a user, as it is an AWS identity with permission policies that determine what the identity can and cannot di in AWS.
- How it differs from a User is that instead of being uniquely associated with one person, a role is intended to be assumable by anyone who needs it.
- Roles are temporary

- Roles are the preferred option from a security perspective.

- Avoid hard-coding your credentials - Roles allow you to provide access without the use of access key IDs and secret keys.

- Policies control a role's permissions

- You can update a policy attached to a role and it will take immediate effect.

- Attaching and detaching you can attach and detach roles to running EC2 instances without having to stop or terminate those instances.

- For exam always use roles over hard coding. For example, using roles are better to use that access key ID or secret access keys. 

Security Groups & Bootstrap Scripts:

How computers Communicate:
- Linux - SSH - Port 22
- Windows - RDP - Port 3389
- HTTP - Web Browsing - Port 80
- HTTPS - encrypted web browsing (SSL) - 443

Security Groups are groups of virtual firewalls for your EC2 instance. By default, everything is blocked including SSH and RDP.

- In order to be able to communicate to your EC2 instance via SSH/RDP/HTTP, you will need to open up the correct ports.

- Changes to security groups take effect immediately

- You can have any number of EC2 instances within a security group.

- You can have multiple security groups attached to EC@ instance.

- All outbound traffic is allowed.

Bootstrap Scripts run when the instance first runs. It is passes user data to the EC2 instance and can be used to install applications.
- Automated the installation of the applications.

#! /bin/bash- shebang and path to interrupter

EC2 Metadata and User Data:

EC2 Metadata is data about your EC2 instance. Including private IP address, public IP address, hostname, security groups, etc.
- Metadata can be retrieved using command line.

User data - is simply bootstrap scripts

- You can use bootstrap script to access metadata 


Networking with EC2:

3 different types of virtual network cards:
- Elastic Network Interface (ENI) - for basic, day-to-day networking.
○ Allows Private IPv4 Addresses, Public IPv4 Address, Many IPv6 Addresses, MAC Address and 1 or more Security Groups.
○ Create a management network.
○ Use network and security appliances in your VPC.
○ Create dual-homed instances with workloads/roles on distinct subnets
○ Create a low-budget, high-availability solution 
- Enhanced Networking (EN) - uses single root I/O virtualization Single Root- IOV (SR-IOV) to provide high performance.
○ For high-performance networking between 10Gbps-100Gbps.
○ Single Root I/O Virtualization (SR-IOV) provides higher I/O performance and lower CPU utilization.
○ Performance: provides higher bandwidth, higher packet per second (PPS) performance and consistently lower inter-instance latencies.
○ Two instance types:
§ Elastic Network Adapter (ENA) - Supports network speeds of up to 100 Gbps for supported instance types. In exam when told to choose between the two instances always choose ENA
§ Intel 82599 Virtual Function (VF) Interface supports network speeds of up to 10 Gbps for supported instance types. Typically used on older instances. 
- Elastic Fabric Adapter (EFA) - accelerates high performance computing (HPC) and machine learning applications.
○ Provides lower and more consistent latency and higher throughput than the TCP transport traditionally used in cloud-based HPC systems.
○ EFA can use OS-Bypass which enables HPC and machine learning applications to bypass the operating system kernel and communicate directly with the EFA device. Currently only supported for Linux. Makes systems a lot faster with much lower latency.


Optimizing with EC2 Placement Groups:

3 Types of Placement Groups: 
- Cluster Placement Groups grouping of instances within a single Availability Zone. Recommended for applications that need low network latency, high network throughput, or both.
○ Best to EC2 instance that need high performance and low latency and high network throughput.
- Spread Placement Groups is a group of instances that are each placed on distinct underlying hardware.
○ These are recommended for applications that have a small number of critical instances that should be kept separate from each other. 
- Partition Placement Groups Each partition placement group has its own set of racks. Each rack has its own network and power source. No two partitions within a placement group share the same racks, allowing you to isolate the impact of hardware failure within you application. 
○ For multiple EC2 instance that need to be in there own rack and dedicated network infrastructure.

- Cluster placement group can nor spam multiple AZ while spread placement groups and partition placement groups can. 
		

Timing Workloads with Spot Instances and Spot Fleets:

- You would use a Spot Instance for stateless, fault-tolerant, or flexible applications.

- You can step a max spot price you are willing to pay and your EC2 will be initialized if the spot price is less than your max price. If the spot price is more than your max price the EC2 instance will get terminated or stopped and you will have 2 minute to decide the option.

Spot blocks are used to stop your Spot instances from being terminated even if the Spot price goes over your max Spot price. You can set Spot blocks between 1-6 hour currently

- Spot instance are useful in high performance computing and this will come up in the exam.

Terminating Spot Instances:

Two Request Type:
- One-time: a spot request it made once and if the spot price goes higher than the max price then the one-time instance is terminated or stopped.
- Persistent: its looking to see if the request is open, active or disabled. You also need to say when the request is valid from and valid to.
○ Important: if you have a spot request that is persistent you cannot just delete the instances, you will need to cancel the spot request then the instance because the spot request will automatically loop creating new instances.

