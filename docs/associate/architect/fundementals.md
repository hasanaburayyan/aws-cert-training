# AWS Fundamentals

## Global Infrastructure

Global infrastructure is made up of Regions, AZs, and Edge locations

Currently there are 22 Regions and 77 Availability Zones

### Regions

Physical location in world that consists of two or more AZs

Regions are just geographical Area. such as Sydney Australia or us-east-2 in the United States.

Each Region consists of 2 or more Availability Zones

### AZs

One or more discrete data centers with redundant power networking and connectivity.

Area meaningfully separated from each other, based on geographical data

### Edge Locations

Endpoints for AWS that are used for caching content. Currently over 215 edge locations

### Exam Tips

1. Region is a physical location in world that consists of two or more AZs
2. An Availability zone is a discrete data center, each with redundant power, networking, and connectivity housed in separate facility
3. Edge locations are endpoints for AWS that are used for caching content. Typically consists of CloudFront (Amazons content delivery Network CDN)
4. Always ask yourself this question when thinking about shared responsibility model, "Can you do this yourself in AWS Management Console?"
   1. If Yes, you are probably responsible
   2. If No, AWS is probably responsible
5. Encryption is shared responsibility
6. Compute Services are: EC2, Lambda, Elastic Beanstalk
7. Storage Services are: S3, EBS, EFS, FSx, Storage Gateway
8. Databases Services are: RDS, DynamoDB, Redshift
9. Networking: VPCs, Direct Connect, Route53, API Gateway, AWS Global Accelerator
10. DONT FORGET: Read whitepaper for well architected before taking exam!!


