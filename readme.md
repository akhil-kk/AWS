## IAM - Identitiy Access Management

* Its a Global service.
* Root account created by default, shouldn't be used or shared.
* Groups only contain users, not other groups.
* A user dont ahve to belong to a group, and a user can belong to multiple groups.
* Users or Groups can be assigned JSON document called policies.
* In AWS you apply the least privilege principle: dont give more permissions than a user needs.

**IAM password policy**

* set a min password length
* Require users to chnage their password after some time.
* MFA = password you know + security device you own.

### MFA devices in AWS

* Google authenticator
* Authy - muti-device
* Yubikey - support multiple root
* Hardware key fob MFA

## AWS CLI

* To access AWS you have three options.
    * AWS management console.
    * AWS command line interface
    * AWS sofwtare development kit.
* Access keys are generated through the AWS console.
```
aws iam list-users          // list all users
```

## IAM Roles

* Some AWS service will need to perform actions on your behalf.
* To do so we will assign permissions to AWS services with IAM roles.
* Common Roles
    * EC2 Instance Roles.
    * Lambda Function Roles.
* IAM roles are a secure way to grant permissions to entities that you trust. Examples of entities include the following:

    * IAM user in another account.
    * Application code running on an EC2 instance that needs to perform actions on AWS resources.
    * An AWS service that needs to act on resources in your account to provide its features.
    * Users from a corporate directory who use identity federation with SAML.
    * IAM roles issue keys that are valid for short durations, making them a more secure way to grant access.

## IAM securtiy tools

* IAM Credentials report

A report that lists all your account's users and the status of their various credentials.

* IAM Access advisor 

Access advisor shows the service eprmissions granted to auser and when those services were last accessed.

## IAM Guidelines

* Dont use root account except for aws account setup
* One physical user = one AWS user.
* Assign users to groups and assign permissions to groups.
* Create a strong password policy.
* Use and enforce the use of MFA.
* Create and use Roles for giving permissions to AWS services.
* Use Access Keys for Programmatic Access.
* Audit permissions of your account with the IAM credentails report.

## Amazon EC2

* Most popular of AWS' offering.
* EC2 = Elastic Compute Cloud = Infrastructure as aservice.
* Capabilities
    * Reting VMs (EC2).
    * Storing data on Virtual drives(EBS).
    * Distributing load across machines(ELB).
    * Scaling services using an auto-scaling group (ASG).

## EC2 sizing & Config

* OS
* CPU
* RAM
* Storage 
    * Network-attached(EBS & EFS)
    * hardsware (EC2 instance & Store)
* N/W card
* Bootstrap script: EC2 user data.

## EC2 instance types, examples

![Ec2 instance types](img/ec2.png?raw=true "Title")

## Launching an EC2 instance

 * Choose an Amazon Machine Image (AMI) - contains all your software config.

## Introduction to Security groups

* Act as a firewall on EC2 instances.
* How traffic is allowed into or out of our EC2 instances.
* Security groups only contain allow groups
* Security groups can reference by Ip or by security group.
* They regulate 
    * Access to ports
    * Authorised IP ranges

## Ports to know

![Ports](img/ports.png?raw=true "Title")

## SSH

![SSH](img/ssh.png?raw=true "Title")

## EC2 instance launch types

* On demand instance; short workload, predictable pricing
* Reserved: (min 1year)
* Dedicated hosts.
* Spot instances

## EC2 instance Storage

### EBS volume (Elastic Block Store)

* network drive you can attach to your instances while they run.
* It allows your instances to persist data even after their termination.

**EBS Volume**

* Its a network drive
* Uses nw to communicate to instance.
* It can be detached from an EC2 instance and attcahed to another one.
* Its locked to an availability zone
* To move volume across, you need to snapshot it.
* Have provisioned capacity.

### EBS Snapshots

* Make a backup of your EBS volume at a point in time.
* Not necessary to detach volume eto do snapshot, but recommended.
* Can copy snaoshots across AZ or Region.

### AMI

* AMI = Amazon Machine Image
* AMI are a customization of an EC2 instance
* You add your own software, configuration, operating system, monitoring…
* Faster boot / configuration time because all your software is pre-packaged
* AMI are built for a specific region (and can be copied across regions)
* You can launch EC2 instances from:
* A Public AMI: AWS provided
* Your own AMI: you make and maintain them yourself

### EC2 Instance Store

* EBS volumes are network drives with good but “limited” performance
* If you need a high-performance hardware disk, use EC2 Instance Store
* Better I/O performance
* EC2 Instance Store lose their storage if they’re stopped (ephemeral)
* Good for buffer / cache / scratch data / temporary content
* Risk of data loss if hardware fails
* Backups and Replication are your responsibility

### EFS – Elastic File System
* Managed NFS (network file system) that can be mounted on 100s of EC2
* EFS works with Linux EC2 instances in multi-AZ
* Highly available, scalable, expensive (3x gp2), pay per use, no capacity planning

![EBSvsEFS](img/ebsVsefs.png?raw=true "Title")


## Elastic Load Balancing and Auto Scaling

### Scalability & High Availability
* Scalability means that an application / system can handle greater loads
by adapting.
* There are two kinds of scalability:
* Vertical Scalability
* Horizontal Scalability (= elasticity)
* Scalability is linked but different to High Availability

## Vertical Scalability
* Vertical Scalability means increasing the size
of the instance
* For example, your application runs on a
t2.micro
* Scaling that application vertically means
running it on a t2.large
* Vertical scalability is very common for non
distributed systems, such as a database.
* There’s usually a limit to how much you can
vertically scale (hardware limit)

## Horizontal Scalability
* Horizontal Scalability means increasing the
number of instances / systems for your
application
* Horizontal scaling implies distributed systems.
* This is very common for web applications /
modern applications
* It’s easy to horizontally scale thanks the cloud
offerings such as Amazon EC2

## Load Balancers

* Load balancers are servers that forward internet traffic to multiple servers (EC2 Instances) downstream.

    **Why use a load balancer?**

    * Spread load across multiple downstream instances
    * Expose a single point of access (DNS) to your application
    * Seamlessly handle failures of downstream instances
    * Do regular health checks to your instances
    * Provide SSL termination (HTTPS) for your websites
    * High availability across zones
## 3 kinds of load balancers offered by AWS:

* Application Load Balancer (HTTP / HTTPS only) – Layer 7
* Network Load Balancer (ultra-high performance, allows for TCP) – Layer 4
* Classic Load Balancer (slowly retiring) – Layer 4 & 7

## Auto Scaling Group

* The goal of an Auto Scaling Group (ASG) is to:
    * Scale out (add EC2 instances) to match an increased load
    * Scale in (remove EC2 instances) to match a decreased load
    * Ensure we have a minimum and a maximum number of machines running
    * Automatically register new instances to a load balancer
    * Replace unhealthy instances

## Amazon S3

* Amazon S3 is one of the main building blocks of AWS
* It’s advertised as ”infinitely scaling” storage.

### S3 Use cases
* Backup and storage
* Disaster Recovery
* Archive
* Hybrid Cloud storage
* Application hosting
* Media hosting
* Data lakes & big data analytics
* Software delivery
* Static website

### Amazon S3 Overview - Buckets

* Amazon S3 allows people to store objects (files) in “buckets” (directories)
* Buckets must have a globally unique name (across all regions all accounts)
* Objects (files) have a Key
* The key is the FULL path:
    * s3://my-bucket/my_file.txt
    * s3://my-bucket/my_folder1/another_folder/my_file.txt

### S3 Bucket Policies

* JSON based policies
    * Resources: buckets and objects
    * Actions: Set of API to Allow or Deny
    * Effect: Allow / Deny
    * Principal: The account or user to apply
    the policy to
* Use S3 bucket for policy to:
    * Grant public access to the bucket
    * Force objects to be encrypted at upload
    * Grant access to another account (Cross
    Account)

![s3 bucket policy](img/s3policy.png?raw=true "Title")

### S3 Websites

* S3 can host static websites and have them accessible on the www
* The website URL will be:
    * <bucket-name>.s3-website-<AWS-region>.amazonaws.com
    OR
    * <bucket-name>.s3-website.<AWS-region>.amazonaws.com

## Amazon S3 - Versioning

* You can version your files in Amazon S3
* It is enabled at the bucket level
* Same key overwrite will increment the “version”: 1, 2, 3….
* It is best practice to version your buckets
    * Protect against unintended deletes (ability to restore a version)
    * Easy roll back to previous version

### S3 Access Logs

* For audit purpose, you may want to log all access to S3
buckets
* Any request made to S3, from any account, authorized or
denied, will be logged into another S3 bucket
* That data can be analyzed using data analysis tools…
* Very helpful to come down to the root cause of an issue,
or audit usage, view suspicious patterns, etc…

### S3 Replication (CRR & SRR)

* Must enable versioning in source and destination
* Cross Region Replication (CRR)
* Same Region Replication (SRR)
* Buckets can be in different accounts
* Copying is asynchronous
* Must give proper IAM permissions to S3

### S3 Storage Classes

* Amazon S3 Standard - General Purpose
* Amazon S3 Standard-Infrequent Access (IA)
* Amazon S3 One Zone-Infrequent Access
* Amazon S3 Intelligent Tiering
* Amazon Glacier
* Amazon Glacier Deep Archive
* Amazon S3 Reduced Redundancy Storage (deprecated - omitted)

### S3 Standard – General Purposes

* 99.99% Availability
* Used for frequently accessed data
* Low latency and high throughput
* Sustain 2 concurrent facility failures
* Use Cases: Big Data analytics, mobile & gaming applications, content
distribution…

## S3 Standard – Infrequent Access (IA)

* Suitable for data that is less frequently accessed, but requires rapid
access when needed
* 99.9% Availability
* Lower cost compared to Amazon S3 Standard, but retrieval fee
* Sustain 2 concurrent facility failures
* Use Cases: As a data store for disaster recovery, backups…

### S3 Intelligent-Tiering

* 99.9% Availability
* Same low latency and high throughput performance of S3 Standard
* Cost-optimized by automatically moving objects between two access
tiers based on changing access patterns:
* Frequent access
* Infrequent access
* Resilient against events that impact an entire Availability Zone

### S3 One Zone - Infrequent Access (IA)

* Same as IA but data is stored in a single AZ
* 99.5% Availability
* Low latency and high throughput performance
* Lower cost compared to S3-IA (by 20%)
* Use Cases: Storing secondary backup copies of on-premise data, or
storing data you can recreate

### Amazon Glacier & Glacier Deep Archive

* Low cost object storage (in GB/month) meant for archiving / backup
* Data is retained for the longer term (years)
* Various retrieval options of time + fees for retrieval:
* Amazon Glacier – cheap:
 Expedited (1 to 5 minutes)
* Standard (3 to 5 hours)
* Bulk (5 to 12 hours)
* Amazon Glacier Deep Archive – cheapest:
* Standard (12 hours)
* Bulk (48 hours)

## Snowball

* Physical data transport solution that helps
moving TBs or PBs of data in or out of
AWS
* Alternative to moving data over the
network (and paying network fees)
* Pay per data transfer job
* Use cases: large data cloud migrations, DC
decommission, disaster recovery
* If it takes more than a week to transfer
over the network, use Snowball devices!

## Databases & Analytics

### Databases

* Storing data on disk (EFS, EBS, EC2 Instance Store, S3) can have its limits
* Sometimes, you want to store data in a database…
* You can structure the data
* You build indexes to efficiently query / search through the data
* You define relationships between your datasets
* Databases are optimized for a purpose and come with different
features, shapes and constraints

### Relational Databases

* Looks just like Excel spreadsheets, with links between them!
* Can use the SQL language to perform queries / lookups

### NoSQL Databases

* NoSQL = non-SQL = non relational databases
* NoSQL databases are purpose built for specific data models and have
flexible schemas for building modern applications.
* Benefits:
    * Flexibility: easy to evolve data model
    * Scalability: designed to scale-out by using distributed clusters
    * High-performance: optimized for a specific data model
    * Highly functional: types optimized for the data model
    8 Examples: Key-value, document, graph, in-memory, search databases

### AWS RDS Overview

* RDS stands for Relational Database Service
* It’s a managed DB service for DB use SQL as a query language.
* It allows you to create databases in the cloud that are managed by AWS
    * Postgres
    * MySQL
    * MariaDB
    * Oracle
    * Microsoft SQL Server
    * Aurora (AWS Proprietary database)

### Advantage over using RDS versus deploying DB on EC2

* RDS is a managed service:
* Automated provisioning, OS patching
* Continuous backups and restore to specific timestamp (Point in Time Restore)!
* Monitoring dashboards
* Read replicas for improved read performance
* Multi AZ setup for DR (Disaster Recovery)
* Maintenance windows for upgrades
* Scaling capability (vertical and horizontal)
* Storage backed by EBS (gp2 or io1)
* BUT you can’t SSH into your instances

![RDS](img/rds.png?raw=true "Title")

### Amazon Aurora

* Aurora is a proprietary technology from AWS (not open sourced)
* PostgreSQL and MySQL are both supported as Aurora DB
* Aurora is “AWS cloud optimized” and claims 5x performance improvement
over MySQL on RDS, over 3x the performance of Postgres on RDS
* Aurora storage automatically grows in increments of 10GB, up to 64 TB.
* Aurora costs more than RDS (20% more) – but is more efficient
* Not in the free tier

### Amazon ElastiCache Overview
* The same way RDS is to get managed Relational Databases…
* ElastiCache is to get managed Redis or Memcached
* Caches are in-memory databases with high performance, low latency
* Helps reduce load off databases for read intensive workloads
* AWS takes care of OS maintenance / patching, optimizations, setup,
configuration, monitoring, failure recovery and backups

![RDS](img/elasticache.png?raw=true "Title")

### DynamoDB

* Fully Managed Highly available with replication across 3 AZ
* NoSQL database - not a relational database
* Scales to massive workloads, distributed “serverless” database
* Millions of requests per seconds, trillions of row, 100s of TB of storage
* Fast and consistent in performance
* Single-digit millisecond latency – low latency retrieval
* Integrated with IAM for security, authorization and administration
* Low cost and auto scaling capabilities

### Redshift Overview

* Redshift is based on PostgreSQL, but it’s not used for OLTP
* It’s OLAP – online analytical processing (analytics and data warehousing)
* Load data once every hour, not every second
* 10x better performance than other data warehouses, scale to PBs of data
* Columnar storage of data (instead of row based)
* Massively Parallel Query Execution (MPP), highly available
* Pay as you go based on the instances provisioned
* Has a SQL interface for performing the queries
* BI tools such as AWS Quicksight or Tableau integrate with it

### Amazon EMR

* EMR stands for “Elastic MapReduce”
* EMR helps creating Hadoop clusters (Big Data) to analyze and process
vast amount of data
* The clusters can be made of hundreds of EC2 instances
* Also supports Apache Spark, HBase, Presto, Flink…
* EMR takes care of all the provisioning and configuration
* Auto-scaling and integrated with Spot instances
* Use cases: data processing, machine learning, web indexing, big data…

### Athena Overview

* Fully Serverless database with SQL capabilities
* Used to query data in S3
* Pay per query
* Output results back to S3
* Secured through IAM
* Use Case: one-time SQL queries, serverless queries on S3, log analytics

### AWS Glue

* Managed extract, transform, and load (ETL) service
* Useful to prepare and transform data for analytics
* Fully serverless service

![RDS](img/glue.png?raw=true "Title")

### DMS – Database Migration Service

* Quickly and securely migrate databases
to AWS, resilient, self healing
* The source database remains available
during the migration
* Supports:
    * Homogeneous migrations: ex Oracle to
    Oracle
    * Heterogeneous migrations: ex Microsoft
    SQL Server to Aurora


### Databases & Analytics Summary in AWS

```
Relational Databases - OLTP: RDS & Aurora (SQL)
In-memory Database: ElastiCache
Key/Value Database: DynamoDB (serverless)
Warehouse - OLAP: Redshift (SQL)
Hadoop Cluster: EMR
Athena: query data on Amazon S3 (serverless & SQL)
Glue: Managed ETL (Extract Transform Load) and Data Catalog service
Database Migration: DMS
```

## Other Compute Services: ECS, Lambda, Batch, Lightsail

### What is Docker?

* Docker is a software development platform to deploy apps
* Apps are packaged in containers that can be run on any OS
* Apps run the same, regardless of where they’re run
    * Any machine
    * No compatibility issues
    * Predictable behavior
    * Less work
    * Easier to maintain and deploy
    * Works with any language, any OS, any technology
* Scale containers up and down very quickly (seconds)
* Docker is ”sort of” a virtualization technology, but not exactly
* Resources are shared with the host => many containers on one server

### ECS

* ECS = Elastic Container Service
* Launch Docker containers on AWS
* You must provision & maintain the infrastructure (the EC2 instances)
* AWS takes care of starting / stopping containers
* Has integrations with the Application Load Balancer

### Fargate

* Launch Docker containers on AWS
* You do not provision the infrastructure (no EC2 instances to manage) – simpler!
* Serverless offering
* AWS just runs containers for you based on the CPU / RAM you need

### What’s serverless?

* Serverless is a new paradigm in which the developers don’t have to manage servers anymore…
* They just deploy code
* They just deploy… functions !

### Benefits of AWS Lambda
* Easy Pricing:
* Pay per request and compute time
* Free tier of 1,000,000 AWS Lambda requests and 400,000 GBs of compute time
* Integrated with the whole AWS suite of services
* Event-Driven: functions get invoked by AWS when needed
* Integrated with many programming languages
* Easy monitoring through AWS CloudWatch
* Easy to get more resources per functions (up to 3GB of RAM!)
* Increasing RAM will also improve CPU and network!

### AWS Batch
* Fully managed batch processing at any scale
* Efficiently run 100,000s of computing batch jobs on AWS
* A “batch” job is a job with a start and an end (opposed to continuous)
* Batch will dynamically launch EC2 instances or Spot Instances
* AWS Batch provisions the right amount of compute / memory
* You submit or schedule batch jobs and AWS Batch does the rest!
* Batch jobs are defined as Docker images and run on ECS
* Helpful for cost optimizations and focusing less on the infrastructure

### Batch vs Lambda
* Lambda:
    * Time limit
    * Limited runtimes
    * Limited temporary disk space
    * Serverless
* Batch:
    * No time limit
    * Any runtime as long as it’s packaged as a Docker image
    * Rely on EBS / instance store for disk space
    * Relies on EC2 (can be managed by AWS)

### Amazon Lightsail

* Virtual servers, storage, databases, and networking
* Low & predictable pricing
* Simpler alternative to using EC2, RDS, ELB, EBS, Route 53…
* Great for people with little cloud experience!
* Can setup notifications and monitoring of your Lightsail resources
* Use cases:
* Simple web applications (has templates for LAMP, Nginx, MEAN, Node.js…)
* Websites (templates for WordPress, Magento, Plesk, Joomla)
* Dev / Test environment
* Has high availability but no auto-scaling, limited AWS integrations

## Deploying and Managing Infrastructure at Scale Section

### CloudFormation

* CloudFormation is a declarative way of outlining your AWS
Infrastructure, for any resources (most of them are supported).
* For example, within a CloudFormation template, you say:
* I want a security group
* I want two EC2 instances using this security group
* I want an S3 bucket
* I want a load balancer (ELB) in front of these machines
* Then CloudFormation creates those for you, in the right order, with the
exact configuration that you specify.
* Infrastructure as code
    * No resources are manually created, which is excellent for control
    * Changes to the infrastructure are reviewed through code

### AWS Elastic Beanstalk Overview

* Elastic Beanstalk is a developer centric view of deploying
an application on AWS
* It uses all the component’s we’ve seen before:
EC2, ASG, ELB, RDS, etc…
* But it’s all in one view that’s easy to make sense of!
* We still have full control over the configuration
* Beanstalk = Platform as a Service (PaaS)
* Beanstalk is free but you pay for the underlying instances

### AWS CodeDeploy

* We want to deploy our application
automatically
* Works with EC2 Instances
* Works with On-Premises Servers
* Hybrid service
* Servers / Instances must be provisioned and configured ahead of time with the CodeDeploy Agent

### AWS Systems Manager (SSM)

* Helps you manage your EC2 and On-Premises systems at scale
* Another Hybrid AWS service
* Get operational insights about the state of your infrastructure
* Suite of 10+ products
* Most important features are:
* Patching automation for enhanced compliance
* Run commands across an entire fleet of servers
* Store parameter configuration with the SSM Parameter Store
* Works for both Windows and Linux OS

## Global Infrastructure Section

### Amazon Route 53 Overview

* Route53 is a Managed DNS (Domain Name System)
* DNS is a collection of rules and records which helps clients understand
how to reach a server through URLs.
* In AWS, the most common records are:
* www.google.com => 12.34.56.78 == A record (IPv4)
* www.google.com => 2001:0db8:85a3:0000:0000:8a2e:0370:7334 == AAAA IPv6
* search.google.com => www.google.com == CNAME: hostname to hostname
* example.com => AWS resource == Alias (ex: ELB, CloudFront, S3, RDS, etc…)

### AWS CloudFront

* Content Delivery Network (CDN)
* Improves read performance, content is cached at the edge
* Improves users experience
* 216 Point of Presence globally (edge locations)
* DDoS protection (because worldwide), integration with Shield, AWS Web Application Firewall

### CloudFront – Origins
* S3 bucket
    * For distributing files and caching them at the edge
    * Enhanced security with CloudFront Origin Access Identity (OAI)
    * CloudFront can be used as an ingress (to upload files to S3)

* Custom Origin (HTTP)
    * Application Load Balancer
    * EC2 instance
    * S3 website (must first enable the bucket as a static S3 website)
    * Any HTTP backend you want

### CloudFront vs S3 Cross Region Replication

* CloudFront:
    * Global Edge network
    * Files are cached for a TTL (maybe a day)
    * Great for static content that must be available everywhere
* S3 Cross Region Replication:
    * Must be setup for each region you want replication to happen
    * Files are updated in near real-time
    * Read only
    * Great for dynamic content that needs to be available at low-latency in few regions

### AWS Global Accelerator

* Improve global application availability and performance using the AWS global network
* Leverage the AWS internal network to optimize the route to your application (60% improvement)
* 2 Anycast IP are created for your application and traffic is sent through
Edge Locations
* The Edge locations send the traffic to your application

### Amazon SQS – Standard Queue

* Oldest AWS offering (over 10 years old)
* Fully managed service (~serverless), use to decouple applications
* Scales from 1 message per second to 10,000s per second
* Default retention of messages: 4 days, maximum of 14 days
* No limit to how many messages can be in the queue
* Messages are deleted after they’re read by consumers
* Low latency (<10 ms on publish and receive)
* Consumers share the work to read messages & scale horizontally

### Amazon SNS

* The “event publishers” only sends message to one SNS topic
* As many “event subscribers” as we want to listen to the SNS topic notifications
* Each subscriber to the topic will get all the messages
* Up to 10,000,000 subscriptions per topic, 100,000 topics limit
* SNS Subscribers can be:
    * HTTP / HTTPS (with delivery retries – how many times)
    * Emails, SMS messages, Mobile Notifications
    * SQS queues (fan-out pattern), Lambda Functions (write-your-own integration)
    
## Cloud Monitoring Section

### Amazon CloudWatch Metrics

* CloudWatch provides metrics for every services in AWS
* Metric is a variable to monitor (CPUUtilization, NetworkIn…)
* Metrics have timestamps
* Can create CloudWatch dashboards of metrics

### Important Metrics

* EC2 instances: CPU Utilization, Status Checks, Network (not RAM)
* Default metrics every 5 minutes
* Option for Detailed Monitoring ($$$): metrics every 1 minute
* EBS volumes: Disk Read/Writes
* S3 buckets: BucketSizeBytes, NumberOfObjects, AllRequests
* Billing: Total Estimated Charge (only in us-east-1)
* Service Limits: how much you’ve been using a service API
* Custom metrics: push your own metrics