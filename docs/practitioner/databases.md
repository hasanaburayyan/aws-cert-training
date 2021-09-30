# Databases

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

## NON-Relational Database on AWS

Columns in table can vary
Previous columns will not affect other rows in the database
Amazons NON-Relational Database is called DynamoDB

### Online Transaction Processing (OLTP)

- Pulls up a row of data such as Name, Date, Address to deliver to, etc.
- Basically takes/inserts a row from database

### Online Analytics Processing (OLAP)

- Pulls huge number of records
- Massive performance needed
- Data warehouse created to solve this.

## Data-warehouse

Use different architecture
Designed to handle large scale calculations of data away from the database so that database performance is not affected.
AMAZON'S Redshift

## ElastiCache

- Web service that makes it easy to deploy, operate and scale an in-memory cache in the cloud.
- Improve performance of web application
- Caches most common queries to return data to users.
- Takes massive load off database queires
- Comes in Memcached and Redis

## Graph database

Amazon Neptune is Amazon’s graph database