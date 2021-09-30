# RDS (OLTP)

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