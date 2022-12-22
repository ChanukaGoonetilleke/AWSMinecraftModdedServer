# AWS Solution Architect Certification Notes

These are my note I took from take the A Cloud Guru AWS Certified Solutions Architect - Associate (SAA-C03)

Table of Content 
1. AWS Fundamentals
2. Identity and Access Management (IAM)
3. Simple Storage Service (S3)
4. Elastic Compute Cloud (EC2)
5. Elastic Block Storage (EBS) and Elastic File System (EFS)
6. Databases
7. Virtual Private Cloud (VPC) Networking
8. Route 53


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
