# AWS Practitioner Notes

## Six Advantages Of Cloud Computing

1. Trade Capital Expense for variable expense
Instead of investing heavily in data centers and servers before you use them you can pay for how much you are gonna use. 

2. Benefit from massive economies of scale
you will never have the same purchasing power as Amazon.

3. Stop guessing about capacity
don't buy too much or too little.

4. Increase speed and agility
A cloud Guru platform was built in 3 weeks, using a new type of design called serverless architecture. It scales infinitely with demand. 

5. Stop spending money running and maintaining data centers

6. Go global in minutes

## Infrastructure As A Service

You manage the server which can be physical or virtual. As well as operating system, usually the data center provider will have no access to your server

## Platform As A Service

Someone else manages the underlying hardware and operating systems. You focus on applications, someone else worries about security patching, updates, maintenance etc.

## Software As A Service

Think of Gmail. All you do is manage your inbox and google handles everything else.

## Cloud Computing Deployment Types

- Public Cloud
- AWS, Azure, GCP
- Hybrid
- Mixture of public and private
- Private Cloud (On Premise)
- you host and manage it in your datacenters

### AWS - High Level Services Of Note*

- AWS Global Infrastructure
- AWS Cost Management
- Compute
- Databases
- Migration & Transfer
- Network & Content Delivery
- Security, Identity, & Compliance
- Storage

## Zones and Regions

- Availability zone is datacenter
( one or more discrete data center each with redundant power networking and connectivity housed in separate facilities)

- Region is geographical area consisting of 2 or more availability zones
(is a physical location in the world which consists of two or more AZs)

- Edge locations are endpoints for AWS which are used for caching content. Typically this consists of CloudFront, Amazon's Content Delivery Network (CDN)

- GovClouds are operated by US citizens on US soil. Only government and private businesses that pass screening checks can use it.

### Choosing the right AWS region

1. Data Sovereignty Laws
2. Latency to end users
3. AWS Services (US east-1 primary Region for releases)

## Support Plans

### Basic

- Free access to forums

### Developer

experimenting with AWS. One primary contact to ask technical questions through Support Center and get response within 12-24 hours during local business hours 29/month

### Business

Production use of AWS - 24x7 support by phone and chat. 1-hour response time to urgent support cases and help with common third party software. Full access to AWS Trusted
advisor for optimizing your AWS infrastructure and access to AWS Support API for automating your support cases 100/month

### Enterprise

Use Case: Mission-critical use of AWS
Technical Account Manager (TAM) 15 minute response time.
15k month

## What is S3

### Simple Service Storage (S3)

- one of the oldest services
- Provides developers and IT teams with secure, durable, highly-scalable object storage. Amazon S3 is easy to use, with a simple web services interface to store and retrieve

- S3 is safe place to store files
- Object-based storage
- Block based storage would be for operating systems (NOT s3)

- Files can be from 0bytes to 5 TB

- Unlimited storage
- Files are stored in Buckets (Folders in cloud)

- S3 is a universal Namespace so name must be unique GLOBALLY
- will always be prefixed with https://s3-region...

- Objects are files that consist of:
- Key (simply the name of the object)
- Value (Data that made up of sequence of Bytes)
- Version ID
- Metadata
- Subresources
  - Access Control Lists
  - Torrent

#### S3 NEED TO KNOW Exam Tips

- How does consistency work for S3 
  - Read after Write consistency for PUTS of new Objects
  - Eventual Consistency for overwrite PUTS and DELETES (can take some time to propagate)

- If writing file, put a file into S3 you can immediately read that data.

- If you update existing file or delete file you may get an older version. Basically changes can take some time to propagate to S3

- S3 has following guarantees
- 99.99% availability for S3 platform But amazon only Gurantees 99.9% availability
- AMAZON does guarantee 99.999999999% durability (the 11 9's) So very unlikely to lose File
- To Calculate: Number of seconds in any given months and multiply it by 99.99%

##### S3 has the following features

- Tiered Storage Available
- Lifecycle Management
- Versioning 
- Encryption
- Secure your data using Access Control Lists and Bucket Policies

### S3 Storage Classes

- S3 - Standard (11 9's )
- S3 - IA (RAPID access)
- S3 - One Zone - IA
- S3 - Intelligent Tiering (using machine learning to determine what you need)
- S3 - Glacier (secure, durable low cost data archiving)
- S3 - Glacier Deep Archive (takes 12 hours to retrieve SUPER cheap)

### What are you charged for with S3?

- Storage
- Requests
- Storage Management pricing
- Data Transfer pricing
- Transfer Acceleration
- Cross Region Replication Pricing

### S3 Transfer Acceleration 

enables fast and secure transfers of files over long distances between your end users and s3 buckets.
(Users upload to edge sites then use Amazon intranet to upload)

### Restricting ACCESS in S3

1. Use Bucket Policies - Applies across the whole bucket
2. Object Policies - Applies to individual files
3. IAM Policies to Users and Groups - applies to users and groups

Static Websites can be hosted in S3 Buckets
Dynamic Websites CANNOT be hosted in S3 Buckets
S3 buckets scale dynamically

## What is CloudFront

A content delivery network (CDN)

works in 3 parts:

- Edge Location
- Origin
- Distribution (name given to CDN which consists of a collection of edge locations)

First users asks for content from edge location then the edge location will go get file and server to user. Then any additional users get files from edge locations

### Types of distributions

Web Distribution - Typically for Websites
RTMP - Used for media streaming (CloudFront is discontinuing support for RTMP distributions on December 31, 2020. For more information, please read the announcement.)

## EC2 Elastic Compute Cloud

Oldest services
Virtual server or servers in cloud.
Web service that provides resizable compute capacity in the cloud. Amazon EC2 reduces the time required to obtain and boot new server instances to minutes
allowing you to quickly scale capacity both up and down as your needs change

### EC2 Pricing Models

1. On Demand (allows you to pay a fixed rate by the hour (or second) with no commitment)
2. Reserved  (Provides you with a capacity reservation and offers a significant discount on the hourly charge for an instance. Contract terms are 1 or 3 years)
3. Spot      ( Enables you to bid a price you want to pay for instance capacity)
		NOTE: if amazon EC2 terminates spot instance because of pricing change during your hour of use you will NOT be charged however if you terminate the instance early 
			you are charged for any hour which the instance ran.
4. Dedicated Hosts (Physical EC2 server dedicated for your use.)

#### Silly Acronym To Remember EC2 Types : FIGHT DR MCPXZ

F - For FPGA
I - FOR IOPS
G - Graphics
H - High Disk Throughput
T - Cheap general purpose
D - For Density
R - For RAM
M - Main choice for general purpose apps
C - For Compute
P - Graphics
X - Extreme Memory
Z - Extreme memory and CPU

## What is EBS

Virtual Disk in The Cloud.

Types:

- SSD
- General Purpose SSD (GP2) - balances price and performance for a wide variety of workloads
- Provisoned IOPS SSD (I01) - Highest performance SSD volume for mission-critical low-latency or high-throughput workloads
- THERE IS ALSO A (IO2)
- Magnetic
- Throughput Optimiazed HDD (ST1) - Low cost HDD volume designed for frequently accessed throughput-intense workloads.
- Cold HDD (SC1) - Lowest Cost HDD volume designed for less frequently accessed workloads
- Magnetic - Previous Generation

## Load Balancers

### Application Load Balancers

Layer 7 aware (Meaning they can make intelligent decisions)

### Network Load Balancers

Extreme Performance/Static IP Addresses

### Classic Load Balancers

Test & Dev, Keep Costs Low

## Databases

- Relational Databases on AWS - RDS:
- SQL Server
- Oracle
- MySQL Server
- PostgreSQL
- Aurora (amazon’s own)
- MariaDB

Can have multiple availability zones.
Can have Read Replicas for enhanced Performance

Multiple AZ’s are for disaster recovery
Read Replicas are to increase performance

### NON-Relational Database on AWS

Columns in table can vary
Previous columns will not affect other rows in the database
Amazons NON-Relational Database is called DynamoDB

#### Online Transaction Processing (OLTP)

- Pulls up a row of data such as Name, Date, Address to deliver to, etc.
- Basically takes/inserts a row from database

#### Online Analytics Processing (OLAP)

- Pulls huge number of records
- Massive performance needed
- Data warehouse created to solve this.

### Data-warehouse

Use different architecture
Designed to handle large scale calculations of data away from the database so that database performance is not affected.
AMAZON'S Redshift

### ElastiCache

- Web service that makes it easy to deploy, operate and scale an in-memory cache in the cloud.
- Improve performance of web application
- Caches most common queries to return data to users.
- Takes massive load off database queires
- Comes in Memcached and Redis

## Route 53

Amazon’s DNS service
It is Global like IAM and S3
Can direct traffic all over the world
Can Register Domain Name

## Elastic BeanStalk

Deploy Applications to cloud
Need no knowledge on AWS just upload code
FREE service (however resources provisioned are not)

## CloudFormation

Its a service that allows you to model and setup AWS resources.
Focus more on the application and not managing the resources
Create templates to describe needed resources
FREE service (however resources provisioned are not)

## Lightsail
Platform As A Service

### POPULAR EXAM QUESTIONS

- Name All the Compute Services:
  - EC2
  - Elastic BeanStalk
  - Lambda
  - Lightsail
  - Batch
  - EC2 Image Builder
  - AWS Outpost
  - Serverless application Repository

- Traditional Computing vs Cloud Computing
- IT assets as Provisioned Resources
- Global, Available, and Scalable Capacity
- Higher level Managed Services
- Built in security
- Architecting For Cost
- Operations on AWS

### Graph database

Amazon Neptune is Amazon’s graph database

## Global Services

- IAM
- Route 53
- CloudFront
- SNS
- SES
- Give Global view BUT are regional
- S3
- AWS Services used on Premise
- Snowball (Typically 80 TB in size AWS ships to you and you ship back to move data)
- Snowball Edge (Similar however has CPU and can deploy lambda on premise)
- Storage Gateway (Stays on premise, allows caching files inside datacenter that replicates to S3)
- CodeDeploy (deploy applications on EC2 on premise)
- Opsworks (similar to elastic beanstalk. Used to deploy)
- IoT Greengrass (connects devices to AWS cloud)

## Cloudwatch

- Monitor services for AWS resources and applications on AWS.
- Compute
- EC2 Instances 
- Autoscaling Groups
- Elastic Load Balancers
- Route 53 Health checks
- Storage and content deliver
- EBS Volume
- Storage gateway
- Collectd type metrics
- Monitors every 5 mins by default
- Can trigger notifications
- Can change intervals for checks.
- AWS Systems Manager
- Monitor EC2 instances at scale, or allows you to monitor EC2 Fleet (many EC2s) Installs piece of software on each VM
- Use system manager to run command across ALL EC2 instances
- Also works on for on premise machines
- Integrates with cloudwatch to give dashboard for everything

## CAPEX vs. OPEX

Capex:

- Stands for Capital expenditure which is where you pay upfront and it is a fixed sunk in cost.

Opex
- Operational Expenditure which is where you pay for what you use.
- Think about it like utilities (gas, electric)

## Pricing Policies

- Pay as you go
- Pay less when you reserve
- Pay even less per unit when using more
- Pay even less as AWS gross
- Custom pricing

## Fundamental Drivers Of Cost With AWS

- Compute
- Storage
- Data outbound

## AWS FREE Services

- Amazon VPC
- Elastic Beanstalk
- Cloud Formation
- Identity Access Management (IAM)
- Auto Scaling
- Opsworks
- Consolidated Biling

## EC2 Pricing

- Clock Hours of Server Time
- Instance Type
- Pricing Model
- Number of Instances
- Load Balancing
- Detailed Monitoring
- Auto Scaling
- Elastic IP Addresses
- Operating Systems and Software Packages
- Pricing Models
- On Demand
- Reserved
- Spot
- Dedicated Hosts
- Lambda Pricing
- Request Pricing
- Free Tier: 1 million requests per month
- $0.20 per 1 mil
- AWS Budgets:
- Gives ability to set custom budgets that alert you when your costs or usage exceed (or are forecasted to exceed your budgeted amount) 
- Used to budget costs before they are incurred

## AWS Cost Explorer
Explore costs that have been incurred over time.


## Tags

- Key:Value pairs
- Metadata
- Tags can be inherited
- Specific Information
- Resource Groups objects that share one or more tags
- AWS Organizations & Consolidated Billing
- AWSO an account management service, consolidates AWS
- Consolidated Billing

## AWS WAF & AWS Shield

- WAF protections from common exploits (Hackers)
- Shield protects from DDos, two tiers (DDos)
- Standard - Free, comes with all deployments
- Advanced - adds reporting, support for DDoS attacks, and cost protection
- Amazon Inspector
- Automatically assesses application for security vulnerabilities or deviations from best practice.
- Trusted Advisor
- Provides real time guidance on provisioning resources according to AWS best practices.
- Advices on Optimization, Performance, Security, Fault Tolerance
- Core Check and Recommendations - Free
- Full Trusted Advisor - Business and Enterprise Only
- Athena, serverless query service
- Query logs
- Business reports
- AWS cost and usage reports
- Queries on click-stream data
- Macie uses AI protects PII, security service

