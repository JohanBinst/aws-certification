# AWS Cloud practinioner notes

## 1. Cloud computing

Different types of cloud computing

## IAM - Identity and Access Management

### Definitions
root user
IAM Users:
IAM User Groups:
IAM Policies
IAM Roles

### IAM Best practices

### Shared responsibilty model

## 2. EC2 - Elastic Compute Cloud

## 3. Storage for EC2 Instance

### EBS

### EFS

## 4. ELB & ASG - Elastic Load Balancing & Auto Scaling Groups

## 5. Amazon S3

## 6. Databases & Analytics

### RDS (Relational Database Service)
- [RDS](https://aws.amazon.com/rds/) - Managed relational database service that supports multiple database engines: MySQL, PostgreSQL, MariaDB, Oracle, SQL Server, and Aurora
- suited for OLTP workloads: Online Transaction Processing

### RDS Deployments options
#### 1. Read replicas
- scale the read workload of your DB (in the same AZ)
- can create oup to 15 read replicas
- data is only written to the main DB

#### 2. Multi-AZ
- failover DB in cas of AZ outage (high availability)
- data is only read & written to the main database
- can only have 1 other AZ as failover, failover is used only when main is down


#### 3. Multi-Region (Read replicas)
- Disater recovery in cas of region issue
- local performance for global reads (application reads in db replica of nearest AZ)
- write is done in main DB (1 AZ)
- replication cost


### Amazon Elasticache

ElastiCache is to get managed Redis or Memcached in-memory databases with high performance and low latency.
--> Helps to reduce the load of databases (RDS DB: Postgres, or other) for read intensive workloads by storing cache in in-memory database

insert schema architecture

### DynamoDB
keywords: serverless, low latency

- Fully managed highly available with replication across 3 AZ
- NoSQL database -> not a relational database -> stores primary key and product pairs (cfr key value)
- scales to massive worklaods because it is a distributes serverless database (no instances of the db are required)
- millions of requests per sections, trillions of rows, 100s of TB of storage
- single digit millisecond latency - low latency retrieval

DynamoDB is a flagship product of AWS

#### DynamoDB Global Tables
DynamoDB Global Tables makes DynamoDB table accessible with low latency in multiple-regions by using Active-Active replciation
2-way replication --> users can read and write in any table specific to the AZ

insert schema architecture

### DynamoDB Accelerator - DAX
- same as Elasticache but for `DynamoDB` only: in-memory cache for DynamoDB only
- 10x performance improvement

### DAX
- Amazon DynamoDB Accelerator (DAX) is a fully managed, highly available, in-memory cache for Amazon DynamoDB that delivers up to a 10 times performance improvement—from milliseconds to microseconds—even at millions of requests per second.

### Redshift
- [Redshift](https://aws.amazon.com/redshift/) - Fully managed, petabyte-scale data warehouse service and analytics tool.
- data is stored in colnmar format (columns instead of rows)
- exam keywords: analytics, data warehouse, colunmar, OLAP
- OLAP (Online Analytical Processing) is used for complex queries and data analysis

#### Redshift serverless
- [Redshift serverless](https://aws.amazon.com/redshift/serverless/) - Serverless data warehouse that automatically scales the datawarehouse based on the workload.
- pay only for compute and storage used during analysis -> very cost efficient to run Redshift
- use cases: reporting, dashboards, real-time analytics

### Amazon EMR (Elastic MapReduce)
- [Amazon EMR](https://aws.amazon.com/emr/) - helps creating Hadoop clusters to analyze and process large amounts of data (Big Data)
- cluster can be made up of EC2 instances and EMR takes care of the provisioning and configuration of the cluster
- automatically scales the cluster based on the workload
- supports Apache Spark, HBasem Presto, Flink, and other big data frameworks
- exam keywords: Hadoop clusters, Big Data, data processing

### Amazon Athena

- [Amazon Athena](https://aws.amazon.com/athena/) - serverless query service that makes it easy to analyze data in Amazon S3 using standard SQL
- S3 objects supported are CSV, JSON, ORC, Avro, and Parquet (built on Presto)
- no need to set up or manage any infrastructure
- use cases: Business intelligence, analytics, reportingm ELB Logs, CloudTrail Logs, VPC Flow Logs
- Amazon QuickSight can be used to visualize the data
- pricing: $5 per TB of data scanned
- cost saving: use compressed or columnar data formats(Parquet, ORC) to reduce the amount of data scanned

exam keywords: analyze data in S3, serverless, SQL

### Amazon QuickSight

- [Amazon QuickSight](https://aws.amazon.com/quicksight/) - Serverless machine learning-powered Business Intelligence tool that allows you to create interactive dashboards and reports
- integrates with AWS services like RDS, Redshift, Athena, Aurora and S3
- pay per session or per user
- exam keywords: Business Intelligence, dashboards, reports, machine learning

### Neptune
- [Neptune](https://aws.amazon.com/neptune/) - Fully managed graph database service that supports both RDF and property graph models
- use cases: social networking, fraud detection, recommendation engines, network security, knowledge graphs (Wikipedia)
- exam keywords: graph database, RDF, property graph
- build and rund applications working with highly connected datasets - optimized for these complex and hard querries
- highly available with replication across 3 AZs

### TimeStream
- [TimeStream](https://aws.amazon.com/timestream/) - Fully managed, serverless, time-series database service for IoT and operational applications
- optimized for IoT and operational applications
- store and analyze trillions of events per day at 1/10th the cost of relational databases
- exam keywords: time-series data, IoT, operational applications

### QLDB
- [QLDB](https://aws.amazon.com/qldb/) - Fully managed ledger database that provides a transparent, immutable, and cryptographically verifiable transaction log
- Quantun Ledger Database
- A ledger is a record of (financial) transactions
- immutable system: no entry can be removed or modified
- cryptographically verifiable: you can verify the integrity of the data -> because of the cryptographic hash of the data after each transaction
- difference with Amazon Managed Blockchain: QLDB is a ledger database, not a blockchain and it is not decentralized (all data is stored at AWS) -> in accordance with financial regulations
- manipulate data using PartiQL (SQL-compatible query language)
- 2-3x faster than common ledger blockchain frameworks
- exam keywords: ledger database, financial transactions, (immutable, cryptographically verifiable)

### Managed Blockchain
- [Managed Blockchain](https://aws.amazon.com/managed-blockchain/) - Create and manage scalable blockchain networks using popular open-source frameworks: Hyperledger Fabric and Ethereum
- join public blockhain networks or create your own private blockchain networks
- exam keywords: blockchain, Hyperledger Fabric, Ethereum

### Glue
- [Glue](https://aws.amazon.com/glue/) - Fully managed extract, transform, and load (ETL) service that makes it easy to prepare and load your data for analytics
- fully serverless
- exam keywords: ETL, extract, transform, load
- use case example: EXTRACT data from S3 and RDS -> TRANSFORM data with Glue script -> LOAD data into Redshift

#### Glue Data Catalog
- [Glue Data Catalog](https://aws.amazon.com/glue/features/catalog/) - Fully managed metadata repository that makes it easy to discover, search, and query metadata across your data lake and data warehouse
- catalog of datasets in AWS structure
- can be used with Athena, Redshift, EMR, and other services to build schemas for data
- probably not on exam

### DMS (Database Migration Service)
- [DMS](https://aws.amazon.com/dms/) - Migrate your databases to AWS with minimal downtime
- supports homogeneous migrations (Oracle to Oracle) and heterogeneous migrations (Microsoft SQL to Aurora)
- Quickly and securly migrate databases to AWS
- Source database remains available during the migration
- exam keywords: database migration


### Overview
- Relational Databases: RDS and Aurora
  - Difference between multi-AZ, read replicas, multi-region
- In-memory Database: ElastiCache
- Key/Value Database: DynamoDB (serverless) & DAX (cache for DynamoDB) if cache is needed
- Data Warehouse or OLAP: Redshift(SQL)
- Hadoop Cluster: EMR
- Athena: query data on Amazon S3 (serverless & SQL)
- Quicksight: dashboards and visualization of data (serverless)
- DocumentDB: "Aurora of MongoDB" (JSON type of datasets - NoSQL database)
- Amazon QLDB: Financial transactions ledger (immutable journal, cryptographically verifiable): centralized!
- Amazon Managed Blockchain: managed Hyperledger Fabric and Ethereum blockchains
- Glue: Managed ETL (Extract, Transform, Load) and Data Catalog service
- DMS: Database Migration Service
- Neptune: Graph database
- TimeStream: Time-series database

## Other compute services: ECS, lambda, Batch and Lightsail

### ECS (Elastic Container Service)
- [ECS](https://aws.amazon.com/ecs/) - Highly scalable, high-performance container orchestration service that supports Docker containers
- ECS is a container management service that makes it easy to run, stop, and manage Docker containers on a cluster
- You must provision the infrastructure (EC2 instances) that run the containers

### Fargate
- [Fargate](https://aws.amazon.com/fargate/) - Serverless compute engine for containers that works with both ECS and EKS
- With Fargate, you no longer have to provision, configure, or scale clusters of virtual machines to run containers --> fully serverless

### ECR (Elastic Container Registry)
- [ECR](https://aws.amazon.com/ecr/) - Fully managed Docker container registry that makes it easy to store, manage, and deploy Docker container images
- Private Docker container registry on AWS

### Lambda
- [Lambda](https://aws.amazon.com/lambda/) - Serverless compute service that lets you run code without provisioning or managing servers
- Lambda runs your code only when needed and scales automatically
- Functions are triggered by events -> event driven : S3 upload, DynamoDB update, API Gateway request
- Pioneer of serverless computing on AWS
- Supports multiple programming languages: Node.js, Python, Ruby, Java, Go, .NET
- Pricing:
  - pay per request (number of invocations)
  - compute time (GB-seconds) = memory in GB provisioned * total runtime in seconds
- Easy monitoring with CloudWatch Logs
- use cases:
  - create thumbnails from images uploaded to S3
  - run serverless CRON jobs
- exam keywords: serverless, event-driven, functions

### API Gateway
- [API Gateway](https://aws.amazon.com/api-gateway/) - Fully managed service that makes it easy for developers to create, publish, maintain, monitor, and secure APIs at any scale
- Create serverless RESTful APIs and WebSocket APIs
- Integrates with Lambda, DynamoDB, and other AWS services
- Proxies requests from endpoint to other services. Eg: Allow users to upload files to S3 or access data in DynamoDB or trigger Lambda functions from HTTP requests
- exam keywords: serverless RESTful APIs, WebSocket APIs

### Batch
- [Batch](https://aws.amazon.com/batch/) - Fully managed batch processing at any scale
- Is not serverless, relies on EC2 instances
- Batch computing is the processing of a large amount of data in a programmatic way

#### Batch vs. Lambda
- Lambda is serverless, Batch is not
- Lambda is event-driven, Batch is not
- Lambda has limited runtime (15 minutes), Batch can run for hours or days
- Lambda has limited storage (512MB), Batch can use EBS volumes
- Lambda is for small, short-lived functions, Batch is for long-running batch jobs

### Lightsail
- [Lightsail](https://aws.amazon.com/lightsail/) - Virtual private server (VPS) service that offers everything needed to build an application or website
- For people with no cloud experience
- low and predictable pricing
- use cases:
  - simple websites: Wordpress, Joomla, Drupal
  - Dev/Test environments
  - simple webapps: has templates for MEAN, LAMP, Nginx, Node.js

### Overview
- ECS: Run Docker containers on EC2 instances (not serverless)
- Fargate: Serverless compute engine for containers
- ECR: Docker container registry for storing, managing, and deploying Docker container images
- Lambda: Serverless compute service
- API Gateway: Serverless RESTful APIs
- Batch: Run batch jobs on AWS using EC2 instances (not serverless)
- Lightsail: Virtual private server (VPS) service

## Deployments

### CloudFormation
- [CloudFormation](https://aws.amazon.com/cloudformation/) - Infrastructure as Code (IaC) service that helps you model and set up your AWS resources so you can spend less time managing those resources and more time focusing on your applications
- CloudFormation templates are written in YAML or JSON
- exam keywords: Infrastructure as Code, templates, YAML, JSON

### Elastic Beanstalk
- [Elastic Beanstalk](https://aws.amazon.com/elasticbeanstalk/) - Platform as a Service (PaaS) that allows you to deploy and manage web applications and services
- Supports multiple programming languages: Java, .NET, PHP, Node.js, Python, Ruby, Go, Docker
- You upload your code and Elastic Beanstalk automatically handles the deployment, from capacity provisioning, load balancing, and auto-scaling to application health monitoring
- exam keywords: PaaS, multiple programming languages

### CodeDeploy
- [CodeDeploy](https://aws.amazon.com/codedeploy/) - Automates code deployments to any instance, including Amazon EC2 instances and instances running on-premises
- exam keywords: code deployments, hybrid(On-premises and AWS)

### Systems Manager (SSM)
- [Systems Manager](https://aws.amazon.com/systems-manager/) - Gives you visibility and control of your infrastructure on AWS
- Patch, configure and run commands at scale (at multiple instances at the same time)
- exam keywords: patching, configuration, automation

#### SSM Session Manager
- [SSM Session Manager](https://aws.amazon.com/systems-manager/features/#Session_Manager) - Provides a secure and auditable instance management
- No need for SSH keys, bastion hosts, or open inbound ports
- exam keywords: secure, auditable, instance management

#### SSM Parameter Store
- [SSM Parameter Store](https://aws.amazon.com/systems-manager/features/#Parameter_Store) - Securely store configuration data and secrets
- exam keywords: secure, configuration, secrets

## Developer services
### CodeCommit
- [CodeCommit](https://aws.amazon.com/codecommit/) - Fully managed source control service that makes it easy for teams to host secure and highly scalable private Git repositories
- exam keywords: source control, Git
- No longer supported in the future

### CodeBuild
- [CodeBuild](https://aws.amazon.com/codebuild/) - Fully managed build service that compiles source code, runs tests, and produces software packages that are ready to deploy
- exam keywords: build service, compile, tests

### CodePipeline
- [CodePipeline](https://aws.amazon.com/codepipeline/) - Continuous integration and continuous delivery (CI/CD) service for fast and reliable application and infrastructure updates
- from code commit to build to deployment
- exam keywords: CI/CD, continuous integration, continuous delivery
