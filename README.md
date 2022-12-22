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
IAM - allows you to manage users and their level of access to the AWS console.

Root account is the email address you used to sign up for AWS. The root account has full administrative access to AWS. It is very important to secure this account.

How to secure root account?
- Turn on Multi-factor auth (MFA)
- Create an admin group for your administrators and assign the appropriate permissions to this group.
- Create user accounts for your admins
- Add your users to the admin group

How do we control permissions using IAM? 
- We assign permissions using policy docs, which are made up of JSON.

- IAM happens globally. It is not restricted to a region or zone.

Users - a physical person 

Groups - functions such as admin, developers. This contains users.

Roles - Internal usage within AWS.

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
