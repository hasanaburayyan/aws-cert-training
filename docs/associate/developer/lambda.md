# Lambda

- Lambda is a compute service where you can upload your code and create a lambda function.
- AWS lambda takes care of provisioning and managing the servers that you use to run the code.
- Removes the need to worry about hardware, Operating systems, application layers, etc. Just worry about code
- Can be used as:
  - An event-driven compute service where AWS lambda runs your code in response to events.
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

## Lambda Pricing

- Priced on number of request
  - First 1 million requests are free. Then $0.20 per 1 million request thereafter
- Duration
  - Duration is calculated from time code begins executing until it returns or terminates
    - This is rounded up to the nearest 100ms
  - price also depends on amount of memoyr you allocate to your function ($0.00001667 per GB-second)

## Lambda Highlights

- No servers!
- Continous Scaling
- Super super cheap (A Cloud Gurus site is less than $1.00 a month)

## Lambda Exam Tips

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
- Can have multiple versions of lambda functions### API Gateway

#### What is an API

- An API is a an application programming interface
  - Takes request does sends it somewhere, gets a response then returns response to whoever made the original request.

#### Types of APIs

- REST APIs (REpresentational State Transfer)
  - Uses JSON (typically)
- SOAP APIs (Simple Object Access Protocol)
  - Uses XML
  - Not very simple## Serverless

- Brief history
  - Data Center --> IAAS --> PAAS --> Containers --> Serverless
  - AWS  released EC2 2006 (Birth Of IAAS)
  - Azure releases Platform As A Service (PAAS)
  - Then containers came about and gave lightweigh alternative to server
  - Lambda was release and serverless computing was born
    - No need to worry about anything but code
    - Every Alexa command is just Lambda speaking back
- Latest version will always use $latest
- Qualified version will use $latest, unqualified will not have it
- Versions are immutable (CANNOT be changed)
- CANNOT split traffic with $latest instead you need to create an alias to latest

## Lambda Triggers (TODO)

## Lambda Versioning

- When versioning you can publish more than one version of your lambda functions
- After version is published it is immutable
- Latest is the only version that can be edited
- ARN types:
  - Qualified ARN
    - Does Have version at the end
  - Unqualified ARN
    - Does not have version at end
- Aliases can be used to point to lambda versions