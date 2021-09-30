# AWS Associate Developer Notes

## IAM

- IAM allows you to manager users and their level of access to the AWS Console
- Centralized control of your AWS account
- Shared Access to your AWS account
- Granular Permissions
- Identity Federation
- Multi Factor Authentication
- Provide temporary access for users/devices and services, as necessary
- Allows you to set up your own password rotation policy
- Integrates with many AWS services.
- Supports PCI DSS Compliance
- Critical Terms:
  - Users: End Users (Think People)
  - Groups: Collection of users under one set of permissions
  - Roles: Create roles and then assign them to AWS resources
  - Policies: A document that defines one (or more) permissions.

## EC2

- Elastic Compute Cloud (EC2)
- Secure, resizable compute capacity in the Cloud
- Basically VM hosted in AWS
- Designed to make web scale cloud computing easier
- Capacity when you need it and complete control
- History:
  - Game Changer when it was introduced.
  - Pay only what you use
  - No Wasted Capacity (Grow and Shrink when needed)
  - Prior to EC2 (Capacity Estimates, Long term investment, 3-5 years)
- Servers Running in Minutes NOT Months.
- Pricing Models:
  - On Demand (Pay For Time Running)
    - Flexible
    - Short-Term
    - Testing The Water.
  - Reserved Instances (Reserve capacity for 1-3 years BIG discount. Up to 72%)
    - Predictable Usage (steady state)
    - Specific Capacity Requirements
    - Pay Up-Front
    - Standard RIs (Claim 72% off)
      - Cannot Change Instance Size Later
    - Convertible RIs
      - Up to 54% off.
      - Option to convert to other instance type of equal or greater value
    - Scheduled RIs
      - Launch within time window you define
        - Match capacity reservation time frame
        - Use RIs during your busy time
  - Spot (Purchase unused capacity at discount of 90% Prices. Process can be interrupted)
    - Applications that have flexible start and end times
    - Applications that are feasible at very low compute prices
    - Users with an urgent need for large amounts of additional computing capacity
  - Dedicated (Physical EC2 server dedicated for your use. Good for software license restriction. Also most expensive)
    - Application with Compliance requirement that does not support multi-tenant virtualization
    - Purchase Plans:
      - On-Demand
      - Reserved
  - Saving Plans:
    - Save up to 72% when paying for All AWS Compute usage, regardless of instance type or Region
    - Commit To One or Three Years
    - Super Flexible (Not only for EC2)
- EC2 Instance Types:
  - Stats of Instance Type
    - Hardware
    - Capabilities
      - CPU
      - Memory
      - Storage
  - Instance Types are optimized to fit different use cases
  - Acryonym To Remember Types FIGHT DR MCPXZ
    - **F** - For FPGA
    - **I** - FOR IOPS
    - **G** - Graphics
    - **H** - High Disk Throughput
    - **T** - Cheap general purpose
    - **D** - For Density
    - **R** - For RAM
    - **M** - Main choice for general purpose apps
    - **C** - For Compute
    - **P** - Graphics
    - **X** - Extreme Memory
    - **Z** - Extreme memory and CPU

## EBS Volumes

- Elastic Block Store
- Storage volumes that can be attached to EC2 instances
- Can be used to:
  - Create file system
  - Run a database
  - Run Operating System
  - Store Data
  - Install Applications
- Designed for mission critical Production Workloads
- Automatically replicated within single AZ to protect against failure (this is automatic)
- Scalable (Dynamically increase capacity and change the type with 0 downtime)
- TYPES:
  - I/O operations Per Second (IOPS)
  - SDD:
    - General Purpose SSD (gp2)
      - 3 IOPS per GiB up to 13,000 IOPS per volume
        - Good for boot volumes and test applications
    - Provisioned IOPS SSD (io1)
      - High performance option and expensive
      - Up to 64,000 IOPS per volume 50 IOPS per GiB
      - Use if you need more than 16,000 IOPS
      - Designed for I/O intensive applications
    - Provisioned IOPS SSD (io2)
      - Latest generation
      - Higher Durability and more IOPS per GiB
      - SAME max IOPS
      - Same price as io2
      - 500 IOPS per GiB
      - 99.999% durability
  - HDD:
    - Throughput Optimized HDD (st1) CANNOT BE BOOT
      - Low-cost HDD volume
      - Store LOADS of data
      - Throughput of 40 MB/s per TB
      - Ability to burst 250 BM/s per TB
      - Max throughput of 500 MB/s per volume
      - Big Data, Data warehouses, ETL, and log processing
    - Cold HDD (SC1)
      - Lowest Cost Option

- EBS volume types
        <https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-volume-types.html>
- EBS instances created from snapshots will maintain encryption status
  - Encrypted - > Encrypted
  - Un-encrypted -> Un-encrypted

### IOPS

- Measures number of read and write operations per seconds
  - Important metric for quick transactions, low latency apps, transaction workloads
  - The ability to action reads and writes very quick
- Throughput
  - Measures number of bits read or written per seconds
  - Important metric for large datasets, large I/O sizes, complex queries
  - All about ability to deal with large datasets.

## Elastic Load Balancers

- Balances loads between multiple web servers
- Types:
  - Application Load Balancer
    - Application layer 7 OSI
    - â€œSmart Decisionsâ€
    - Can see what request is doing to determine what needs done with request
    - Can create advanced request routing
    - Best suited for load balancing of HTTP and HTTPS
  - Network Load Balancer
    - Layer 4
    - Super Fast performance
    - Best suited for TCP traffic
    - Capable of handling millions of requests per seconds
    - Use for extreme performance
    - Most expensive
  - Classic Load Balancer
    - Not Recommended
    - Legacy Purposes
    - Tested on exam alot
    - Meant for Legacy HTTP/HTTPS
    - Sticky Sessions and X-Forwarded
    - Can do layer 7 or layer 4
    - Load Balancer Errors:
      - Error 504 Gateway has timed out if your application stops with 504 that means the application is having issues. This could be either at Web Server layer or at Database Layer.
  - X-Forwarded-For Header:
    - User (123.45.6.789) -> Load balancer (10.0.0.23) -> EC2 (10.0.0.23)
      - The user sends a request to load balancer, load balancer does not use the user's public IP it hits the private IP for EC2 and the EC2 sees the private IP. If we want to know the IP the request came from we need to look in the header for the â€œX-Forwarded-Forâ€

## Route53

- Amazonâ€™s DNS service
- Allows you to map domain names to
  - EC2 instances
  - Load Balancers
  - S3 Buckets
- Naked domain is the domain excluding â€˜wwwâ€™
- A and AAAA are only for the naked domain name

## Roles

- Roles allow access to resources without ACCESS keys
- Roles are preferred from a security perspective
- Roles are controlled by policies
- You can change a policy on a role and it will take immediate effect
- You can attach and detach roles to running EC2 instances without having to stop or terminate these instances

## RDS (OLTP)

- Relational databases are a compilation of tables that have rows and columns
- Relational Database Types:
  - SQL Server
  - Oracle
  - MySQL Server
  - PostgreSQL
  - Aurora (Amazonâ€™s proprietary RDS)
  - MariaDB
- Non Relational Database:
  - Database with:
    - Collection = Table
    - Document = Row
    - Key Value pairs = Fields
  - Data does not need to be predefined
- Data warehousing
  - Used for business intelligence
    - Cognos
    - Jaspersoft
    - SQL Server
    - Oracle Hyperion
  - Used for data queries that are very heavy and should be done separate from production database
- Online Transaction Processing OLTP
  - Simple transactions (happen frequently)
    - Insert into table

## Redshift

- Online Analytics Processing OLAP (happens occasionally)
  - More complex analysis
    - Sum of radios sold in EMEA and profit from each

## ElastiCache

- Web service that makes it easy to deploy operate and scale in memory cache in cloud
  - Take load off database by using cache memory
  - Supports two open-source in-memory engines:
    - Memcached
    - Redis
Aurora is not available on Free Tier
RDS does not give public IPv4 only a DNS record

## Multi-AZ & Read Replicas

- Backups
  - Automated backups:
    - Will allow you ro recover your database to any point in a time within a â€œretention periodâ€
    - Automated Backups will take a full daily snapshot and will also store transaction logs throughout the day
    - When you do a recovery AWS will choose the most recent daily back up and then apply transaction logs relevant to that day
    - This allows for a point in time recovery down to a second within the retention period
    - Retention periods are between 1 - 35 days
    - Enabled by default
    - Backup data stored in S3
    - You get free storage space equal to the size of your database
    - Backups are taken within a defined window and during that time the I/O may experience latency
    - Will be deleted if original DB deleted
  - Snapshots
    - Snapshots are done manually (user initiated)
    - Will always be stored after deletion of original instance
    - When restoring from snapshot the restored version will be a completely separate database with its own endpoint
- Encryption
  - Uses the AWS Key Management Service (KMS)
  - Once RDS is encrypted the data stored at rest in underlying storage is encrypted as are its automated backups and read replicas and snapshots
  - Currently encrypting an existing DB instance is not supported, you would need to create snapshot make a copy of snapshot and encrypt the copy
- Read Replicas (Used For Performance)
  - Done Asynchronously
  - Create Read ONLY copy of production database
  - Can have 5 read replicas per database by default
  - Scale out DB to spread load across read replicas
  - Can have read replicas of read replicas
  - MUST have automatic backups turned on in order to deploy a read replica
  - Read replicas can be promoted to be their own databases This breaks replication
  - Read replicas can be in different AZ or regions
    - Available for:
      - MySQL Server
        - PostgreSQL
        - MariaDB
        - Aurora
    - NOT Available for:
      - SQL Server
      - Oracle
- Multi-AZ (Disaster Recovery ONLY)
  - Done Synchronously
  - RDS makes copy of all transaction to a copy of the Database in another AZ
  - Designed for Disaster recovery
  - AWS handles replication for us
  - DNS will change if a database disaster is detected.
  - Available for:
    - SQL Server
    - Oracle
    - MySQL Server
    - PostgreSQL
    - MariaDB
    - Aurora (Done by default)

## Elasticache

- Web service that makes it easy to deploy, operate and scale an in-memory cache in the cloud
- Faster than using the disk speeds
- Significantly support latency for read heavy workloads
- Improves performance by storing critical pieces of data in memory for low latency access
- Types:
  - Memcached
    - Widely adopted memory object caching system
    - Elasticache protocol compliant with Memcached
    - Use when not concerned with redundancy
  - Redis
    - Popular open-source in-memory key-value store that supports data structures such as sorted sets and lists
    - Elasticache supports Master / Slave replication and Multi-AZ which can be used to achieve cross AZ redundancy
    - Use when you want AZ redundancy
  - Differences:
    - Elasticache manages Redis more like a relational database because of replication and persistence features of Redis
    - Redis ElastiCache clusters are managed as stateful entities that include failover.
    - Memcached is designed as pure caching solution with no persistence similar to auto scaling with EC2
    - Nodes with Memcached are expendable and autoraplacable.
  - Use Cases:
    - Object Caching is primary goal (Memcached)
    - Need simple caching modell (Memcached)
    - Running large cache nodes and require multithreaded performance with multi cores (Memcached)
    - Need to scale cache horizontally with growth (Memcached)
    - More advanced data types (Redis)
    - Sorting and ranking datasets in memory (Redis)
    - Persistence of key store information (Redis)
    - Run in multi-AZ with failover (Redis)

## S3

- Simple Storage Service (S3)
  - Give devs and IT team secure, durable, scalable object storage
    - Not for OS and database
    - Data spread across multiple devices and facilities so these are HA
  - Object based
    - Objects can be 0 Bytest to 5 TB
  - Larges size file that can transfer to S3 using PUT is 5 GB
  - Unlimited Storage
  - Files are stored in Buckets (similar to folder)
  - S3 is a universal namespace (means they are a global service)
  - When upload is successful you recieve a HTTP 200 status code
- Data consitency
  - Read after Write consistency for PUTS of new Objects
    - Means that as soon as file is uploaded it is available to read
  - Eventual Consistency for overwrite PUTS and DELETES
    - Means can take some time for changes to propegate
- S3 Under Hood
  - S3 is object based and objects conists of the following
    - Key (This is the name of an object)
    - Value (This is the data, sequence of bytes)
    - Version ID (Allows for versioning and rolling back)
    - Metadata (Data about the data)
    - Subresources - Bucket specfic configurations
      - Bucket Policies, access control lists
      - Cross Origin Resource Sharing (CORS)
    - Transfer Acceleration
      - Allows for increase transfer speed

### The Basics

- Built for 99.99% availability for S3 platform
- Amazon Gurantees 99.9% availability
- Amazon Gurantees 99.999999999% (the 11 9's) durability for S3 information
  - This means they expect you to lose 1 file ever 10,000 years
- Tiered Storage Available
- Lifecycle Management
- Versioning
- Encryption
- Secure data access with Access Control lists

### Storage Tiers/Classes

#### S3 (standard)

- 99.99% availability
- 11 9s durability
- Redundancy exists across multiple devices in multiple facilities and is designed to sustain loss of 2 facilities concurrently

#### S3 IA (Infrequently Accessed)

- Data that is access less frequently but requires rapid access when needed
- Lower fee than S3 but chared with access data

#### S3 One Zone IA

- Same as IA however data is stored in a single AZ
- Still contains 11 9s durability
- Only 99.5% availability
- Cost 20% less than regular S3 IA

#### S3 Reduced Redundancy Storage

- Designed with only 99.99% durability
- 99.99% Availability
- Meant for data that is easily recreatable is lost
- Not offered in some regions
- AWS recommends NOT using this class
  - Recommended to use S3 standard
  - S3 standard price was reduce to be lower than this to help move people off

#### S3 Glacier

- Designed for Data that is infrequently accessed
- Very Cheap
- Takes 3-5 hours to retrieve data

#### S3 Deep Archive Glacier

- Glacier but more infrequent
- 12 hour retrieval time

#### S3 Intelligent Tiering

- Designed for data with unknown or unpredictable access patterns
- 2 tiers
  - frequent
  - infrequent
- Objects are automatically moved around between tiers depending on access patterns
- 11 9s durability
- 99.99% accessibility
- Small Monthly fee for monitoring/automation

### Charges

- Storage per GB
- Requests (GET, PUT, COPY, ect)
- Storage Mangement Pricing
  - Inventory, Analytics, Object Tags
- Data Management Pricing
  - Free transfer in
  - Charge for transfer in
- Transfer Acceleration
  - Use of CloudFront to optimize speed

## S3 ACLs & Policies

### Access Control List ACL

- Per file/object basis
  - By default only access to owner of file
- Fine grain access control

### Bucket Policies

- Documents that govern what settings for a given resource
- JSON objects
- Can use policy generator so you dont have to write JSON
  - Will generate JSON code that you can copy and paste into policy editor
  - Sometimes the policy generator will need to have a wildcard operator added to the resource

## S3 Encryption

- Encryption
  - In Transit (Encrypt data being sent to and from bucket)
    - Done with SSL/TLS
  - At Rest (Encrypt data that is in bucket)
    - Server Side Encryption
      - S3 Managed Keys - SSE-S3
        - Amazon does everything
          - Encrypts data
          - Encrypts Keys
      - AWS Key Management Service, Managed Keys, SSE-KMS
        - Get a seperate key called "Envelope Key"
          - This is key that encrypts the key
          - Get Audit trail to see when and who has used encryption key
          - Can use your own key
      - Server side Encryption with customer Provided Key
        - AWS manages encryption and decryption
        - User manages their own keys
    - Client Side Encryption
      - User encrypts files themselves before uploading files into S3
- Enforcing Encryption
  - Every upload sends a PUT request
  - Request header contains information for S3 to understand what needs to be done
  - x-amz-server-side-encryption parameter included in request header if file needs encrypted at upload time
    - Two options available
      - x-amz-server-side-encryption: AES256 (SSE-S3 - S3 managed keys)
      - x-amz-server-side-encryption: ams:kms (SSE-KMS - KMS managed keys)
  - In order to enforce encryption all we need to do is make a bucket policy that denies any S3 PUT requests which do not include the x-amz-server-side-encryption
  - How to enable
    - Can be done via the the console (which is the easy way)
    - Can be done with an S3 Bucket Policy (Written in JSON)

### Cross-Access-Resource-Sharing (CORS)

- Allows access from one resource (bucket) to another
- If you open to all you leave your resources exposed and vulnerable to attack

## CloudFront

### Content Delivery Network (CDN)

- A system of distributed servers (network) that deliver webpages and other web content to a user based on geographic locations of the user, the origin of the webpage, and a content deliver server
- Basically speeds up delivery of web content
- Content Delivery vs. Transfer Acceleration
  - CDN focus on download
  - Transfer Acceleration is upload
- Scenario
  - Website in UK
  - Users in America, South America, South Africa, Austrailia, India
    - Users further from UK can experience greater latency and less responsiveness
  - We use edge locations to keep copy of website in edge locations which are much closer to users.
    - First time user requests resource edge location makes request to server in UK and downloads the resource
    - resource is then cached so that subsequent requests for that item will be served to user from edge location
    - cache is temporary and will be cleared after a time period
    - cache can be cleared manually but there will be a fee to do so
      - This may be done if you need users to be given most recent updates
- Key Terminology
  - Edge Location
    - Location where content is cached and can also be written (Not a region or AZ)
    - More edge locations than AZs or Regions (edge locations > AZs > Regions)
  - Origin
    - The origin of all the files that the CDN will be distributing
    - Can be S3 Bucket, EC2 Instance, Elastic Load Balancer, or Route53
  - Distribution
    - The name given to CDN which consist of collection of edge locations
  - Web Distribution
    - Typically used for websites
  - RTMP
    - Used for Media Streaming
- Cloud Front can be used to deliver the ENTIRE website including the following content
  - dynamic
  - static
  - streaming
  - interactive
- Can be used with NON AWS servers
- Distribution Types
  - Web Distribution
    - Used for Websites, HTTP/HTTPS
    - Can NOT serve Adobe flash mutli media content
  - RTMP Distribution (Adobe Real Time Messaging Protocol)
    - Media streaming
    - Flash multi-media content
- CloudFront can be used for Transfer Acceleration for uploading files to S3
- You can restrict access to certain (paying usings) by using signed URL or signed cookies
- Can use WAF to protect at application layer
- Can use whitelist and blacklist to restrict access to countries
- Cache can be cleared by invalidating objects (which you will be charged for)
- CloudFront can be used to upload files as well as download files.

### S3 Perfomance Optimization

- (This has been deprecated advice since AWS increased S3 performance in 2018)
- By default S3 is designed to handle very high request rates
  - If you are recieving over 100 PUT/LIST or 300 DELETE per second then you need to optimize
  - This was changed in 2018 to 3500 put requests per second and 5500 get requests
- Mixed Request Type Workloads
  - A mix of GET, PUT, DELETE, LIST
- Optimize by NOT using sequential keys as part of the file names
  - Random over sequential
- This spreads the I/O on different partitions which spreads the I/O

## Serverless

- Brief history
  - Data Center --> IAAS --> PAAS --> Containers --> Serverless
  - AWS  released EC2 2006 (Birth Of IAAS)
  - Azure releases Platform As A Service (PAAS)
  - Then containers came about and gave lightweigh alternative to server
  - Lambda was release and serverless computing was born
    - No need to worry about anything but code
    - Every Alexa command is just Lambda speaking back

### Lambda

- Lambda is a compute service where you can upliad your code and create a lambda function.
- AWS lambda takes care of provisioning and managing the servers that you use to run the code.
- Removes the need to worry about hardware, Operating systems, application layers, etc. Just worry about code
- Can be used as:
  - An event-driven compute service where AWS labda runs your code in response to events.
    - Could be changes to data in s3, or dynamodb, etc
    - As compute service to respond to HTTP request using Amazon API Gateway
- Languages supported by lambda
  - NodeJS
  - Java
  - Python
  - C#
  - Go
  - Ruby
  - Powershell

#### Lambda Pricing

- Priced on number of request
  - First 1 million requests are free. Then $0.20 per 1 million request thereafter
- Duration
  - Duration is calculated from time code begins executing until it returns or terminates
    - This is rounded up to the nearest 100ms
  - price also depends on amount of memoyr you allocate to your function ($0.00001667 per GB-second)

#### Lambda Highlights

- No servers!
- Continous Scaling
- Super super cheap (A Cloud Gurus site is less than $1.00 a month)

#### Lambda Exam Tips

- Lambda scales out (NOT up) automatically
  - Millions of functions running in parrallel
  - Will not increase memory the function uses
- Lambda functions are independent (1 event = 1 function)
- Lambda is serverless
  - Also remember it is a compute service
- Know what services are serverless
  - Lambda
  - S3
  - API Gateway
  - DynamoDB
  - SNS
  - Kinesis
- Lambda functions can trigger other lambda functions
  - 1 event can = x functions if function triggers other functions
- Architectures can get extreamly complicated
  - AWS X-ray allows you to debug Lambda
- Lambda can do things globally they are not limited to their regions
- Know your triggers
- Can have multiple versions of lambda functions
- Latest version will always use $latest
- Qualified version will use $latest, unqualified will not have it
- Versions are immutable (CANNOT be changed)
- CANNOT split traffic with $latest instead you need to create an alias to latest

#### Lambda Triggers (TODO)

#### Lambda Versioning

- When versioning you can publish more than one version of your lambda functions
- After version is published it is immutable
- Latest is the only version that can be edited
- ARN types:
  - Qualified ARN
    - Does Have version at the end
  - Unqualified ARN
    - Does not have version at end
- Aliases can be used to point to lambda versions

### API Gateway

#### What is an API

- An API is a an application programming interface
  - Takes request does sends it somewhere, gets a response then returns response to whoever made the original request.

#### Types of APIs

- REST APIs (REpresentational State Transfer)
  - Uses JSON (typically)
- SOAP APIs (Simple Object Access Protocol)
  - Uses XML
  - Not very simple

#### What is API Gateway

- Amazon API Gateway is a fully managed service that makes it easy for developers to publish, maintain, monitor, and secure APIs at any scale.
  - Witha  few clicks in the AWS Management Console you can create an API that acts as a front door for applications to access data, business logic, or functionality from your back-end services.
    - These services can be:
      - EC2
      - AWS Lambda
      - Any Web Application

- What can API Gateway do
  - Expose HTTPS endpoints to define a RESTful API
  - Serverless-ly connect to services like lambda and Dynabmodb
  - Send each API endpoint to different target
  - Runs efficiently with low cost
  - Scale effortlessly
  - Track and control usage by API key
  - Throttle requests to prevent attacks
  - Connect to CloudWatch to log all request for monitoring
  - Control multiple versions of API

- How to configure API Gateway
  - Define API (container)
  - Define Resources and nested Resources (URL Paths)
  - For each resource:
    - Select supported HTTP methods (verbs)
    - Set security
    - Choose target (such as EC2, Lambda, DynamoDB, etc.)
    - Set request and response transformations
  - Deploy API to a Stage
    - Use API Gateway domain, by default
    - Can use custom Domain
    - Supports AWS Certificate Manager (FREE SSL/TLS certs!)
      - If you bought Domain with Route53

#### API Caching

- You can enable API caching in Amazon API Gateway to cache your endpoint's response
  - Reduce the number of calls made to your endpoint
  - Improve the latency of the calls made to your endpoint and improve the latency of the requests to your API
  - When enabled for a stage API Gateway caches responses from your endpoint for a specified time-to-live (TTL) period in seconds
  - Then responds to the request by looking up the endpoint response from the cache instead of making a request to your endpoint

#### Same Origin Policy

- concept in web application security model.
  - Web browser will allow scripts contained in a web page to access data in second webpage ONLY if both web pages have the same origin.
    - This is done to prevent Cross-Site Scripting (XSS) attacks
  - Enforced by Web browsers
  - Ignored by tools (Postman, Insomnia, Curl, etc.)

#### Cross-Origin Resource Sharing (CORS)

- Way the server at the other end (not the client code in the browser) can relax the same-origin policy
- Cross-origin resource sharing (CORS) is a mechanism that allows restricted resources on a web page to be requested from another domain outside the domain from wich the first resource was served.
- Browser makes HTTP OPTIONS call for URL
  - OPTIONS is an HTTP method like GET, PUT, and POST
- Server returns a response that says "These other domains are approved to GET this URL"
- Error - "Origin policy cannot be read at the remote resource?"
  - This means you need to enable CORS on API Gateway

### Advanced API Gateway

- API Gateway import features allows you to import Swagger v2.0 definition files
  - Can overwrite definitions
  - Can merge definitions
- API Throttling
  - By default is throttle to 10,000 requests per seconds
  - Max number of concurrent requests is 5,000
  - If limits are reached you will get a 429 Too Many Requests status code
  - Limits can be lifted but further charges will be incured
- API Gateway can be used as SOAP web service passthrough

### Step Functions

- Allows visualization of your serverless functions
- Provide graphical console to arrange and visualize components of your application as a series of steps
- Makes running multistep applications simple
- Automatically trigger and tracks each step, and retries when there are errors so your app executes in order and as expected
- Setp Functions log the state of each step so when things do go wrong you can diagnose and debug problems quickly

### X-Ray

- X-Ray is a service that collects data about requests that you application serves
- Visualize serverless application
- See detailed information about any TRACE request to application and downstream services that get used
- How to use:
  - Install X-Ray SDK in code
  - SDK will then send JSON information to the X-Ray Daemon
  - The Daemon will then send data to the X-Ray API
- SDK gives you
  - Interceptors to add to your code to trace incoming HTTP requests
  - Client handlers to instrument AWS SDK clients that your application uses to call other AWS services
  - A HTTP client to use  to instrument calls to other internal and external HTTP web services
- Integration
  - Elastic Load Balancing
  - AWS Lambda
  - Amazon API Gateway
  - Amazon Elastic Compute Cloud
  - AWS Elastic Beanstalk
- Languages Supported
  - Java
  - Go
  - Node js
  - Python
  - Ruby
  - .NET

### Dynamodb

- Dynamodb is a fast and flexible NoSQL
- Designed for apps that need single-digit millisecond latency at any scale
- Full managed databse that supports both document and key-value data models
- Has flexible data model and reliable performance
- Great fit for mobile, web, gaming, ad-tech, IoT applicaitons
- Dynamodb is serverless and scalable
- Backed by SSD Storage
- Spread accross 3 geographically distinc data centers
- Choice of 2 consitency models:
  - Eventual consistent Reads (Default)
    - Consistency across all copies of data that is usually reached within a second
  - Strongly consistent Reads
    - Returns a result that reflects all writes that received a successful response prior to the read
- Dynamodb make up:
  - Tables
  - Items (think row in table)
  - Attribute (Think Column of table)
  - Key (identifier for data)
  - Value (actual data)
  - Documents can be written in JSON, HTML, XML

#### Dynamodb Primary Keys

- Dynamodb stores and retrieves data based on Primary Key
- Two types of primary keys
  - Partition Key
    - Unique attribute (example user ID)
    - Value of partition key is input to internal hash function which determines the partion or physical location on which the data is stored
    - If using partition key as your primary key, then no two items can have the same partition key
  - Composite Key (Partition Key + Sort Key) in combination. Same user posting mutiple times in forum
    - Primary key would be COmposite Key consisting of:
      - Partition Key - User ID
      - Sort key - Timestamp of the post
      - 2 items may have the same partition key but they must have a different Sort key
      - All items with same Partition Key are stored together, then sorted according to the sort key value
      - Allows you to store multiple items with the same Partition Key
  
#### Dynamodb Access Control

- Authentication and Access Control managed using AWS IAM
- Create an IAM user within your AWS accoun which has specific permissions to access and create DynamoDB tables
- Create IAM role which can enable you to obtain temporary access keys
- Can create special IAM condition to restrict user access to only their records.

#### Exam Tips

- Low latency
- Supports both document and key value data models
- JSON, HTML, XML
- 2 types of primary key
  - Partion key
  - Composite Key (Partition + Sort Keys)
- Consistency models
  - Strongly Consitent
  - Eventually Consistent

#### Indexies

- 2 types of indexes supported to help speed up queries
  - Local Secondary Index
    - Can only be created when creating table
    - Cannot be added or modified later
    - Has same partition key as table
    - Has different sort key than table
    - ANy queries based on this sort Key are much faster than using the index than the main table
  - Global Secondary Index
    - Much more flexible
    - Create index whenever you like
    - Choose different partion key and sort key to original table
    - Speeds up any queries relating to this alternative partion and sort key

#### Indexies Exam Tips

- Indexies enable faster queries on data
- Gives different view of your data based on alternative Partion / Sort keys
- Differences in 2 indexies
  - Local created at table creation. Same partion different sort
  - Global secondary created whenever and has different partion and different sort keys

#### Dynamodb Scan vs Query API Calls

##### Query

- A query is operation that finds items in your table based on primary key attribute and distinct value to search for
  - If looking for user with ID of 212 then you would query based off primary user ID and value 212
  - This will select all attributes for document
- Can use optional sort key name and value to refine results
- By default query returns all attributes for item
  - ProjectionExpression parameter will allow you to specify what attributes should be return
- Results always sorted by sort key
  - Numeric order by default in ascending order (1,2,3,4)
  - Can reverse order by setting ScanIndexForward (Tricky because this is for Query not SCAN!) paramerte to false
- By default Queries are eventually consistent
- Can be explicitly set for Stongly consistent

##### Scan

- A scan operation examines ever item in the table
- By default returns all data attributes
- Can also use ProjectionExpression parameter to set what attributes to return
- Can filter results of scan after they have been run

##### Query Or Scan

- Query is more efficient than Scan
- Scan dumps the entire table then filters out the values to provide
- Scans take longer the larger the table gets
- Scan operation on a large table can use up the provisioned throughput for a table in just one single operation
- You can reduce impact of query or scan by setting smaller page size
  - could set page size to 40
    - larger number of operations with smaller size each
- Avoid using scan operations if you can
  - design tables in a way that you can use the query, GET, or BatchGetItem APIs
- By default scan operation processes data sequentially then returns in 1 MB incements
  - only scans one partition at a time
- Can configure scan to run in parrallel if you divide a table or index into segments

##### Scan and Query exam tips

- Query operation finds items in table using only the primary key attribute
- You provide the primary key name and distinct value to search
- Scan operation examines every item in the table
- Both return all data attributes by default
- Use ProjectionExpression parameter to refine results
- Query results alwasy sorted by Sort key
- Sorted in ascending order
- Set ScanIndexForward parameter to false to reverser the order (QUERIES ONLY)
- Query operation is generally more efficient than scan
- Reduce page size to make scan more efficient
- Can make parrallel scan
- Design tables to use query, GET, or BatchGetItem APIs

#### DynamoDb Provisioned Throughput

- Throughput measured in capacity Units
- Two Types of Capacity Units
  - Write Capacity Unit
    - 1 x Write Capacity Unit = 1 x 1KB Write per second
  - Read Capacity Unit
    - 1 x Read Capacity Unit = 1 x Strongly Consistent Read of 4KB per second OR 2 x Eventually Consistent Reads of 4KB per second (DEFAULT)
- If application reads or writes large objects it will cost more

##### Provisioned Throughput Exam Tips

- Provisioned throughput is measured in capacity units
- 1 x Write Capacity = 1 x 1KB Write per second
- 1 x Read Capacity Unit = 1 x Strongly Consistent Read of 4KB per second OR 2 x Eventually Consistent Reads of 4KB per second (DEFAULT)
- When Calculating take number of reads or writes a second multiply that by the size per operation / the per second of operation rounded up.

#### DynamoDB OnDemand Capacity

- New Pricing option
  - Chareges apply for Reading, Writing, and Storing data
  - Do not need to specify Read and Write capacity
  - Will scale up and down based on read and writes to your database
  - Ideal for unpredictable workloads
  - Allows you to pay for only what you use (pay per request)

#### DynamoDB Accelerator (DAX)

- Fully managed clustered in-memory cache for DynamoDB
- ONLY FOR READ operations
- Delivers up to 10x read performance
- Microsecond performance for millions of requests per second
- Ideal for Read-Heavy and bursty workloads

- How does it work
  - DAX is write-through caching service
    - When data is written to dynamodb it is also written to DAX
    - Point Dynamodb API Calls to DAX cluster
    - If item is in DAX it will be returned from DAX
    - If item does not exist then DAX will retrieve item from DynamoDB and write it in cache for further requests
- Allows ability to reduce Provisioned Read Capacity

- Not GOOD for
  - Caters ONLY for Eventually consitent reads
    - CANNOT do Strongly Consitent
  - Write intensive
  - Applications that do not perform many read operations
  - Applications that dont require microsecond response times

### Elasticache with DynamoDB

- In memory caching that sits infront of many RDS databases
- This can also sit infront of Dynamodb
- Sits between application and database
- Takes load off database
- good if your database is particularly read-heavy and the data is not changing frequently
- Supports Memcached and Redis
- 2 Stategies available
  - Lazy Loading
    - Loads data into cache only when necessary
    - if requested data is in cache Elasticache returns data to application
    - If not in cache or has expired Elasticache returns a null
      - Application then fetches data from the database and writes the data recieved into cache so that is available next time
    - Advantages:
      - Only requested data cached
      - Node failures are not fatal
    - Disadvantages:
      - Cache miss penalty (initial request query to database and write data after done)
      - Stale data - if data is only updated when cache is updated it can become out of date and does not automatically update
    - Time To Live (TTL)
      - How to deal with stale data
      - Sets a number of seconds until data expires
      - Hits on expired data will be treated as miss
  - Write-Through
    - adds or updates data to cache whenever data is written to database
    - Advantages:
      - Data is never stale
      - Users are generally more tolerant of additional latency when updating data than when retrieving it
    - Disadvantages
      - Does invoke write penalty for having to write twice
      - If node fails and new one is spun up data is missing until added or updated
        - This can be mitigated by implementing lazy loading in conjucture with write-through)
      - Wasted resources if most of data is never read

#### DAX vs Elasticache

- DAX optimized just for DynamoDB
- DAX ONLY supports Write-Through
- If you need lazy loading you have to use Elasticache

### DynamoDB Transactions

- DynamoDB Transactions were designed for mission critical operations
- Transactions
  - ACID Transactions (Atomic, Consitent, Isolated, Durable)
  - Read or write multiple items across multiple tables as an all or nothing operation
  - Check for a pre-requisite condition before writing to a table
- Implement complex business logic into single atomic transaction

### DynamoDB TTL

- DynamoDB Time To Live (TTL)
- Time To Live is attribute that defines an expiry time for your data
- Expired items marked for deletion
- If data is marked it will be deleted with in 48 hours
- Good for removing irrelevant or old data
  - Session data
  - Event Logs
  - Temporary data
- Reduce cost by removing data no longer relevant
- TTL is expressed as epoch/unix time
  - numeric value represents the number of seconds that have elapsed since 12am January 1 1970
- When current time is greater than TTL the item will become expired and marked for deletion
- You can filter out expired items from your queries and scans
  - This is useful because deletes can take 48 hours

### DynamoDB Streams

- Streams are Time-ordered sequence of itme level modifications (insert, update, delete)
- Logs are encrypted at rest and stored for 24 hours
- Accessed using a dedicated endpoint
- By default the Primary key is recorded
- Before and After images can be captured
- Used for triggers
- Accessed through their own endpoints
- Events are recorded in near real time
- Really good for serverless and lambda
- Application can take actions based on content
- Lambda can pull stream and trigger events based on stream events

### Provisioned Throughput Exceeded Exception

- Will see this if your request read/write capacity provisioned is exceeded for DynamoDB table
  - SDK will autoretry until successful
  - If not using SDK
    - Reduce request frequency
    - Implement Exponetial backoff

#### Exponential Backoff

- Components in network can generate errors due to being overloaded
  - Usally dealt with by implementing retries (which SDK does)
  - In addition to reties SDK also uses exponential Backoff
- Progressively longer waits between consecutive retries (50 ms, 100 ms, 200ms)
- if after 1 minute does not work, your request size may be exceeding the throughput for read/write capacity
- Exponential backoff is used for more than Dynamodb. Every feature of AWS SDK.
  - Applies to many services in AWS
    - S3
    - CloudFormation
    - SES
  - If not using SDK will need to implement this yourself in the application

## Key Management Service KMS

- Service to manage encryption keys for your data on AWS
- Integrated for seamless use with many AWS services
- Simple to encrypt data with keys you manage
- When to use:
  - Whenever working with sensitive data
  - Customer Data
  - Financial Data
  - Secrets
  - Credentials
- Integrates with:
  - S3
  - RDS
  - DynamoDB
  - Lambda
  - EBS
  - EFS
  - CloudTrail (know who has been using keys and accessing data)
  - Developer Tools

### CMK

- Customer Master Key
  - Can Encrypt and decrypt data up to 4KB
  - Used to generate encrypt and decrupt Data Ke
- Data Key
  - Used to encrypt data
- Known as Envelope Encryption

- Symmetric Keys
  - Single key for both encrypt and decrypt
- Asymetric Keys
  - Public and private keypair that can be used for encrypt/decrypt or sign/verify
  - If you want people outside your AWS IAM to use you will need to use public key in Asymetric

#### CMK Exam tips

- Can use Alias to refer to CMK
- Has Creation Date
- Has description
- Has Key State (Enabled, Disabled, Pending, Deletion, Unavaible)
- Key Material (Customer Provided, KMS Provided)
- Stays Inside KMS

- Setting up CMK (Alias --> Description --> Key Material)
- Key Adminstration Permissions (Users --> Roles --> Admin Permissions)
  - Users and roles who can administer key
- Key Usage Permissions (Users --> Roles --> Admin Permission)
  - users and roles who will use key

- AWS-Managed CMK
  - Created by AWS for interaction with AWS services
- Customer-Manged CMK
  - Keys created and managed by users

- DataKey
  - Used to encrypt and decrypt data
  - Can be generated from CMK

#### KMS API Calls

- `aws kms encrypt`
  - cant take name of file to encrypt
  - output name to put encrypted file
  - creates a sipher text output
- `aws kms decrypt`
  - used to decrypt encrypted file
  - decrypts cipher text back to plain text
- `aws kms re-encrypt`
  - allows rotation of encrypted files keys
  - decrypts then re-encrypts with new key
- `aws kms enable-key-rotation`
  - Allows AWS to rotate your key on annual basis
- `aws kms generate-data-key`
  - Creates a data key so you can encrypt data above 4KB

#### Envelope Encryption

- Process for encrypting your data
  - for files over 4KB in size
- How to get one
  - Use CMK to generate Data-key
- Why use it
  - Network
    - When you encrypt data directly with KMS it must be transferred over the network
  - Performance
    - With envelope encryption, only the data key goes over the netwoek not your data
  - Benefits
    - The data key is used locally in your application or AWS servic. Avoiding the need to transfer large amounts of data to KMS
  