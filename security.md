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
