# EBS Volumes

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

## IOPS

- Measures number of read and write operations per seconds
  - Important metric for quick transactions, low latency apps, transaction workloads
  - The ability to action reads and writes very quick
- Throughput
  - Measures number of bits read or written per seconds
  - Important metric for large datasets, large I/O sizes, complex queries
  - All about ability to deal with large datasets.