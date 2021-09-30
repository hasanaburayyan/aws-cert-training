# API Gateway

## What is an API

- An API is a an application programming interface
  - Takes request does sends it somewhere, gets a response then returns response to whoever made the original request.

### Types of APIs

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

## What is API Gateway

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

### API Caching

- You can enable API caching in Amazon API Gateway to cache your endpoint's response
  - Reduce the number of calls made to your endpoint
  - Improve the latency of the calls made to your endpoint and improve the latency of the requests to your API
  - When enabled for a stage API Gateway caches responses from your endpoint for a specified time-to-live (TTL) period in seconds
  - Then responds to the request by looking up the endpoint response from the cache instead of making a request to your endpoint

### Same Origin Policy

- concept in web application security model.
  - Web browser will allow scripts contained in a web page to access data in second webpage ONLY if both web pages have the same origin.
    - This is done to prevent Cross-Site Scripting (XSS) attacks
  - Enforced by Web browsers
  - Ignored by tools (Postman, Insomnia, Curl, etc.)

### Cross-Origin Resource Sharing (CORS)

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