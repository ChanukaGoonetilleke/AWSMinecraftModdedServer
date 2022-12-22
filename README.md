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
 13. Big Data!



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


