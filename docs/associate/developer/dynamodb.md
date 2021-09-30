# Dynamodb

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

## Dynamodb Primary Keys

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
  
## Dynamodb Access Control

- Authentication and Access Control managed using AWS IAM
- Create an IAM user within your AWS accoun which has specific permissions to access and create DynamoDB tables
- Create IAM role which can enable you to obtain temporary access keys
- Can create special IAM condition to restrict user access to only their records.

## Exam Tips

- Low latency
- Supports both document and key value data models
- JSON, HTML, XML
- 2 types of primary key
  - Partion key
  - Composite Key (Partition + Sort Keys)
- Consistency models
  - Strongly Consitent
  - Eventually Consistent

## Indexies

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

### Indexies Exam Tips

- Indexies enable faster queries on data
- Gives different view of your data based on alternative Partion / Sort keys
- Differences in 2 indexies
  - Local created at table creation. Same partion different sort
  - Global secondary created whenever and has different partion and different sort keys

## Dynamodb Scan vs Query API Calls

### Query

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

### Scan

- A scan operation examines ever item in the table
- By default returns all data attributes
- Can also use ProjectionExpression parameter to set what attributes to return
- Can filter results of scan after they have been run

### Query Or Scan

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

### Scan and Query exam tips

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

### DynamoDb Provisioned Throughput

- Throughput measured in capacity Units
- Two Types of Capacity Units
  - Write Capacity Unit
    - 1 x Write Capacity Unit = 1 x 1KB Write per second
  - Read Capacity Unit
    - 1 x Read Capacity Unit = 1 x Strongly Consistent Read of 4KB per second OR 2 x Eventually Consistent Reads of 4KB per second (DEFAULT)
- If application reads or writes large objects it will cost more

#### Provisioned Throughput Exam Tips

- Provisioned throughput is measured in capacity units
- 1 x Write Capacity = 1 x 1KB Write per second
- 1 x Read Capacity Unit = 1 x Strongly Consistent Read of 4KB per second OR 2 x Eventually Consistent Reads of 4KB per second (DEFAULT)
- When Calculating take number of reads or writes a second multiply that by the size per operation / the per second of operation rounded up.

## DynamoDB OnDemand Capacity

- New Pricing option
  - Chareges apply for Reading, Writing, and Storing data
  - Do not need to specify Read and Write capacity
  - Will scale up and down based on read and writes to your database
  - Ideal for unpredictable workloads
  - Allows you to pay for only what you use (pay per request)

## DynamoDB Accelerator (DAX)

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

## Elasticache with DynamoDB

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

### DAX vs Elasticache

- DAX optimized just for DynamoDB
- DAX ONLY supports Write-Through
- If you need lazy loading you have to use Elasticache

## DynamoDB Transactions

- DynamoDB Transactions were designed for mission critical operations
- Transactions
  - ACID Transactions (Atomic, Consitent, Isolated, Durable)
  - Read or write multiple items across multiple tables as an all or nothing operation
  - Check for a pre-requisite condition before writing to a table
- Implement complex business logic into single atomic transaction

## DynamoDB TTL

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

## DynamoDB Streams

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

## Provisioned Throughput Exceeded Exception

- Will see this if your request read/write capacity provisioned is exceeded for DynamoDB table
  - SDK will autoretry until successful
  - If not using SDK
    - Reduce request frequency
    - Implement Exponetial backoff

## Exponential Backoff

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