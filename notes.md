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
### RDS & Aurora

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

## Security & Compliance

### Shared responsibility model
- AWS is responsible for security of the cloud -> hardware, software, networking, and facilities that run AWS services
- Customer is responsible for security in the cloud -> data, identity, access management, platform, applications, and network configuration

### AWS Shield
- AWS Shield is a managed DDoS protection service that safeguards applications running on AWS
- DDoS protection
- Standard: protection against most common DDoS attacks
- Advanced: protection against more sophisticated attacks
- exam keywords: DDoS protection

### AWS WAF - Web Application Firewall
- Protects web applications from common web exploits
- Filter specific requests based on rules
- Rules can be based on IP addresses, HTTP headers, HTTP body, or URI strings
- exam keywords: WAF, web application firewall, protect web applications

### AWS Network Firewall
- Managed firewall service that makes it easy to deploy essential network protections for all of your Amazon Virtual Private Clouds (VPCs)
- From Layer 3 to Layer 7 protection
- exam keywords: protect entire VPC, network firewall

### AWS Firewall Manager
- Manage security rules in all accounts of an AWS Organization
- exam: manage VPC security groups on multiple accounts in an organisation --> AWS Firewall Manager
- Security policy: common set of security rules:
    - VPC Security Groups for EC2, ALB, RDS, ElastiCache, etc.
    - WAF rules for API Gateway, CloudFront, App Load Balancer
    - AWS Shield Advanced for DDoS protection
    - AWS Network Firewall for VPCs

### Penetration Testing
- AWS customers are allowed to perform penetration testing on their AWS infrastructure within certain limits
- DDOS testing other attacks that can harm the AWS infrastructure are not allowed

### Encryption in rest vs in transit
- Encryption in rest: data is encrypted when it is stored (data is not moving)
- Encryption in transit: data is encrypted when it is moving from one place to another (eg data moving from EC2 to S3)

### Encryption with KMS
- AWS Key Management Service (KMS) is a managed service that makes it easy for you to create and control the encryption keys used to encrypt your data
- AWS manages the encryption keys for you, you define the policies
- type of KMS keys: 
    - Customer Managed Keys: you create and manage the keys
    - AWS Managed Keys: AWS creates and manages the keys (aws/s3, aws/ebs)
    - AWS Owned Keys: Collection of CMKs (Customer Master Keys) that an AWS service owns and manages to use in multiple accounts
    - CloudHSM Keys: keys are stored in a hardware security module (CloudHSM)
- exam keywords: KMS, encryption, key management service

### CloudHSM
- CloudHSM is a cloud-based hardware security module (HSM) that enables you to easily generate and use your own encryption keys on the AWS Cloud
- you manage the encryption keys entirely
- exam keywords: CloudHSM, hardware security module, encryption keys

#### KMS vs CloudHSM
- KMS: AWS manages the software for encryption, pay per use
- CloudHSM: AWS provisions encryption hardware, dedicated hardware, pay per hour

### AWS Certificate Manager (ACM)
- AWS Certificate Manager is a service that lets you easily provision, manage, and deploy public and private Secure Sockets Layer/Transport Layer Security (SSL/TLS) certificates for use with AWS services and your internal connected resources

### AWS Secrets Manager
- AWS Secrets Manager helps you protect access to your applications, services, and IT resources without the upfront investment and on-going maintenance costs of operating your own infrastructure
- Integration with Amazon RDS
- Possibility to rotate secrets automatically
- exam keywords: Secrets Manager, rotate secrets, RDS secrets

### AWS Artifact
- AWS Artifact is your go-to, central resource for compliance-related information that matters to you
- eg. PCI DSS, HIPAA, ISO, SOC, etc.
- exam keywords: compliance, AWS Artifact

### AWS GuardDuty
- AWS GuardDuty is a threat detection service that continuously monitors for malicious activity and unauthorized behavior to protect your AWS accounts and workloads
- uses Machine Learning to detect anomalies
- input data: VPC Flow Logs, CloudTrail Logs, DNS Logs
- exam tip: can protect against CryptoCurrency attacks
- exam keywords: GuardDuty, threat detection, malicious activity

### Amazon Inspector
- Amazon Inspector is an automated security assessment service that helps improve the security and compliance of applications deployed on AWS
- For EC2 instances: 
    - leveraging the AWS System Manager (SSM) agent
    - Analyze against unintended network accessibility, vulnerabilities, and deviations from best practices
    - analyze the running OS against known vulnerabilities
- For container image push to Amazon ECR:
    - assesment of the container image as they are pushed
- for Lambda functions:
    - assesment of the Lambda function code and package dependencies as it is deployed
- Reporting & integration with AWS Security Hub
- send findings to Amazon Event bridge
- exam keywords: Amazon Inspector, security assessment, compliance

### AWS Config
- AWS Config is a service that enables you to assess, audit, and evaluate the configurations of your AWS resources
- Helps with auditing and recording compliance of your AWS resources based on the configurations you have set
- Helpful for big enterprises to make sure all resources are compliant with the company's security policies
- exam keywords: AWS Config, compliance, audit

### Amazon Macie
- Amazon Macie is a security service that uses machine learning to automatically discover, classify, and protect sensitive data in AWS
- Macie helps and alerts you to sensitive data such as personally identifiable information (PII)
- can be integrated with Amazon EventBridge
- exam keywords: Macie, sensitive data, PII

### AWS Security Hub
- Central security tool to manage security across multiple AWS accounts and automate security checks
- Integrated dashboards showing current security and compliance status to quickly take actions
- Automatically aggregate alerts in predefined or personal findings format from various AWS serivces & AWS partner tools:
    - Config
    - GuardDuty
    - Inspector
    - Macie
    - IAM Access Analyzer
    - AWS Systems Manager
    - AWS Firewall Manager
    - AWS Health
- must enable AWS Config Service to use Security Hub
- exam keywords: Security Hub, security checks, compliance

### Amazon Detective
- GuardDuty, Macie and Security Hub are great tools to detect security issues, but they do not provide a full investigation
- Amazon Detective is a service that helps you to investigate and identify the root cause of potential security issues or suspicious activities
- automatically collects and process events from VPC Flow Logs, CloudTrail, GuardDuty to create a visual graph of the resources and the interactions between them. So you can easily identify the root cause of the issue.
- exam keywords: Detective, investigate, root cause

### AWS Abuse
- AWS Abuse is a service that helps you to report any abuse of the AWS services
- eg. phishing, malware, spam, DoS or DDoS etc. that is hosted on AWS
- exam keywords: AWS Abuse, report abuse

### Root user privileges
- Root user has full access to all AWS services and resources in the account
- Some actions can only be performed by the root user: 
    - `change account settings( account name, email, root user password, root user access keys)`
    - `close the account`
    - `change or cancel AWS support plan`
    - restore IAM user permissions
    - view certain tax invoices
    - `register as a seller in the Reserved Instance Marketplace`
    - Configure and Amazon S3 bucket to enable MFA
    - edit or delete an Amazon S3 bucket policy that includes an invalid VPC ID or VPC endopoint ID
    - sign up for GovCloud

### IAM Access Aanlyzer
- IAM Access Analyzer helps identify which resources are shared externally: 
    - S3 Buckets
    - KMS Keys
    - IAM Roles
    - Lambda Functions
    - SQS Queues
    - Secrets Manager Secrets
- Define Zone of Trust = AWS account or AWS Organization
- Access outiside zone of trust is flagged as a finding
- exam keywords: IAM Access Analyzer, shared resources, Zone of Trust, analyze access

## 18 Account Management, Billing & Support
### 1 AWS Organizations
- AWS Organizations helps you centrally manage and govern your environment as you grow and scale your AWS resources
- Organize accounts into Organizational Units (OUs): 
    - OUs can contain other OUs
    - OUs can contain accounts
    - eg. dev, test, prod, finance,
- Main account is the master account 
- Apply service control policies (SCPs) to OUs
- Consolidated billing across all accounts
- Benefits: 
    - Centralized management of multiple AWS accounts
    - Cost savings through consolidated billing
    - Fine-grained control over access, security, and compliance: SCPs
    - Automation of account creation and management: through API
    - exam tip: Organizations is used to manage multiple AWS accounts
- exam keywords: Organizations, OUs, SCPs, consolidated billing

#### A. Multi account strategies
- Single Account: 
    - simple, easy to manage
    - no isolation between environments
    - no cost separation
- Multi Account:
    - separate accounts for dev, test, prod
    - isolation between environments
    - cost separation
    - more complex to manage

#### B. SCPs
- Service Control Policies (SCPs) are a type of organization policy that you can use to manage permissions in your organization
- applied to OUs
- SCPs are applied to all accounts in the OU
- SCPs are used to restrict permissions (eg. deny access to S3) or to allow permissions (eg. allow access to EC2)
- JSON based policies like IAM policies
- exam keywords: SCPs, Service Control Policies, organization policy

#### C. Consolidated billing
- Consolidated billing is a feature that enables you to consolidate payment for multiple AWS accounts within your organization by designating one of the accounts as the payer account
- Benefits: 
    - volume pricing: combined usage for all accounts
    - easy tracking of charges: one bill
    - easy to allocate costs: cost allocation tags
    - exam tip: consolidated billing is used to consolidate billing across multiple accounts

### AWS Control Tower
- Easy way to se up and govern a secure and compliant multi-account AWS environment based on best practices
- Benefits: 
    - set up a secure multi-account environment
    - automate the setup of accounts
    - centrally manage security and compliance
    - reduce the time to set up new accounts
    - exam keywords: Control Tower, multi-account, secure environment
- AWS Control Tower runs on top of AWS Organizations: it automatically sets up AWS Organizations and implements the SCPs (Service Control Policies) for you
- exam keywords: Automated multi-account setup, best practices, security, compliance

### AWS Resource Access Manager (RAM)
- Share AWS resources that you own with other AWS accounts
- Share with any account or within your organization
- Avoid resource duplication
- Supported resources: Aurora, VPC Subnets, Transit Gateway Route 53, EC2 Dedicated Hosts, License Manager, etc.

### AWS Service Catalog
- Users that are new to AWS have too many options and may create stacks that are not compliant with company policies
- AWS Service Catalog allows you to create and manage catalogs of IT services that are approved for use on AWS
- Users can launch only the products that are approved by the IT department
- The products are CloudFormation templates
- Use IAM permissions to control access to the products
- exam keywords: Service Catalog, IT services, approved products

### Pricing models in AWS
- Pay as you go: 
    - pay for what you use
    - no upfront cost
    - no long-term commitment
- Save when you reserve:
    - commit to a specific instance configuration
    - pay upfront or pay partially upfront
    - 1 year or 3 year term
    - significant discount compared to on-demand
- Pay less by using more:
    - volume discounts
    - tiered pricing
- Pay less as AWS grows:
    - AWS lowers prices over time
    - AWS passes the savings to customers

#### Free services
- IAM
- VPC
- Consolidated billing
- Elastic Beanstalk (*)
- CloudFormation (*)
- Auto Scaling Groups (*)
(*) you pay for the resources that are created by these services
- Free tier: 
    - 12 months free: 750 hours of EC2, 5GB of S3, 25GB of DynamoDB
    - Always free: 1M Lambda requests, 1M free requests on API Gateway, 25GB of EBS

#### EC2 pricing
- On-demand instances:
    - minimum of 60s
    - pay per second after the first minute (Linux/Windows) or per hour (other)
    - no long-term commitment
- Reserved instances:
    - 1 year or 3 year term
    - significant discount compared to on-demand
    - pay upfront or pay partially upfront
    - convertible reserved instances: change the instance type
    - scheduled reserved instances: launch within time window
- Spot instances:
    - bid for unused EC2 capacity
    - can be terminated by AWS with 2 minutes notice
    - great for batch jobs, big data analysis, etc.
- Dedicated hosts:
    - physical server with EC2 instance capacity fully dedicated to your use
    - can help you reduce costs by allowing you to use your existing server-bound software licenses
    - can be purchased On-Demand (hourly)
    - can be purchased as a Reservation for up to 70% off the On-Demand price
- Savings plans: future lecture

#### Lambda and ECS
- Lambda: 
    - pay per call
    - pay per duration
    - free tier: 1M free requests per month, 400,000 GB-seconds of compute time per month
- ECS:
    - EC2 Launch Type Model: No additional fees, you pay for AWS resources stored and created in you application

- Fargate Launch Type Model: pay for vCPU and memory used by the containers

#### Storage pricing - S3
Pricing depends on:
- Storage class: 
    - S3 Standard: general purpose storage of frequently accessed data
    - S3 Infrequent Access (IA): long-lived, but less frequently accessed data
    - S3 One Zone-IA: long-lived, infrequently accessed, non-critical data
    - S3 Intelligent Tiering: designed to optimize costs by automatically moving data to the most cost-effective access tier
    - S3 Glacier: long-term archive
    - S3 Glacier Deep Archive: lowest cost storage class for long-term retention and digital preservation
- Number and size of objects: Price can be tiered (base on volume)
- Number and type of requests
- Data transfer OUT of S3 region (IN is free)
- Transfer acceleration: fast, easy, and secure transfers of files over long distances between your client and an S3 bucket
- Lifecycle transitions: move objects to different storage classes

Similar pricing model for EFS pay per use, has infrequent access & lifecycle rules

#### Storage pricing - EBS
Pricing depends on:
- Type of volume: 
    - General Purpose SSD (gp2)
    - Provisioned IOPS SSD (io1)
    - Throughput Optimized HDD (st1)
    - Cold HDD (sc1)
    - Magnetic (standard)
- Size of volume
- IOPS:
    - Generl purupose SSD: included
    - Provisioned IOPS SSD: you pay for the IOPS provisioned
    - Magnetic: number or requests
- Snapshots: incremental backups of EBS volumes:
    - Added data cost per GB per month
- Data transfer:
    - Outbound data transfer are tiered for volume discounts
    - Inbound data transfer is free

#### Pricing for RDS
- per hour billing
- Database charateristics:
    - Engine
    - Size
    - Memory class
- Purhcase type:
    - On-demand
    - Reserved (1 year or 3 year term)
- Backup storage: There is no additional charge for backup storage up to 100% of your total database storage for a region
- Additional storage: you pay for the storage you provision
- Number of input and output requests per month
- Deployment type: Single-AZ or Multi-AZ
- Data transfer: Outbound data transfer are tiered for volume discounts, Inbound data transfer is free

#### Content Delivery Network (CDN) - CloudFront
- Pricing is different accross different regions
- Aggregated for each edge location, then applied to your bill
- Data Transfer out (volume discount)
- Number of HTTP/HTTPS requests

#### Networking costs in AWS per GB - Simplified
- Free for traffic into Availability Zones
- Free for traffic between EC2 instances in the same Availability Zone
- Traffic between 2 EC2 instances in different Availability Zones: 
    - $0.01 per GB using private IP
    - $0.02 per GB using public IP / Elastic IP
- Traffic between 2 EC2 instances in different regions: $0.02 per GB inter region data transfer

### AWS Savings plan
- AWS Savings Plans is a flexible pricing model that offers low prices on EC2 and Fargate usage, in exchange for a commitment to a consistent amount of usage (measured in $/hour) for a 1 or 3 year term
- Easiest way to setup long-term commitments on AWS
- 2 types of Savings Plans:
    - Compute Savings Plans: 
        - up to 66% discount compared to on-demand
        - regardless of family, region, size, OS, tenacy or compute options
        - compute options: EC2, Fargate, Lambda
    - EC2 Instance Savings Plans: 
        - up to 72% discount compared to on-demand
        - commit to usage of individual instance families in a region (eg. C5 or M5 instances in US West)
        - regardless of AZ, size (eg. M5.2xlarge), OS or tenacy
        - All upfront, partial upfront, no upfront
- Machine Learling Savings Plans: Sagemaker
- Setup from the AWS Cost Explorer console

### AWS Compute Optimizer
- AWS Compute Optimizer is a service that recommends optimal AWS resources for your workloads to reduce costs and improve performance by using machine learning
- Analyzes resource configurations and CloudWatch metrics and uses machine learning to recommend optimal resources
- supported resources: EC2 instances, Auto Scaling Groups, ECS tasks, Lambda functions, RDS databases

### Billing and Costing Tools
- Estitmate costs in the cloud:
    - AWS Pricing Calculator
- Tracking costs in the cloud:
    - Billing Dashboard
    - Cost Explorer
    - Cost Allocation Tags
    - Cost and Usage Reports
- Monitoring agains cost plans:
    - Billing Alarms
    - Budgets







