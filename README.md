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
