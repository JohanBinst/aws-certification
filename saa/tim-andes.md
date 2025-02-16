# Adrian Cantrill's AWS Certified Solutions Architect - Associate (SAA-C03) Course


# INTRODUCTION & SCENARIO

# Public Introduction - No Notes

# Course Resources
Course has GitHub Repository: https://github.com/acantril/aws-sa-associate-saac03
Walked through how to d/l Git to PC and clone repo for access.
To update to latest version: "git pull"

Walked through and recommended VS Studio Code install

# Site Tools & Features

## Quick tour of the learning platform
Products page, Slack channel, free GitHub repo: "Labs" link, mini projects in the GH repo, "More" tab for tech support

# AWS Exams / Certifications

## How to get started
Don't start with the Cloud Practitioner Foundational Cert, start with Associate level SA (Solutions Architect). The content overlaps.
After you finish SA Associate do the Role Based certs, then Specialty certs later. Get SA Professional prior to Specialties certs
- In Associate level, start with 1. SA before SysOps/Developer 2. then Developer Associate 3. then SysOps Associate (Hardest exam of the 3).
- In Professional level, tests are way harder. Longer questions, more questions. 1. Professional SA, 2. DevOps Pro exam

# Scenario - Animals4life

Animal rescue/awareness Org. Global company, 100 staff, 100 remote staff, etc etc. Small data-center is old, and data should be migrated out.
Badly implemented AWS trial in SYD Region. Isolated Azure/GCP Pilots. All staff uses this infrastructure. Company runs lean but will get new tech
if it helps business.
- On Premise: 192.168.10.0/24, Class C
- AWS Pilot: 10.0.0.0/16, Class B
- Azure Pilot: 172.31.0.0/16, Class B
Major offices NY, Seattle, London all use Head Office services for data
Field workers on laptop, 3g/4g/ satellite for email/files, chat/planning, research data

## Problems: Hardware failing, datacenter decommissioned in 18months, so business needs to migrate out. New investment needed, not sure if on premise, azure, aws, etc. Previous AWS/Azure attempts didn't pan out. Distance to datacenter is sub-optimal for much of company. Lean/appropriately sized, but trouble with peak traffic. IT team sucks at cloud.

## Ideal Outcomes:
- Fast performance for all field workers
- Able to deploy into new regions quickly when required
- Low cost and scalable base infrastructure, cost close to 0 as possible while meeting reqs
- Agility - new marketing campaigns, social and progressive applications (IOT, Big Data, etc). Wants to make use of emerging technologies
- Automation - low base staffing costs

## Pay attention to which areas need more information, so you can ask the right questions.

# Connect with other students and your instructor - techstudyslack.com. Make sure you meet people in the industry--50% of jobs aren't posted anywhere.
- No better way to learn tech than help others

# Course upgrades: If you've already bought a course but want a bundle, you'll just have to pay the difference.


# COURSE FUNDAMENTALS AND AWS ACCOUNTS

## AWS Accounts
AWS Accounts are not only required to use AWS services, they are also one of the most important tools available to a solutions architect.
Many students confuse accounts with users inside the accounts. An org may use one account or many thousands. Bigger orgs generally use multiple AWS accounts.

At a high level, AWS Account is a container for Identities (users) (which you log in with) and Resources (which you provision).

When creating an AWS account you need to provide:
- Unique email address (for EACH AWS account); this creates a special type of identity: the account root user
- Provide a payment method, generally a Credit Card (No need to spend: You can choose a Free tier and create a zero-spend budget)

Root Users can only access their own accounts. Initially, it is also the only user. Root user has full control over the one specific AWS account and any resources inside it. Root user CANNOT be restricted in any way. Protect the root username and password.

### Billing
Credit Card used to open account is the Account Payment Method. Any billable usage is charged to this CC. "Pay-as-you-go" platform. There is a free tier which we use in this course.

### Security
You can create restricted identities/users using Identity and Access Management (IAM): Users, Groups, and Roles can also be created and given FULL or LIMITED permissions. All of these ID's start off with NO access/permissions in the account. The IAM service is Account specific. Cross-account permissions are a possibility, as well (to be covered later).

### Boundary of the Account
AWS accounts are really good at containing what's inside the accounts; bad employee or bad actor, etc. Having separate AWS accounts for different uses (DEV, PROD, etc), you can limit overall damage.

By default, all access to an AWS account is denied except for the root user.

### TIP: Create new accounts for the course, don't use existing AWS accounts. The longer an AWS account exists, the more potential for configuration errors.


## DEMO: Creating the GENERAL AWS Account: https://learn.cantrill.io/courses/1820301/lectures/41301459
1. Create General AWS account (*MANAGEMENT). This account's root user will be what we log in with (root user = account specific).
2. Add root user MFA for security.
3. Create a Budget to protect against unintended costs.
4. Create an IAM user, IAMADMIN. Give permissions. Then we'll use this ID for the course.
5. Create a second accound, Production. Will also have IAMADMIN user.

## TIP: using one email for multiple accounts with Gmail. AWS accounts should be viewed as disposable, create as many as you need. Create a new account for each course.
### TIP Example: email is catguy@gmail.com. You can use + sign in email address to create 'unique' email addresses. Ex: catguy+AWSAccount1@gmail.com, catguy+AWSAccount2@gmail.com, etc etc. This is called a Dynamic Alias.

Choose free tier AWS account after providing all account setup info (unique email, CC, verification.

Complete the prompted steps. Account will now be created.

### Account
- Always a good idea to update Alternate Contacts
- IAM User and Role Access to Billing Information, click "Edit", check Activate IAM Access
-- If this IAM box isn't checked, even an IAM ID will full admin permissions wouldn't be able to access the billing console

### Multi-Factor Authentication (MFA)
- Username and PW is step one
- MFA makes things more secure with OTP

Definition: Factors - Different pieces of evidence which prove identity

4 Common Factors:
- Knowledge (username / PW)
- Possession (debit card, MFA device, MFA app, etc)
- Inherent - Something you are: fingerprint, biometrics, etc.
- Location - Physical location, which network (corp or wifi)

More factors means more security and harder to fake. Also means less convenient. We're trying to strike a balance between security and convenience.

With AWS: 1. first, username and PW 2. MFA OTP (physical MFA or virtual via app ie. Google Authenticator)

To Activate MFA for a specific ID, like Root user, you activate MFA for that user. AWS generates secret key and other associated information (user it links to, service). All this information use all this information together to generate a QR code. Scan code using MFA app

### Securing an AWS Account
Attach MFA device to Root user.

In AWS Console... Account > Security Credentials to IAM console > locate "Assign MFA Device", follow steps.
- Log Out and test MFA login.

#### REMEMBER: When setting up a new AWS account / Identity, you need to add another entry within your OTP application.

By end of this course, you should have a total of 4 virtual MFA's configured.

### Creating a Budget
Understand Free Tier and set up a budget.

AWS Free Tier: https://aws.amazon.com/free/
- Details allocations of free resources

Spend Details: Account > Billing Dashboard > click "Bills" (for spend details)

Billing Notification Preferences: Click "Billing Preferences" > check all boxes within "Invoice delivery preferences" and "Alert preferences" and Update

Create Cost Budgets: click "Budgets" > select Use a Template > select an appropriate option based on monthly spend budget (select Zero spend budget) > Budget Name "Monthly Zero Budget", enter Email Recipients for alerts ([EMAIL]+trainingawsgeneral@gmail.com) > click "Create Budget"
-- Budgets allow you to monitor spend and configure alerts when hitting spend targets

### Creating the Production Account
After creating General AWS account, we now need to create multiple AWS accounts and connect them with an AWS Organization.

#### Create Production AWS Account
Steps:
1. First, decide on email address to use [EMAIL]+trainingawsproduction1@gmail.com
2. Credit Card
3. Support Plan (Free Tier)
4. Secure AWS account with MFA to Root user of Production Account
5. Billing Preferences, check the boxes, adding email address for alerts
6. Create budget (Zero Spend Template)
7. Enable IAM User & Role Access to Billing (in Accounts)
8. Optional: Update alternate contacts in Account

### IAM (Identity and Access Management) Basics
We first need to understand the identity situation. Accounts created have Root user will have full access. AWS account and Root user can be thought of as the same thing.

Generally, you want to give access to other people in the companies, but with restricted access -- ONLY GIVE THEM PERMISSIONS REQUIRED TO DO A JOB, called "Least Priveleged Access".

EXAM: IAM is a GLOBALLY RESILIENT service, so any data is always secure across all AWS regions.

Any IAM's in an account are completely separate from any other accounts. IAM as a service can do as much as the Root user if given all permissions, exception being some billing stuff (but that can be activated).

Inside IAM, you can create multiple identities.

IAM let's you create 3 types of identity objects:
- User
- Group
- Role

Users: Humans or applications that need access to your AWS account. An application that does backups of the account may also be an IAM user.

Group: Collections of related users. All dev team users, finance, HR, etc.

Roles: Can be used by AWS Services or if you want to grant external access to your account. Used to grant access to services in your account to an uncertain number of entities. Eg. If you want all EC2 instances in your account to access the Simple Storage Service (S3), you can create a role which grants access and allow instances to use that role.

TIP: ROLES should be used when the number of entities needing access is *uncertain*.

### IAM Policy or Policy Document
Objects or documents to be used to Allow or Deny access to AWS services, only when attached to users, groups, or roles.

### High Level IAM
IAM has 3 main jobs:
1. IDP (ID Provider): Manages identities
2. Authentication Process: Authenticates identities (when anyone makes request to AWS, they're known as a Security Principle--they must prove their identity)
3. Authorization: Allowed or Denied access to resources. This is based on Policies associated with the identity that is authenticated with.

### Other IAM Key Points
- No cost for IAM
- Global service / Global Resilience (copes with failure of large parts of the AWS system)
- IAM only controls what its identities can do. Allow or Deny identities in account
- No direct control on external accounts or users. It only controls local accounts or users
- Identity federation (to be covered later) and MFA

Next, we'll create an IAM account with full permissions to take the place of the Root user. Root users should generally only be used to create an account. Afterward, best practice is to utilize an IAM User rather than account root user. We'll use this IAM user to create new identities with less permissions (only enough for the user to do a certain task)

## DEMO Adding an IAM Admin to GENERAL ACCOUNT
Set up AIM ID with Admin permissions

Search "IAM" > IAM Dashboard

To sign on with IAM identities, use sign-in URL: http://[account-id].signin.aws.amazon.com/console.
-- To make friendlier URL, set alias.

### To set alias, make it globablly unique.
1. Within IAM Dashboard, find right-side AWS Account info, find "Account Alias", click "Create".
- Must be a globablly unique ID. I am using "ta-cantrill-training-aws-general"
-- Now URL is https://ta-cantrill-training-aws-general.signin.aws.amazon.com/console

### Create IAM Admin ID
IAM Dashboard > left sidebar "Users" > Create user "iamadmin"
- Give Access to Console
- Create an IAM user (2nd option, 1st option to be covered later)
- Custom PW
- Give admin permissions "Attach policies directly" > check "AdministratorAccess"
- Create user
- Test login
- Confirm login with profile dropdown that will show account name
- Secure admin account with OTP > Security Credentials > Assign MFA
- Log out and test OTP

## DEMO Adding an IAM Admin to PRODUCTION ACCOUNT
Same as previous section.

## IAM Access Keys
Access AWS via command line or APIs. This is done using IAM access keys.

### IAM Access Keys
- long term credential (don't change or rotate regularly)
- IAM user has 1 username and 1 PW (cannot have more than 1). Password on IAM user is actually optional.
- Credential Leak: If someone knows your username (public) and password (private)
- Unlike username/PW, IAM user can have TWO access keys
- Access key actions: create, delete, made inactive, made active. Default: Active state
- Access keys are formed from two parts:
1) Access Key ID
2) Secret Access Key
--AWS provides both when key is created.
- Once the key is generated, you CANNOT access the Secret Access Key part again
- If leaked/lost, you need to delete ID and Secret Access Key and recreate completely
- If made inactive or deleted, CLI will stop working until re-active or new key is created
- Rotating Access Keys: delete old one make new one and replace old one
- NOT recommended: Don't give Root user Access Keys
- IAM Roles DO NOT use access keys

## DEMO Creating Access Keys and Setting Up AWS CLI v2 Tools

Once logged in with Admin user:
IAM Dropdown > Security Credentials > scroll down to "Create Access Key", click > Command Line Interface (CLI) > check box at bottom > Next > Set Decription Tag > "Create Access Key"

Once Access Key is created, you can use Actions dropdown to Deactivate, Activate, and Delete. If you ever lose access to a key, you need to deactivate & delete it, then create a new one.

### Download AWS CLI v2
AWS CLI v2 (Windows) Installation - https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2-windows.html

AWS CLI v2 (macOS) Installation - https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2-mac.html

AWS CLI v2 (Linux) Installation - https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2-linux.html

### Configure CLI
Configure a set of credentials which CLI will use to communicate with AWS. We will use the General IAMADMIN user for this one.

COMMAND: 'aws configure': configures default profile for CLI
COMMAND: 'aws configure --profile iamadmin-general' / 'aws configure --profile iamadmin-production': named profile for CLI

Upon entering the above Command:
- AWS Access Key ID
- AWS Secret Key
- Default Region Name: us-east-1
- Default output format (press Enter with blank field for default)

Test that this is successful with COMMAND 'aws s3 ls --profile [CLI profile name]'. This will error first as we need to specify named profile:
'aws s3 ls --profile iamadmin-general', which will currently return a blank string as there are no s3 buckets.

#### Configure for Production
COMMAND: 'aws configure --profile iamadmin-production'
COMMAND to test: 'aws s3 ls --profile iamadmin-production'

SECURITY REMINDER: Never share your SECRET KEY. If leaked, delete and create new set of keys and re-configure in CLI

TIP: If after you Configure CLI with credentials, you can delete the credential files (CSVs)


## AWS FUNDAMENTALS

### AWS Public VS Private Services
Architecture of both Public/Private Services. "Private"/"Public" refer to networking only. Private runs within VPC, Public is S3
- Both require Permissions / Configuration
3 Zones:
- 1. Public Internet Zone
- 2. AWS Private Zone: VPC's are Virtual Private Clouds. VPCs are isolated unless configured otherwise; can attach IGW (internet gateway) for access to internet
- 3. AWS Public Zone (runs between Public and Private zones). It's a network connected to the Public internet

#### AWS Public Service: What is true of an AWS Public Service? 1. Located in the AWS Public Zone 2. Anyone can connect, but permissions are required to access the service
#### AWS Private Service: What is true of an AWS Private Service? 1. Located in a VPC 2. Accessibly from the VPC it is located in 3. Accessible from other VPCs or on-premise networks as long as private networking is configured


### AWS Global Infrastructure
AWS have created a global public cloud platform which consists of isolated 'regions' connected together by high speed global networking.

Two types of Deployment at global level: 1) AWS Regions, 2) AWS Edge Locations (doesn't directly map to continent or country)
#### AWS Region: Geographically spread. Full compute, storage, DB, AI, Analytics
-- Three main benefits
--- 1. Geographically separate for physical reslience. Isolated Fault Domain
--- 2. Geopolitical Separation. Different governance
--- 3. Location Control. Performance
-- Inside regions: You can use Region Code or Region Name. Eg Sygney Australia. RC: ap-southeast-2, RN: Asia Pacific (Sydney)

#### AWS Availability Zone (AZ)
AZ's are located inside regions. Eg. for Sydney AU: ap-southeast-2a, ap-southeast-2b, ap-southeast-2c. If an issue is only in 1 availability zone (AZ), you'll still have functioning services in the other AZs

#### AWS Edge Location: Local distribution points closest to user. Content distribution services, edge computing. Eg. Netflix storing content close as possible to user. Edge locations for fast/efficient data transfer because they're closer to the user. Uses CloudFront

#### AWS AZ VS Edge Location
An Availability Zone is an isolated location within an AWS region. An edge location delivers cached content to the closest location to reduce latency for users.

NOTE: Visit: infrastructure.aws

Service Resilience
- Globally Resilient: Operates globally with a single DB and replicated across multiple regions. World would need to fail to experience a full outage here. Eg. IAM
- Regionally Resilient: Operate in single region with one dataset in a region. Replicate data to AZs for resilience.
- Availability Zone Resilient: Prone to failure as they have less redundancies.

### AWS Default Virtual Private Cloud (VPC)
A Virtual Network inside AWS. VPCs are regional services; regionally resilient. They operate from multiple AZ's in a region.
- A VPC is 1 account and 1 region, cann't be spread across multiple accounts/regions
- Private and isolated unless configured otherwise
- Default VPC (max 1 per region, pre-configured) and Custom VPCs (can have many)
- Can be used to connect AWS private networks to on-premise network. Or connecting during multi-cloud deployments

EXAM: VPCs are REGIONALLY resilient

#### Default VPC
There can only be one default VPC per region, and they can be deleted and recreated from the console UI. Unless configured otherwise, VPC is entirely private/isolated.
- VPC CIDR: Start and end range of IP addresses VPC can use. If anything needs (and is allowed to) communicate with VPC, it needs to communicate to the VPC CIDR
- Default VPC only gets 1 CIDR IP range. Can't change it.
- Default VPC provides Internet Gateway (IGW), Security Group, and NACL
- VPC can be subdivided into subnetworks. Each subnet in VPC is located in one AZ. Default VPC has one subnet in each AZ by default
-- Each subnet uses part of the VPC CIDR range
-- Default VPC CIDR: always 172.31.0.0/16
-- Assigns public IPv4 addresses
--- /20 subnet in each AZ in the region. The higher the /#, the smaller the network. /17 is half the size of /16

QUIZ: How many subnets are in a default VPC? Default VPCs always have the same IP range and same '1 subnet per AZ' architecture. # Subnets = # AZ's in region

EXAM: Default VPC CIDR IP? 172.31.0.0/16

##### Default VPC - Create / Delete

To Locate: AWS Dashboard > Search "VPC" > Your VPCs

To Delete: check Default VPC > actions dropdown "Delete" > follow prompt

To Create Default VPC: If you've deleted Default VPC. In Your VPCs > Actions dropdown > Create Default VPC

### Elastic Compute Cloud (EC2) Basics
Basically the default compute service of AWS. It allows you to provision Virtual Machines known as Instances with resources you select and an operating system of your choosing.
- EC2 is IaaS, Infrastructure-as-a-service. Unit of consumption is the Instance. Instance is a configured O/S
- Private service by default, uses VPC networking
- Public access must be configured. The VPC it's running within must support Public access (if using custom VPC, you need to configure this in VPC)
- EC2 is AZ Resilient
- When launching an Instance, you can choose size and capability
- On-Demand Billing, by second or hour
- Storage Types: Local on-host storage, or network storage via Elastic Block Store (EBS)
- By default, AWS has a [soft] limit of 20 instances per region

EXAM: EC2 is AVAILABILITY ZONE resilient

#### EC2 instance has attribute called State
States to Know: Running, Stopped, Terminated
- When instance is launched and provisioned, it moves to Running. If instance is shut down, it is Stopped
- Instance can be terminated, but this cannot be reversed

These States influence the charges for an instance.
- Stopped instance uses less resources, therefore less expensive. You won't be charged for "running" the instance
- Regardless of Running or Stopped, storage is still allocated and you'll still be charged for EBS storage even if instance is stopped
- To guarantee 0 cost on instance, you must Terminate. Termination is irreversible

#### Components for instance charge: running the instance, storage the instance uses, extras for any commercial software the instance is launched with

#### AMI: Amazon Machine Image
Image of an EC2 instance
- Can create EC2 instance
- Can be created FROM an EC2 instance

##### AMI contains attached permissions. Controls which accts can/can't use AMI:
- Public Type - Everyone allowed
- Owner - Implicit Allow
- Explicit - Allow specific AWS accounts

##### AMI includes the following:
- One or more Amazon Elastic Block Store (Amazon EBS) snapshots, or, for instance-store-backed AMIs, a template for the root volume of the instance (for example, an operating system, an application server, and applications).
- Launch permissions that control which AWS accounts can use the AMI to launch instances.
- A block device mapping that specifies the volumes to attach to the instance when it's launched.

##### NOT stored in AMI:
- Instance Settings
- Network Settings

EXAM: What is NOT stored in an AMI? Instance and Network Settings

Root Volume: AMI contains boot volume of instance, boots O/S

Block Device Mapping: Config that links volumes that AMI has and how they're presented to O/S. Ie. Which is boot volume, which is data volume

#### Connecting to EC2:
- Connect to Windows instances using RDP (Remote Desktop Protocol), port 3389
- Connect to Linux distros use SSH protocol, port 22. Log in using SSH key pair

### DEMO: Create an EC2 Instance
https://learn.cantrill.io/courses/1820301/lectures/41301621
1. Create SSH Key Pair: Navigate to EC2 Console (search bar) > left sidebar > Network & Security > Key Pairs) > click "Create Key Pair"
- Note: For creating key pair, Private key file format choises are .pem and .ppk. For MacOS/Linux, always use .pem, if using modern Windows you can choose .pem. Older Windows or Putty terminal app, choose .ppk
2. Configure: Left sidebar "Instances" > click "Launch Instances" > select O/S (Amazon Linux) > select keypair login (A4L) > Network Settings: select Create Security Group > name/description "MyFirstInstanceSG" > leave Inbound security groups rules as defaults > Launch EC2 Instance

### DEMO: Connect to Terminal of an EC2 Instance
1. In EC2 Dashboard, Right Click your EC2 instance, select "Connect" > SSH Client
2. Open your local Terminal / Command Prompt and change directories to wherever your SSH private file key is (likely Downloads, it's a .pem file created previously)
3. Copy the command at the bottom of the SSH Client tab "ssh -i "A4L.pem" ec2-user@ec2-54-89-175-122.compute-1.amazonaws.com", verify fingerprint with "yes"
- Note: If using MacOS/Linux and "Permission Denied": paste in terminal "chmod 400 A4L.pem"
- More key file permissions help: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/connection-prereqs.html#connection-prereqs-private-key

### S3 Basics: Simple Storage Service
Global Storage Platform - regional based/resilient. Access from anywhere.
- Public service, can cope with unlimited data & multi-users
- Perfect for hosting large amounts of data
- Economical and accessed via UI/CLI/API/HTTP

#### S3 Delivers 2 things: Objects and Buckets

##### S3 Objects
What is an Object? An object is a file and any optional metadata that describes the file.

Two components and some associated metadata:
1. Object Key. identifies object in a bucket
2. Value. data or contents of the object. Object size can range from 0 bytes to 5 terabytes (TB) in size.
Metadata: Version ID, Metadata, access control, subresources

NOTE: S3 = Default Storage Service in AWS

##### S3 Buckets (Simple Storage Service)
Containers created in a specific AWS region; default place to go to in order to configure S3
- Data inside a bucket has a primary home region. Never leaves this region unless configured to do so
- Blast radius of a failure is limited to a region
- Buckets can hold an unlimited number of objects; infinitely scalable
- S3 bucket has no complex structure; flat-structure; everything stored at same level; all stored at Root level (if you list out on Command, it'll look like there are folders, but there aren't Eg. /old/photo1.jpg). Folders are called 'prefixes' in S3.


# EXAM: Bucket name must be Globally Unique. Error where you can't create a bucket? Prolly not a unique name

# EXAM: More bucket name restrictions: 3-63 characters, all lowercase, no underscores, not formatted like IP addresses

# EXAM: Bucket limits: soft limit of 100 buckets per AWS account, hard limit of 1000 buckets (hard limit increased by connecting with Support). If you have more than 1000 users, you can't use 1 bucket per user, but you can use prefixes within a bucket to let multiple users use one bucket.

#### EXAM: Unlimited Objects in a bucket, ranging from 0 bytes to 5TB in size

#### EXAM: Object Structure: Key = Name, Value = Data

#### S3 Patterns and Anti-Patterns
- S3 is an Object Store system, NOT File System and NOT Block System
- S3 has no File System, it's flat. It's not Block storage, so you can't mount it as K:\ or /images
- Great for 'offload'
- S3 should be your default INPUT and/or OUTPUT to MANY AWS products

#### EXAM: Where to store data in AWS? S3 should be default answer

#### QUIZ: What is true of Simple Storage Service (S3)
- S3 is an AWS Public Service
- S3 is an Object Storage System
- Buckets can store an unlimited amount of data

### DEMO: Creating an S3 Bucket
Create, interact with bucket, upload to bucket, interact with uploaded objects
- As S3 is Global, you can't select a Region in advance

STEPS: Move to S3 Console > click 'Create bucket' > name 'koalacampaign987654123' (must be globally unique) > select Region (default N.VA) > untick "Block *all* Public Access (this just enables you to Enable public access later) > click "Create Bucket"

#### Amazon Resource Name (ARN): All resources in AWS have a unique identifier, the ARN.
To see bucket ARN, Amazon S3 > Buckets > click the bucket you want > 'Properties' tab > Amazon Resource Name

#### DEMO: Upload files to Bucket
Amazon S3 > Buckets > click the bucket you want > Objects, click Upload > Select Files > Use default settings > click Upload
- Now, you'll see these files in the Object tab

Note on creating a folder: it doesn't actually create a folder, it creates an object that appears to be a folder. They are just emulated using prefixes Eg. archive/koalazzz.jpg -> Not actually a file, but named to look like it
- Without versioning enabled, same name files can overwrite each other. With Versioning, they can't

#### DEMO: Delete Buckets in S3
Two step process:
1. Empty the bucket > select Bucket, click Empty
2. Re-select Bucket, click Delete

### CloudFormation (CFN) Basics
A tool which lets you create, update, delete infrastructure in AWS using Templates
- At its base, CFN uses templates. Can create/update/delete templates
- Template written in YAML or JSON

From the Documentation: AWS CloudFormation is a service that helps you model and set up your AWS resources so that you can spend less time managing those resources and more time focusing on your applications that run in AWS. You create a template that describes all the AWS resources that you want (like Amazon EC2 instances or Amazon RDS DB instances), and CloudFormation takes care of provisioning and configuring those resources for you

#### What makes a template? Components:
- All templates have a list of resources. This is the only mandatory item
- Description. Free text field for the author to provide details on template. (If you have AWSTemplateFormatVersion, Description MUST follow it in YAML/JSON
- Metadata. Can control the UI (groupings, order, labels, descriptions), as well as other things (to be covered later)
- Parameters. Value parameters, default values, etc.
- Mappings. Create lookup tables.
- Conditions. Allows decision making in the template. Step 1 create condition, Step 2 use condition
- Outputs. Once template is finished it can present outputs like admin or setup adddress, instance ID

#### How does CFN use Templates?
Eg. Template that creates EC2 resource. Resources defined in CFN Templates are called Logical Resources.
- When template is given to CFN, CFN creates a stack which is a living and active representation of a Template. Stack is created with CFN does something with a template.
- For any logical resources in the stack, CFN makes a corresponding physical resourse in your AWS account. It's CFNs job to keep logical and physical resources in sync. Physical resource: A resource created by creating a CloudFormation Stack
- If you delete a CFN Stack, its logical resources are deleted and CFN subsequently deletes the physical resources

# EXAM: In a CFN Template, if you have the AWSTemplateFormatVersion item, the Description MUST follow directly after in your YAML/JSON template file

### DEMO: Simple Automation w/ CFN; Creating EC2 with CFN

"CloudFormation" or CFN in Search > click "Create Stack" > Template is ready > Upload a Template File > use Demo file (ec2instance.yaml) > click "Next" > Name: "cnfdemo1" > leave the rest default > "Next" > skip config "Next" > Review cfndemo1: Capabilities, check the box
- Template auto-creates an s3 bucket when you upload a Template
- YAML file:
-- LatestAmiID: Instead of giving latest AMI ID, you can make Type a "latest version" AMI
-- CloudFormation Functions are used within YAML Outputs to get values like InstanceID, Availability Zone (AZ), Public IP of EC2, etc. Eg. !Ref, !GetAtt
-- Resources Component is the main one in the file. In this temmplate, an instance role and instance role profile are being created (SessionManagerRole, SessionManagerInstanceProfile) -- covered later.
-- Also being created in the Resources portion of the template: EC2 instance, InstanceSecurityGroup. Port 22 (SSH)/Port 80 (HTTP)
-- Resources: EC2Instance: Properties: InstanceType: "t2.micro" -- Free tier elligible
- After Submitting stack to be created, you'll see that each Resource being created is done so by an Event, "CREATE_IN_PROGRESS", "CREATE_COMPLETE". This whole process takes some time before all of cnfdemo1 is showing CREATE_COMPLETE

#### EC2 Session Manager: EC2 Dashboard > Connect to Instance > Session Manager
- No need to SSH in now
- Two logical resources in YAML template configure this ability


## CloudWatch Basics
CloudWatch is a core supporting service within AWS which provides metric, log and event management services. Collects / manages operational data on your behalf.

### Three jobs:
1. Metrics. AWS Products, Apps, on-premises. Some metrics require extra installed CloudWatch Agent
2. CloudWatch Logs. AWS Products, Apps, on-premises. Almost anything logged can be ingested by Logs
3. CloudWatch Events. AWS Services & Schedules. If an AWS service does something, this will generate an event that can perform another action. Or you can set up a chrono-repeating event through here.

### Core Concepts
- Namespace: Container for monitoring data. There is a naming ruleset for naming. All AWS data foes into a special namespace AWS/[service]
- Metric: Collection of related data points in a time-ordered structure
- Datapoints: A single unit of a metric; consists of timestamp and a value
- Dimensions: Generally, a metric is a collection (Eg. CPU utilization comes from all EC2 instances, not just one). You can use dimensions to single out resources to see their individual metrics. "Separate datapoints for different things or perspectives within the same metric"
- Alarms: Taking actions based on metrics. States: OK or ALARM (ALARM can be SNS Notification or Action), and INSUFFICIENT DATA (when there's not yet enough data)


## DEMO: Monitoring with CloudWatch
https://learn.cantrill.io/courses/1820301/lectures/41301629
1. Create EC2 Instance: Nav to EC2 service > Launch Instance Defaults for all, but you can pay to Enable Detailed CloudWatch Monitoring
2. Create CloudWatch alarm: Nav to CloudWatch dashboard > All Alarms > Create Alarm
3. Select Metric > EC2 > Browse Tab (make sure you know last 4 of Instance ID number) > Last 4 of ID number, check box for CPUUTilization metric
4. Metrics / Contitions: Conditions: Static, Whenever CPU Util is Greater/Equal 15% > "Next" > Remove Notification > Alarm Name "cloudwatchtestHIGHCPU" > Next/Create Alarm
5. Back to EC2, connect to EC2 with Instance Connect
6. Need to install Stress app > command: sudo yum install stress -y
7. Stress Test: command: stress -c 1 -t 3600. Make sure CloudWatch alarm is OK status before entering this command.
8. Clean up: Delete CloudWatch Alarm and Terminate EC2 instance. Delete EC2 Security Group

Detailed CloudWatch Monitoring: Enables you to monitor, collect, and analyze metrics about your instances through Amazon CloudWatch. Additional charges apply if enabled. If no value is specified the value of the source template will still be used. If the template value is not specified then the default API value will be used.


## Shared Responsibility Model
Vendor and User shared responsibilities. This applies from a security perspective so you know which elements you and the vendor manage.
- Customer is responsible for security 'in' the cloud: client-side data encryption, server-side encryption, networking traffic protection, O/S, platform, IAM, apps
- AWS responsible for security 'of' the cloud


## High-Availability (HA) vs Fault-Tolerance (FT) vs Disaster Recovery (DR)
### High-Availablily - Aims to ensure an agreed level of operational performance, usually uptime, for a higher than normal period. Doesn't aim to stop failure, but online and providing services as often as possible. Fix should be as quick as possible, often with automation to bring systems back into service quickly; maximizing a system's online time.
- System availability is in the form of percentage uptime. Three 9's -- Up 99.9% of the time==8.77 hours/year downtime. Five 9's==5.26 minutes/year down time
- Costs required to implement: design decisions and automation
### Fault Tolerance - The property that enables a system to continue operating properly in the event of the failure of some (one or more faults within) of its components. Fault tolerance systems work through failure with no disruption; operating through failure.
- Cost of fault tolerance can be expensive because of redundancies and failure toleration via duplicate system components
- Example: Plane operates with Fault Tolerance (more engines, electronic systems etc); can't tolerate failure in flight
### Disaster Recovery - Post-disaster recovery plan. A set of policies, tools, and procedures to enable recovery or continuation of vital technology infrastructure and systems following a natural or human-induced disaster. When disaster occurs, you want to avoiding losing irreplaceable items.


## IAM Identity Policies
Policies attached to identities in AWS.
1. Understand their architecture 2. Gain ability to read/understand a policy 3. Learn to read/write your own

IAM Policy is a set of security statements to AWS, granting or denying product/features.
- IAM Identity Policy Document: 1 or more statements, created using JSON
-- Statement Id or Sid: Let's you identify a statement and what it does
-- Action: Can be specific individual action, a wild card, or list of multiple independent actions
-- Resources: Wild cards, lists of individual resources (using ARN name)
-- Effect: Allow or Deny

NOTE: Action and Resource within IAM Policy must match for statement to execute.

### How to Handle Overlap Type Situations
Priorities:
1. Explicit DENY: Overrules everything.
2. Explicit ALLOW: Allows access to all actions on any S3 resource (overrules all but Explicit DENY).
3. Default DENY (Implicit): No explicit DENY or ALLOW, so this takes effect. IAM ID's are generally restricted access by default.
- DENY (explicit), ALLOW (explicit), DENY (implicit)

### Three types of Policies
- 1. Inline Policies - JSON policies applied to each IAM account individually. (Manually applying policies to each Identity)
- Managed Policies - Created as their own object. You can attach this policy to more than one identity. Best for Common Access Rights
-- 2. AWS managed or 3. Customer managed
-- Reusable
-- Low Management Overhead
When to use Inline Policies? For Special or exceptional Allows or Deny's


## IAM Users and ARNs (Amazon Resource Name)
### IAM Users: An identity used for anything requiring long-term AWS access eg. Humans, apps, service accounts. If you can picture one thing; named thing, 99% of the time use IAM
- Starts with the principal; an entity trying to access AWS account (ppl, svc, group of  these_
- Authenticate principal. Principal needs to prove identity against IAM (using Username/PW (humans usually) or Access Keys (app or human in CLI))
- Principal becomes Authenticated Identity
- Authorization for actions via IAM Policy (statements)

### ARN (Amazon Resource Name):
Uniquely identify resources within any AWS accounts. ARNs are used in IAM policies and have a defined format

### ARN Format
arn:partition:service:region:account-id:resource-id
arn:partition:service:region:account-id:resource-type/resource-id
arn:partition:service:region:account-id:resource-type:resource-id

Note: s3 is globally unique, so no need to specify region...
arn:aws:s3:::catgifs -> references s3 bucket ITSELF
arn:aws:s3:::catgifs/* -> references objects IN the bucket (thse two ARNs do not overlap)

# EXAM: MAX 5,000 IAM Users per account
# EXAM: IAM User can be a member of 10 groups maximum
System with more than 5,000 identities? Can't use IAM user for each identity. IAM Roles & Identity Federation fixes this (more later)


## DEMO - Simple Identity Permissions Policies in AWS
Assign some permissions to an IAM identity
- 1-click deployment https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/create/review?templateURL=https://learn-cantrill-labs.s3.amazonaws.com/awscoursedemos/0052-aws-mixed-iam-simplepermissions/demo_cfn.yaml&stackName=IAM
-- Create IAM user Sally and two s3 buckets

IAM PW - Min. 8 characters. Uppercase, lowercase, numbers

Steps:
1. open first link, create PW, create stack
2. Login to new IAM Sally with incognito window, change PW, check ec2 and s3 that the permissions are limited
3. Using the lesson's attached .zip, open s3_fulladmin.json and copy the code to clipboard
4. In ADMIN account > IAM dashboard > User: Sally > Permissions > "Add permissions" > Create inline policy > JSON tab, paste copied text > name "s3admininline" and click "Create policy"
5. In s3, you can prove permissions by uploading merlin/thor.jpg through Sally IAM account

### DEMO - Delete all CFN / IAM info above
1. Delete Managed Policy: IAM > Users > Sally > Permissions > remove "AllsAllS3ExceptCats"
2. s3 > select "catpics"/"animalpics" buckets > click "Empty" > type "permanently delete", submit
3. CFN > Stacks > Delete Stack. NOTE: If you don't see this stack, check your region to make sure youre in N.Virginia


## IAM Groups
IAM groups are containers for IAM users. Makes managing IAM users easier.
- Groups can have both Inline and Managed policies attached
- Soft limit: 300 Groups per account (you can get Support to increase this)
- Groups are NOT a True Identity; they can't be referenced as a PRINCIPAL in a policy (you can grant access to users, not groups)
- Can hold Identity Permissions

EXAM: You can't login to IAM Groups; no credentials/login of their own
EXAM: IAM User can be a member of up to 10 IAM Groups (hard limit)
EXAM: AWS Account has a 5,000 IAM user limit (hard limit)
- There is no effective limit for the number of Users in a single IAM Group
EXAM: There is no "All Members" group by default. In IAM, you could create and add all Users to a group
EXAM: Groups CANNOT have nesting. No Groups within Groups
EXAM: Groups are NOT a True Identity; they can't be referenced as a PRINCIPAL in a policy (you can grant access to users, not groups)

Eg. If Sally is a part of 2 IAM Groups, each with an attached policy, and she has an attached policy, she has 3 policies which become Merged Policies
- For figuring out overlapping, combined all policies and tally Allows/Deny's and undergo the same DENY-ALLOW-DENY pattern

### Resource Policy: Controls access to a specific resource, allowing/denying identities to access that bucket. Does this by referencing this ID's with ARNs


## DEMO - Permissions control using IAM Groups
How groups can be used to hold permissions for group members

1. After prep steps complete, remove catpic permissions from Sally IAM > Users > Sally > Permissions > check cat Policy, "Remove"
2. IAM > User Groups > click "Create group" > name "developers" > select policy name "IAMGROUPS-AllowAllS3ExceptCats-7OLPCURC1UQF"
3. IAM > User Groups > tab Users > Add Users > select Sally > Add Users

### IAM Groups DEMO: Tidy Up:
1. IAM > User Groups > Developers > Remove AllowAllS3ExceptCats policy
2. IAM > Users Groups > delete Developers
3. Empy s3 Buckets . s3 > Buckets > click and Empty cat/animals buckets
4. CloudFormation > Stacks > delete IAMGROUPS


## IAM Roles - The Tech
- Principal: Physical person, app, device, or process which wants to Authenticate with AWS.
- IAM User: If you can think of a single entity as a principal, then prolly use IAM User
- IAM Roles: If you don't know the number of principals. Or more than 5,000 principals.
- A Role doesn't represent 'you', it represents a level of access inside an AWS account. Permissions borrowed for a short period of time
- Roles can be referenced within Resource Policies.

### IAM Roles Policies - Two Types
1. Trust Policy - The trust policy specifies which trusted account members are allowed to assume the role.
2. Permissions Policy - The permissions policy grants the user of the role the needed permissions to carry out the intended tasks on the resource.
- Temporary Security Credentials: Given when a Role gets assumed by something that is allowed to assume it. These are like access keys, but time limited.
-- Generated by STS, Secure Token Service. "sts:AssumeRole"
-- Checked against Permissions Policy


## IAM Roles: When to use IAM Roles
Examples for selecting when and when to not use IAM Roles.

- Example 1. Common use of Roles are for AWS Services themselves
-- Eg. AWS Lambda. Lambda function has no permissions by default, so it needs permissions to do things when it runs. Running Lambda Function is called "function invocation"/"function execution". We need to give this function permissions with access keys and there's a better way than hardcoding keys into script. To provide these permissions, we create an IAM Role called "Lambda Execution Role", which has a Trust Policy/Permissions Policy
-- This is good for a role because you'd have to hardcode into the function otherwise (security risk/update issues). Roles provide TSC (Temp security credentials)
-- For a given Lambda Function, you could have 0 to unknown number of copies running. Therefore, it makes sense to be a Role.

- Example 2. Emergency or out-of-the-usual situations
-- Eg. Group Helpdesk team given Read-Only access to a customer's AWS account to watch performance. Anything past read-only handled by a Senior team. However, if a customer calls at a time when Senior team is unavailable, the Helpdesk team may need more than read-only; Break Glass Situation. "Break glass for excepted access".
-- An emergency role can be assumed when Helpdesk user needs to "Break glass for more than read-only access"

- Example 3. Adding AWS to existing corporate environment
-- Eg. You have an existing physical network with an existing identity provider, Microsoft Active Directory. External Accounts / Identities cannot be used to directly access AWS Resources. For a corporate with more than 5,000 staff, you can't assign each employee an IAM (MAX 5000). Roles can re-use IAM Users
-- Allow IAM Role to be assumed by one of the External Entities (the identities in Microsoft Active Directory)
--- When Role is assumed, Temporary Security Credentials are used

TERM: ID Federation: Giving permissions to an external ID provider and allowing externals to assume a Role
TERM: Web Identity Federation. Eg. When you are given the option to login with Google, Facebook, etc (these are Web Identities), then use these to assume an IAM Role for AWS access.
-- Advantages: No AWS credentials on the external entity. Makes use of existing accounts. Scales to hundreds of millions of users and beyond.

EXAM: How you can architect solutions that will work for mobile apps: Use ID Federation
EXAM: External Accounts / External Identities cannot be used to directly access AWS Resources. They must assume a Role to gain access.

### IAM Roles: When to use Roles: Cross-Account Access
Eg. Two AWS accounts. Your Account and Partner Account
- Your account offers an application which processes scientific data and they want you to store data in Partner Account's s3 bucket. Your account has 1000s of ID's and they don't want this data in their account.
- In this situation, use a Role in the Partner Account. Any objects uploaded by this Role into the Partner Account means the Partner Account owns these objects
- Roles can be used cross-account to access individual resources, or access to whole accounts


## Service-linked Roles (SLR) & PassRole (PR)
A service-linked role is a unique type of IAM role that is linked directly to an AWS service. Service-linked roles are predefined by the service and include all the permissions that the service requires to call other AWS services on your behalf. The linked service also defines how you create, modify, and delete a service-linked role. A service might automatically create or delete the role. It might allow you to create, modify, or delete the role as part of a wizard or process in the service. Or it might require that you use IAM to create or delete the role.

### SLR: Key Difference between SLR and normal IAM Roles
- You can't delete a service linked role until it's no longer required / used within that AWS service

### SLR: Permissions needed to create - Policy
Key elements: top statement is Allow, action iam:CreateServiceLinkedRole, resource is NOT guessable--see link below
- https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html

### SLR: Role Separation
One group given ability to create roles, other group gets ability to use the SL Role

### PR: PassRole Permissions
To use pre-existing role with a service without having to create / edit a new role, you need to provide PassRole Permissions.

To pass a role (and its permissions) to an AWS service, a user must have permissions to pass the role to the service. This helps administrators ensure that only approved users can configure a service with a role that grants permissions. To allow a user to pass a role to an AWS service, you must grant the PassRole permission to the user's IAM user, role, or group.
- "Pass the role permissions"
- A method inside AWS that gives you the ability to implement Role Separation
-- An important AWS security architecture


## AWS Organizations
A product that allows larger businesses to manage multiple AWS accounts in a cost-effective way with little to no management overhead

Large orgs need to manage many AWS accounts (100s or more). Without AWS Orgz, these accounts would each have their own pool of IAM users and separate payment methods. Beyond 5-10 accounts, this becomes unwieldy.

### AWS Org - How it's created
First, take a single / standard AWS account (not within an org) and with this create an AWS Organization. The Org isn't created IN the account, you're just using the account to create the AWS Org. This standard AWS account that created the Org then becomes the Management Account for the org (previously Master Account).

Using this management account, you can invite other standard AWS Accounts into the org. As they are existing accounts, they need to approve the Org invites. If they approve, they become part of the Org. Once these Standard Accounts join the Org, they become Member Accounts

### AWS Org - Hierarchy of Containers (which contain Members and other containers)
Structure in AWS Orgs is hierarchical (upside-down tree). Top of hierarchy is Root Container of Organization (not to be confused with Account Root User)--this is a container for AWS Accounts, Mgmt and Member Accounts. This Org Root container also can contain other containers, known as Organizational Units (OU's): can contain AWS accounts or other Organizational Units

#### Types of Accounts relating to AWS Orgs
- Management Account / Master Account. Account that created the AWS Organization and invites Account Members
- Standard Account. A standard AWS account that is not part of an AWS Org
- Member Account. A standard AWS account that joined an AWS Org
NOTE: Only ONE Management Account per AWS Org

### AWS Org - Management Account
- Only ONE Management Account per AWS Org
- Account that creates the Org
- Account that handles Consolidated Billing

#### AWS Org - Consolidated Billing
Consolidated Billing. Eg. AWS Org with 4 accounts: 1 Mgmt and 3 Members that would each have their own billing information. However, since they're in an AWS Org, the individual billing methods are REMOVED for member accounts. Instead, billing is passed through to Management Account of the AWS Org (AKA Payer Account)
- Payer Account - Management Account that contains the payment method for an AWS Organization
- This helps remove Financial Management Overhead
- Bulk discounts; consolidation of reservations and volume discounts

#### AWS Org - Service Control Policies (SCP)
Allows you to restrict what Member Accounts can do.

#### AWS Org - New Account within Org
For new account, you just need a valid, unique email address. This way, there is no invite process (like there is with having pre-existing accounts join an AWS Org).

### AWS Org Changes Best Practice for User Logins / Permissions
With Orgs, you don't need IAM users inside every AWS Account. Instead, use Roles to allow IAM Users to access other accounts.
- Best practice is single account to handle all logins
- Large enterprise may use Identity Federation to pull in on-premise identities for logging in to login account
- Role Switch: Once Member accounts are logged in, they can Role Switch from login account into other Member Accounts

## DEMO - AWS Organizations
Steps:
1. The GENERAL account will become the MANAGEMENT / MASTER account for the organisation
2. We will invite the PRODUCTION account as a MEMBER account and create the DEVELOPMENT account as a MEMBER account.
3. Finally - we will create an OrganizationAccountAccessRole in the production account, and use this role to switch between accounts.

1. Nav to AWS Organization > "Create an Organization"
2. In Incognito Window, log in to the Production Account admin, copy Account ID > back to General AWS Management Account window > "Add an AWS account" > Invite Existing Account > Paste in ID / add message > Send Invitation
3. In Production Admin account > nav to AWS Organizations > Invitations > Accept Invitation
4. Manually adding a Role to an invited account > In Prod account nav to IAM > Roles > Create Role > Type of Entity: AWS Account > get account ID of General AWS Org Account > select Another AWS Account > Paste Account ID > Add Permissions: AdministratorAccess > Next > name "OrganizationAccountAccessRole" > Create Role. In IAM > Roles >  OrganizationAccountAccessRole > Trust Relationships, you'll see the General Account ID referenced as a Trusted Entity
5. Role Switch: From General to Production Account. Copy Production ID > Main Dropdown "Switch Role" > click "Switch Role" > paste Prod ID > name of Role created "OrganizationAccountAccessRole" > Display Name "Prod" > select color Red > Create / Switch Role. You'll see Display name "Prod" on top right menu drop down. You can also SWITCH BACK

6. Create new Account within Org. AWS Orgz > Add Account > Create an AWS Account > name "OrganizationAccountAccessRole" > Create
7. After new Account created, copy its account ID > dropdown Switch Role > switch to DEV role


## Service Control Policies (SCPs)
- A feature of AWS Organizations which allow restrictions to be placed on MEMBER accounts in the form of permissions boundaries. Establish which permissions can be granted in an account.
- SCPs can be applied to the organization, to OU's or to individual accounts
- Member accounts can be effected, the MANAGEMENT account cannot. But, it can indirectly attach to Account Root User
- SCPs DON'T GIVE permission - they just control what an account CAN and CANNOT grant via identity policies
- SCP is a JSON document
- SCPs inherit down the Org tree. Eg. If attached to Root Container, all Org accounts affected. If attached to OU, it affects the OU and all units / members within

TIP: SCPs DON'T GRANT any permissions, they just establish boundaries / limit permissions

### SCP: Allow / Deny Lists
- Allow List. Block by Default and allow certain services
- Deny List. Allow be Default and block certain services (Deny List is Default list, and default policy attached is FullAWSAccess)

To implement Allow Lists, 1. Remove AWS FullAccess Policy, 2. Add Allowed services into a new SCP

Best practice is Deny List for less admin overhead.

### SCP: Identity Policies in Accounts VS SCPs
EXAM: There is an overlap of permissions between these two types of policies. The OVERLAPPED permissions are what are actually active


## DEMO - Using Service Control Policies (SCP)
Update the structure within the organization, add hierarchy (Root, Dev OU, Prod OU) - and apply an SCP to the PRODUCTION account to test their capabilities
- Follows the same DENY-ALLOW-DENY IDP pattern

1. Create OU: Be in Admin account > AWS Organizations > check Root container box, "Actions: Create New" > Org Unit Name "PROD" > Create OU.
2. Create OU: Repeat above for DEV
3. Move relevant accounts to new OUs: check Production account, dropdown "Move" > Select respective OU (PROD/DEV) > Move AWS Account
4. Add SCP to Production Account: Switch Role: PROD > nav to s3 > Create Bucket > name (must be globally unique) "catpics3453451" > region: us-e-1 > upload attached photo (proving we have admin access)
5. Restrict with SCP. Switch Back > AWS Orgz > Policies > click SCP, enable SCP > Create Policy > copy .json text content from lesson file denys3.json > replace JSON with copied text > name "Allow All Except S3" > create policy
6. AWS Orgz > AWS Accounts > click PROD OU > tab "Policies" > Attach Allow All Except S3 Policy
7. Detach FullAWSAccess. AWS Orgz > Account PROD > tab "Policies" > select "attached directly" FullAWSAccess > Detach > Detach Policy
8. We reverted everything back to normal (re-attached Full Access policy to PROD OU, emptied s3 bucket, deleted s3 bucket


## Cloudwatch Logs
- CloudWatch Logs is a public service which can accept logging data, store it and monitor it
- It is often the default place where AWS Services can output their logging
- CloudWatch Logs is a public service and can also be utilised in an on-premises environment and even from other public cloud platforms
- Built-in AWS Service integrations: EC2, VPC Flow Logs, Lambda, CloudTrail, R53, and more
- Unified Cloudwatch Agent: How anything outside AWS can log data to Cloudwatch
- Metric Filter: Can generate metrics based on logs

### Cloudwatch - What it looks like
First, it's a Regional Service. Starting point: Logging Sources; external compute, DB's, external APIs, AWS services. Log Events are created from data from logging sources. Log Events are stored inside Log Stream (an ordered sequence of log events from the same source). Then a Metric Filter takes Log Group/Stream data, distills metrics which can bet set with alarm notifications

EXAM: CloudWatch is a REGIONALLY resilient service

### Cloudwatch - Vocab
- Log Group: Container for multiple log streams for the same type of logging. Log Group also stored config settings (retention, permissions)
- Log Stream: An ordered sequence of log events from the same source. Log Streams inherit Log Group config settings.
- Log Events: Created from data from logging sources
- Logging Sources: external compute, DB's, external APIs, AWS services


## CloudTrail
- CloudTrail Is a product which logs API actions/calls and account events. Eg. Stop instance, change security group, delete S3 bucket--all logged.
- Very often used to diagnose security or performance issues, or to provide quality account level traceability
- Enabled by default in AWS accounts and logs free information with a 90 day retention
- It can be configured to store data indefinitely in S3 or CloudWatch Logs

### CloudTrail - Vocab
- CloudTrail Event: When CloudTrail logs API calls/activities, it logs them as CloudTrail Events; a record of an activity in an AWS account (action taken by user, role, or service)
- Event History: Record of activity, default stored for 90 days. Enabled by default, no cost for the 90 day history
- Trail: In order to customize CloudTrail service, you need to create 1 or more "Trails". Unit of configuration within CloudTrail. Logs events for the AWS region it's created in.
-- One-Region Trail: Only EVER in the region it's created in. Only logs events for this region
-- All-Regions Trail: Collection of Trails within every AWS Region, but logged as one trail. If AWS adds new regions, they get automatically added to All Region Trails
- Global Service Events: A very small number of services log events globally to ONE region (us-east-1). Eg. IAM, STS, CloudFront. A Trail needs this enabled in order to log these events. Should be enabled in the created Trail by default

EXAM: CloudTrail is a REGIONAL Service. A Trail logs events for the AWS region it's created in

### CloudTrail - Event Types (3)
1. Management Events: Provide information about mgmt operations performed on resources in your AWS account; AKA Control Plane Operations. Eg. Creating VPC, terminating EC2 instance
2. Data Events: Contain information about resource operations performed on or in a resource. Eg. Objects loaded to s3, accessed from s3, lambda function being invoked
3. Insight Events (discussed later): Identify unusual activity, errors, or user behavior in your account
NOTE: By default, CloudTrail only logs Management Events

### CloudTrail - Trails
- One-Region Trail: Only EVER in the region it's created in. Only logs events for this region
- All-Regions Trail: Collection of Trails within every AWS Region, but logged as one trail. If AWS adds new regions, they get automatically added to All Region Trails
NOTE: Small number of services log events globally to ONE region (us-east-1). Eg. IAM, STS, CloudFront. These are called Global Service Events. So, Trails are either logged within the region they were created in, or to us-east-1 if it's a Global Service Event. Or to all regions if All-Region Trail
-- All events are captured by a Trail (management events by default, data events if manually enabled)
-- A Trail stores events in an S3 bucket by default. Logs generated and stored in an s3 bucket can be stored indefinitely; charged for storage in s3. Trail event files are small JSON files, however
-- Alternative to previous bullet, CloudTrail can integrate with CloudWatch Logs and deposit logged data there. Advantage here is being able to use CloudWatch Logs features

## CloudTrail - Continued
- Recent addition to CloudTrail, you can now create Organizational Trail. This means, if created from mgmt account, it can store all info from all accounts in the Org. Making it a single management point for all API and account events across every account in the Org.
- CloudTrail is enabled by default on AWS accounts. Free 90 day event history retention; no storage in s3 unless you configure a Trail
- Trails are how you can config s3 and CW Logs
- By default, only Management Events are logged in CloudTrail (creating, stopping, terminating instance, console login, any AWS interaction). Data events need to be enabled, but come at an extra cost

EXAM: Global Service Events: While most AWS services log data to the same region that service is in, there are a few True Global Services that are logged as GSE's in us-east-1; a Trail must be enabled to capture GSE data
EXAM: CloudTrail is NOT real-time. CT typically delivers log files within 15 minutes of the account activity occurring. CloudTrail is not the product choice you want if you need real time logging.

## CloudTrail Pricing - https://aws.amazon.com/cloudtrail/pricing/
- 90 day Event History is Free
- Get 1 copy of Management Events free in every region in each AWS account
- Beyond that, Management Events: $2.00 / 100,000 events (after the first free copy)
- Data Events: $0.10 / 100,000 events
- CloudTrail Insights $0.35 / 100,000 events analyzed

## DEMO - Implementing an Organizational Trail (CloudTrail)
This CloudTrail will be configured for all regions and set to log global services events.
We will set the trail to log to an S3 bucket and then enhance it to inject data into CloudWatch Logs.

NOTE: You can create individual trails in accounts, but it's always more efficient to use an Organizational Trail.
NOTE: By default when you create a Trail, it creates a Trail for all AWS Regions in your account

EXAM: S3 bucket names MUST be GLOBALLY UNIQUE

1. iamadmin login > CloudTrail > Trails > Create trail > Trail name "Animals4lifeOrg" > check "Enable for all accounts in my org" > uncheck Enable under "Log file SSE-KSM encryption (use this in production, not in this practice) > Enable CloudWatch Logs > CW Logs Role name "CloudTrailRoleForCloudWatchLogs_Animals4Life" > Next > select Event types to log: check Management Events > Next > Review / Create trail
- After creating, can take some time for data to start appearing
2. Open the s3 link on the new Trail > move down through CloudTrail/ > View json.gz (can decompress with Chat GPT) to verify Trail is working
3. In new tab, nav to CloudWatch > Log Groups > Log Streams all in us-east-1
- Account ID is contained within Log Stream file name.
- In Cloud Trail Event History, this will log Events for 90 days even if you have no Trail created. Trails allow you to customize what happens to the data

- In this demo, we created a Trail 1) to store data in s3 2) to put it into CloudWatch Logs

NOTE: s3 charges based on storage. If CloudTrail is enabled, the logs will accumulate possibly past Free Tier
- To Avoid logging events and incurring charges: Go to Trails, "Stop Logging"


## AWS Control Tower
AWS Control Tower offers a straightforward way to set up and govern an AWS multi-account environment, following prescriptive best practices. AWS Control Tower orchestrates the capabilities of several other AWS services, including AWS Organizations, AWS Service Catalog, and AWS IAM Identity Center (successor to AWS Single Sign-On), to build a landing zone in less than an hour. Resources are set up and managed on your behalf.

AWS Control Tower orchestration extends the capabilities of AWS Organizations. To help keep your organizations and accounts from drift, which is divergence from best practices, AWS Control Tower applies preventive and detective controls (guardrails). For example, you can use guardrails to help ensure that security logs and necessary cross-account access permissions are created, and not altered.
- Think of Control Tower as another evolution of AWS Organizations

### CT: Parts of Control Tower
- Landing Zone: Multi-account environment (what most people interact with). SSO/ID Fed, Centralized Logging, Auditing
- Guard Rails: Detect/Mandate rules/standards across all accounts
- Account Factory: Automates and standardizes new account creation
- Dashboard: Single page oversight of entire environment/org

#### CT: Landing Zone
A well-architected multi-account environment. Home Region is the one you deploy into and is always available.
- Built with AWS Orgz, Config, CloudFormation
- Security Organizational Unit (OU): Log Archive and Audit Accounts (CloudTrail / Config Logs)
- Sandbox OU: For testing and for less rigid security situations
- IAM ID Center (prev. AWS SSO): SSO, multiple accounts, ID Federation (using on-premise identity stores)
- Monitoring and Notifications: CloudWatch and SNS
- Service Catalog: End User account provisioning

#### CT: Guard Rails
- Rules for multi-account governance.
- Three types: Mandatory, Strongly Recommended, Elective
- GR functions in 2 Ways:
-- Preventative: Stop you from doing things (AWS Org SCP). Enforced or not enabled. Eg. Allow/deny regions, disallow bucket policy changes (prevent things from happening)
-- Detective: Compliance checks (AWS Config Rules) for maintaining Best Practices. Types: Clear, In Violation, Not Enabled. Eg. Detect / confirm if CloudTrail has been enabled on  your account (identify things happening)

#### CT: Account Factory
- Automated account provisioning. Cloud Admins or End Users (w/ appropriate permissions)
- Guardrails automatically added
- Give admin permissions to a named user (IAM ID)
- Standard Account & Network standard configuration. Eg. IP addressing using VPC
- Allows accounts to be closed or repurposed
- Can be fully integrated with a business's Software Development Lifecycle

## AWS Control Tower (continued)
- Under Control Tower, AWS Organizations creates two Organizational Units (OU): Foundational/Security and Sandbox OU's
- Within each Foundational OU and Security OU, two accounts are created in each: Audit and Log Archive accounts
- Account Factory: Create/configure/delete accounts using Templates: Account Baseline (template) and Network Baseline (template)
- For Guardrails, AWS uses AWS Congfig and SCP
- Drift: Divergence from best practices


## S3 Security (Resource Policies & ACLs)
Bucket Policies: Type of AWS Resource Policy

EXAM: S3 is PRIVATE by default
- only ID with any initial access is Account Root User of account which owns the S3 Bucket
- Any other permissions must be explicity granted through a few ways:
-- S3 Bucket Policy, a form of Resource Policies. RP's: These are attached to Resources, not Identities
-- Resource Policies (RP) provide a resource perspective on permissions. Control access on a Resource
--- Controlling who can access a resource
- EXAM: Unlike ID Policies, Resource Policies's have presence of an explicit Principal Component.

NOTE: You can only attach IDP's to ID's in your OWN account. Only controlling security inside account
- Resource policies can be attached to its own account or DIFFERENT accounts. Inside this RP, you can reference any identities (whether in same or different account)

- RPs can ALLOW/DENY anonymous principals -- even those not authenticated by AWS; anonymous access

### S3 Sec: TL;DR Bucket Policies can grant access for other AWS accounts, and anonymous access

RP's have one major difference to Identity Policies: The presence of an explicit Principal Component.
- The Principal part of an RP defines which Principals are affected by the policy (who is impacted?)

TERM: Principals. A person or application that uses the AWS account root user, an IAM user, or an IAM role to sign in and make requests to AWS. Principals include federated users and assumed roles.
- if a Resource Policy applies to you, you are the Principal
- Eg. "Principal": "*", --> Star is wildcard, which means ANY principal; applies to anyone accessing the Bucket

### S3 Sec: Other s3 Bucket Policy features / functions
Ex 1. Used to control who can access objects, even blocking specific IP addresses
Ex 2. Can Deny a Principal who isn't using MFA from accessing a Bucket
- Additional Examples: https://docs.aws.amazon.com/AmazonS3/latest/dev/example-bucket-policies.html

NOTE: There can only be ONE Policy on a bucket. But, this policy can have multiple statements.

### S3 Sec: Another Form - Access Control Lists (ACLs) - LEGACY
- Legacy (Use Bucket or Identity Policies instead). This is because ACLs are inflexible; no conditions, for example. Can only do 5 things.
- ACL is a subresource

### S3 Sec: Block Public Access Settings
Added in response to lots of public PR disasters; bad bucket configuration leading to data leaks. Until BPA, public/anons could access Bucket. BPA has setting which override Bucket Policies, BUT they apply to just Public Access
- These settings created when making Bucket, but can be adjusted later

EXAM: Identity Policies: Controlling different resources / prefer IAM / Same account only policies
EXAM: Resource Policies: For just controlling S3 / for anonymous or cross-account access
EXAM: Access Control Lists: NEVER unless required, as they are Legacy. AWS recommends against use of ACLs


## S3 Static Hosting
Accessing S3 is generally done via APIs. Static Website Hosting is a feature of the product which lets you define a HTTP endpoint, set index and error documents and use S3 like a website.
 - S3 Static Hosting allows access to s3 via HTTP - Eg. Blogs
 - Usage (2 Documents required): First enable, and in doing so, you have to set INDEX and ERROR documents
 - Index page is entry point to most websites
 - Error Document: When you access a page that isn't there, or other type of service side error that's when Error Doc is shown
 -- Index and Error docs need to be html documents as s3 Static Hosting reads HTML files
 - When Static Hosting is enabled, a static website hosting endpoint is created. Name of endpoint is based on bucket name and region
 -- Want a custom Domain? (via R53)... if so, bucket name matters. Name of Bucket MUST match domain name
 --- Eg. Want a site called top10.animals4life.org? Name your bucket "top10.animals4life.org"

 ### S3 Static Hosting: What else is S3 Static Hosting Good for (other than hosting static websites?
 - Example 1: Offloading. If you have a site with lots of images hosted by compute service, you can offload the media to an S3 bucket w/ static hosting to save money (compute is usually pricier). Offload large data to S3.
 - Example 2: Out-of-band pages. In IT, this means method of accessing something outside of the main way. Example: You want to perform server maintenance and the server needs to go down. You can put an "Under Construction" static page in S3 to put up when production server is down.

 ## S3 Pricing
 Pricing for S3 forms of a number of major components:
 - Cost to Store Data: per gigabyte per month charge
 - Data Transfer Free: for every Gb of data transferred out of S3, per gigabyte charge
 - Data Requests: GET, POST, list, port. Cost per 1,000 operations

### S3: What's FREE?
 - 5Gb monthly storage
 - 20,000 GET requests
 - 2,000 PUT requests


## DEMO Creating a Static Website with S3
 1. Create S3 Bucket > bucket name "[custom-globally-unique]" > uncheck "Block All Public Access" and acknowledge > Create Bucket
 2. Enable Static Website Hosting > access new bucket > Properties tab > scroll to bottom, Edit Static Website Hosting, Enable > Hosting Type: Static > Index Document "index.html" > Error Document "error.html" > In properties, scroll down and copy new static URL
 3. Upload some Objects to the bucket > Objects tab, "Upload" > Upload index.html, error.html, and "img" folder
 4. Paste copied URL into browser
 - You'll get a 403 Forbidden error (Access Denied) - Remember, S3 buckets are private by Default. We need to add permissions for anonymous/public users to visit site (no method to provide creds to S3)
 5. Give Permissions to un-authenticated uses to acess bucket > Access S3 bucket > Permissions tab > Bucket Policy > Edit > Grab JSON from .zip > Paste in, but replace the "Resource" value BEFORE the "/*" (mine now looks like "Resource":["arn:aws:s3:::top10catsever876.com/*"]) > Save
 6. You can now visit your website
 Extra: If you Registered a domain in R53, you can customize your URL. R53 > Hosted Zones > access your domain > Create Record > select Simple Routing > Record Name Eg. "top10".animals4life.io > choose Endpoint "Alias to S3 website endpoint" > Region: us-east-1 > S3 endpoint, select your bucket > click "Define simple record" > Create Records. Now Cantrill can go to top10.animals4life.io. Remember: Domain name and bucket name must match exactly to do this
 7. Clean Up: Empty bucket, delete bucket


 ## Object Versioning & MFA Delete (EXAM)
- Object versioning is a feature which can be enabled on an S3 bucket - allowing the bucket to store multi versions of objects
- These objects can be referenced by their version ID to interact directly - or omit this to reference the latest version of an object
- Objects aren't deleted - object deletion markers are put in place to hide objects.
- Object Versioning starts off in a Disabled state. Once enabled, you CANNOT disable it again. Instead, you can Suspend it. A suspended bucket can be re-enabled.

EXAM: A bucket with Object Versioning enabled can NEVER have OV disabled again

Without versioning, Objects are identified solely by the Object's name, which is unique in the bucket. If you modify an object, the original version of the object is replaced. Versioning lets you store multiple versions of objects within a bucket/
- Operations which would modify an Object instead creates a new version
- Another attribute on an Object in a Bucket (other than Key (name)) is 'id'. A bucket without Versioning enabled has Object id's of 'null'
-- With Versioning enabled, id's are active. Modifying an object will create a new object with a new id. The newest Object version is called the Current or Latest Version
-- If an object is accessed without indicating to S3 which version is required, the Latest Version will be returned. You can access versions by specifying the id

### Object Versioning: Versioning Impacts Deletions
With Versioning enabled, if we indicate to S3 we want to delete the object without giving Version ID, S3 will create a new version of the object with a Delete Marker. In reality, the Object is just hidden. You CAN delete a Delete Marker, which re-activates previous versions.
- To truly delete a particular object, you need to specify the id

### Object Versioning: REMINDERS:
- Versioning CANNOT be disabled after activating, only suspended (and suspending doesn't remove old versions, so you're still billed for all of it)
- Space is consumed by all versions of the object and you are billed for ALL versions
- Only way to return to reduced cost due to Versioning is to delete the bucket and re-add all content to another bucket that doesn't have Versioning enabled

### MFA Delete
Something enabled withing the Versioning config in a bucket. This makes MFA required to change a bucket's versioning state (To change from Enabled to Suspended, etc).
- MFA is required to Delete Versions. When performing API calls to change/delete Version, you need to provide serial number of MFA token AND code, concatenated


## DEMO S3 Versioning
This lesson looks at a 'Animal of the week' website, and how to use versioning to recover when objects are changed and deleted accidentally or intentionally.

1. Create new S3 Bucket: Login to Mgmt/General Admin account > S3 > Buckets > Create Bucket > name [unique] "acbucket23425" > uncheck Block Public Access > Enable Bucket Versioning > Create Bucket
2. Enable Static Hosting: New bucket > Properties tab > Enable Static Website Hosting (bottom of page) > Index doc "index.html" > error doc "error.html" > Save changes
- REMEMBER: Just enabling Static Website Hosting is insufficient, you also need to add a Bucket Policy
3. Add Policy: Access new bucket > Permissions tab > edit Bucket Policy > copy text from bucket_policy.json (from demo .zip) > paste in json, edit Resource to look like " "Resource": "arn:aws:s3:::acbucket23425/*" ", except with your copied Bucket ARN instead
4. Upload files: acbucket > Upload > file "index.html" and folder "img" > click Upload
5. Versions: acbucket > Objects tab > toggle Show Versions > access winkie.jpg > Upload > Add Files > version 2/winkie.jpg > Upload > Access winkie.job object and see multiple versions if "Show versions" toggle is enabled
6. Delete Marker: Untoggle Show Versions within winkie.jpg Object > select winkie.jog > Delete > toggle on Show Versions > see Delete Marker > select Delete Marker and Delete
7. Delete Latest Version to Perma-Delete: acbucket Objects > toggle on Show Versions > select Latest Version of winkie.jpg > Delete
- NOTE: Whenever working with specific Versions of an object, this permanently deletes and makes next most recent version the new Latest / Current Version
8. Clean Up: Empty acbucket > Delete acbucket

REMEMBER: Versioning Enabled can incur significantly higher costs than Versioing turned off.


## S3 Performance Optimization
Single PUT Upload: Up to 5GB Max (don't trust single PUT with this much data), 1 blob of data. Single stream transfer uploaded using s3:PutObject API PUT call. If errors out/fails, full data stream has to restart, making it unreliable. Speed and reliability affected by this sub-optimal transfer.

Multipart Upload: MINIMUM size 100MB. Improves speed and reliability compared to Single Put Upload. Breaks data stream into parts which can break and restart separately, making it more resilient. Always choose multipart beyond 100MB upload.
- Upload can be split into max of 10,000 parts, parts ranging from 5MB -> 5GB. Each part can fail and restart in isolation; risk of uploading large amounts of data is reduce. Transfer rate is increased as you are uploading in parallel, more effectively using internet bandwidth
- The last remaining part can be less than 5MB

S3 Transfer Acceleration:
- How Global Transfer works: Data does not travel in the most efficient route, data can take indirect paths and potentially slows down from hop to hop.
- S3 Transfer acceleration selects the closest, best-performing AWS Edge location and sends directly to S3 bucket. Edge Location transits data over AWS Global Network instead of via public internet (public internet is flexible and reliable over fast). Internet is like public transit with many layovers, whereas AWS Global Network is like a direct flight.
- By Default, Transfer Acceleration is Disabled on an S3 Bucket
- Bucket naming restrictions for Transfer Acceleration: no periods in name, must be DNS compatible


## DEMO S3 Performance
Enable Accelerated Transfer on an S3 bucket and review the AWS provided tool to complete Direct uploads vs Accelerated Transfer

Create s3 bucket (no periods in name, DNS naming compatible) > name "testac3464576" > Create Bucket > new Bucket Properties tab > edit Transfer Acceleration, Enable > Save changes
- NOTE: When Transfer Acceleration is Enabled, an Accelerated endpoint address is provided. You need to use this endpoint to get the benefit of Accel. Transfers.
- To compare upload speeds: http://s3-accelerate-speedtest.s3-accelerate.amazonaws.com/en/accelerate-speed-comparsion.html


## Key Management Service (KMS)
AWS Key Management Service (AWS KMS) makes it easy for you to create and manage cryptographic keys and control their use across a wide range of AWS services and in your applications. AWS KMS is a secure and resilient service that uses hardware security modules that have been validated under FIPS 140-2, or are in the process of being validated, to protect your keys.
- Regional & Public Service: every region isolated when using KMS. Note: KMS is capable of multizone (covered later)
- Public service, occupies AWS Public Zone and can connect from anywhere with access to this zone, with permissions
- KMS Mgmt allows you to CREATE, STORE, MANAGE keys
- Has both Symmetric and Asymmetric keys
- Capable of cryptographic operations, ENCRYPT, DECRYPT, etc
- KMS Keys NEVER leave the product; this is it's primary function. To keep keys in and securely held WITHIN the service

EXAM: FIPS 140-2: KMS Provides a service compliant with FIPS 140-2 Level 2, a US security standard
EXAM: KMS is REGIONAL and PUBLIC

### KMS: KMS Keys
Used by KMS within cryptographic operations. You, apps, and other AWS svcs can use these keys. KMS Key is a container for physical key material; it is Logical (representation of an encryption key)--the data contained is ID, date, policy, description, and state
- Every KMS Key backed by Physical Material (Actual key that is used to encrypt/decrypt). Physical Key material can be generated by KMS or imported
-- This 'material' is what is used to direct/encrypt (data up to 4KB)
- After picking region, user first performs CreateKey. Reminder: KMS performs all operations internally (KMS Keys NEVER leave KMS)
- TERM: Role Separation: Permissions to Encrypt, Decrypt, and Generate Key are all SEPARATE permissions

### KMS: Data Encryption Keys (DEK)
Earlier, it was noted that KMS Keys can only perform cryptoOps on data 4KB or less in size. KMS gets around this by generating Data Encyption Keys
- DEK is generated using KMS key using GenerateDataKey operation
- *** KMS doesn't store the DEK in any way. It provides it to you, then discards it. KMS does not do the encyption or decryption of data using DEKs, you or the service performs the DEK encrypt/decrypt.

### KMS: Key Concepts
- KMS Keys are ISOLATED to a REGION and never leave
- Multi-region keys discussed in a different lesson
- Within KMS, keys are either AWS owned or Customer owned. AWS Owned are for use in multiple accounts and operate in the background
-- Two types of Customer Owner 1) AWS Managed (auto-created by AWS services, like S3) 2) Customer Managed (created explicitly by customer to be used by app or AWS svc
-- Customer Managed Customer Owned KMS Keys: More configurable. AWS Managed can't really be customized
- Aliases: shortcuts to keys. Aliases are PER REGION. Neither aliases or keys are Global, by default

### KMS: Key Rotation
When the physical backing material used to perform cryptoOperations is changed at regular intervals (usually once annually)
- KMS Keys support key rotation
- Customer Key Rotation is optional
- When key is rotated, material (data) is changed and NOT the logical key

### KMS: Permissions (Policies / Security)
Account Trust is explicitly added to a Key Policy, or not.
- Key Policy (type of Resource Policy): Every KMS key has a policy. On Customer Managed keys, you can change the policy
- Keys have to explicitly be told they trust the account they're contained within
- Generally, KMS is managed using this combination: Key Policies trusting account + Identity Policies allowing IAM users to interact with key

REMINDER: Resource Policies require a PRINCIPAL in their JSON file, IDP's do not


## DEMO - KMS - Encrypting the battleplans with KMS
Run through the practical steps of creating and configuring a KMS Key, an Alias and we use that Key and the CLI tools to encrypt and decrypt some data

1. Generate KMS Key: Login to Mgmt/General Admin account > KMS > Create a key > Key Type: Symmetric > Next > create alias "catrobot" > Next > Define key admin permissions: check "iamadmin" (so iamadmin user can administer this key) > Next > Define key usage permissions: select "iamadmin" > Next > Review > Finish
2. Enable Key Rotation: Access catrobot key > Key Rotation tab > Check auto-rotate KMS key yearly, Save
3. Use Key / Create Battle Plan: access CloudShell (first icon on right-side main AWS menu, looks like Terminal icon) > Create plaintext battleplan:  || echo "find all the doggos, distract them with the yumz" > battleplans.txt ||
4. Encrypt message - Output will be the Encrypted not_battleplans.enc. Enter below lines into Shell
aws kms encrypt \
    --key-id alias/catrobot \
    --plaintext fileb://battleplans.txt \
    --output text \
    --query CiphertextBlob \
    | base64 --decode > not_battleplans.enc
5. Receiver needs to Decrypt the cihpertext. Enter below lines into Shell:
aws kms decrypt \
    --ciphertext-blob fileb://not_battleplans.enc \
    --output text \
    --query Plaintext | base64 --decode > decryptedplans.txt
6. Clean Up: Select key > Key Actions: Schedule for deletion (waiting period 7-30 days, input 7) > Confirm > Schedule deletion


## SSE-S3 (AES256)
Step through the various encryption options available within S3 and finish by looking at default bucket encryption settings
- Server-Side Encryption (SSE).
-- EXAM: Buckets are NOT encrypted, Objects are; encryption not defined at Bucket level. Encryption is defined at Object level
- Client-Side Encryption (CSE). S3 never sees plaintext

### SSE-S3: SSE VS CSE: How data is stored on disk in an encrypted way; encryption at rest
- Path: Users/App <-> S3 Endpoint <-> S3 Storage.
-- In transit: On both SSE/CSE, Data in transit between User/S3 Endpoint is encrypted in transit.
-- AT REST is what we're focusing on.
--- In CSE, Objects being uploaded are encrypted by the client before they ever leave client-side. AWS will never see data in plain text form. In CSE, you own keys, process, and tooling
--- In SSE, even though data is initially encrypted in-transit using HTTPS, the Objects themselves are NOT initially encrypted. From User > S3 Endpoint, data is in its original form. At S3 endpoint, the data gets encrypted and delivered to S3 Storage as ciphertext.

NOTE: AWS has made SSE mandatory, so you can no longer store objects in an unencrypted form on S3. You control what type of SSE is utilized

### SSE-S3 - Types of Server-Side Encryption within S3:
- SSE-C: SSE with Customer provided/managed Keys. Customer handles keys, S3 handles enc/dec. In-Transit data encrypted by HTTPS, plaintext otherwise
- SSE-S3: [The Default] SSE with Amazon S3 Managed Keys. AWS handles both enc/dec and key mgmt. Uses AES-256
-- Three problems with SSE-S3: 1) Not suitable strongly regulated environments 2) if you need Role Separation, not suitable 3) need to control Key Rotation? not suitable. AKA No Key Control, No Role Separation
- SSE-KMS: SSE with KMS Keys stored in the AWS Key Management Service. KMS service now managing the keys, meaning you can create a Customer Managed Key; isolated permissions, fully configurable. KMS Generates and delivers DE Keys to S3 (KMS does not store DEKs). Great for controlling Permissions, Role Separation and Key Rotation Control.
* Difference between methods is what parts of the process you trust S3 with and how encrypt process/key mgmt is handled
* High Level: Two components to SSE: 1) encrypt/decrypt process, 2) generation/mgmt of crypto keys (these two components handled differently in different SSE types)

### SSE-S3: Resources
- Visual of SSE Methods and Details: https://imgur.com/a/lCg5gmA
- https://docs.aws.amazon.com/AmazonS3/latest/user-guide/default-bucket-encryption.html
- https://docs.aws.amazon.com/kms/latest/developerguide/services-s3.html
- https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingKMSEncryption.html
- https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingServerSideEncryption.html
https://docs.aws.amazon.com/AmazonS3/latest/dev/ServerSideEncryptionCustomerKeys.html


## Demo - SSE-S3 - Object Encryption and Role Separation
Create an S3 bucket, and upload 3 images to the bucket using different encryption methods

1. Create S3 Bucket > name "catpics[random number]" > Create Bucket
2. Create Key: Nav to KMS > Create Key > Defaults > Alias "catpics" > Next > Don't set any Key Administrative Positions > Next > skip Key Usage Permissions > Finish
3. Upload SSE-S3 image: Back to S3 > catpics bucket > upload just sse-s3-dweez.jpg (must upload separate as we are configuring separate encryptions) > expand Properties accordian, Server-side encryption "Specify an en encryption key" > Encryption settings "Override bucket settings" > Encryption Key type "SSE-S3" > Upload
4. Upload SSE-KMS image w/ AWS managed default key: Upload see-kms-ginny.jpg > Properties > SSE - Specify an encrypt key > Override bucket settings > key type: SSE-KMS > Choose from your AWS KMS keys: choose the one ending "aws/s3", an AWS managed default key > Upload
5. Replace Step 4 Object, SSE-KMS image w/ KMS Generated Key: Upload see-kms-ginny.jpg > Properties > SSE - Specify an encrypt key > Override bucket settings > key type: SSE-KMS > Choose from your AWS KMS keys: alias "catpics" > Upload
6. Apply Deny policy on IAM, preventing KMS use > IAM Dashboard > Users > iamadmin > Permissions tab > Add Policy: Inline Policy > JSON tab > delete template > Paste in JSON provided in lesson > Review policy > name "denyKMS" > Create policy. Now you can open see-s3 image, but not the kms image. IAM > Remove DenyKMS
7. Set Default Bucket Encryption: catpics bucket > Properties tab > Default Encryption "edit" > key type: SSE-KMS > AWS KMS Key: Choose, "catpics"
8. Upload Default Merlin jpg with no encrypt settings: upload default-merlin.jpg without changing anything > Properties tab: Server-side encryption settings - see default stuff added from Step 7

EXAM: If you need to fully manage the keys used as part of S3 encryption process, you have to use SSE-KMS


## S3 Bucket Keys
Amazon S3 Bucket Keys reduce the cost of Amazon S3 server-side encryption using AWS Key Management Service (SSE-KMS). Bucket-level keys for SSE can reduce AWS KMS request costs by up to 99 percent by decreasing the request traffic from Amazon S3 to AWS KMS.
- Without bucket keys, you make a ton of calls to KMS API. Each object is a separate call for DEK to KMS. Also throttling issues--the generate DEK operation can only be run 5,500, 10,000, or 50,000 times per second--this is shared across regions. AKA Using a single KMS Key results in a scaling limit for PUTS per second per key.
-- Bucket Keys improve this situation. Instead of KMS Key generating each DEK, it generates a single time-limited bucket key. This bucket key lives in the bucket and for a period of time, generates DEKs... offloads work from KMS to S3, reducing cost and increasing scalability.
NOTE: Not retroactive, so previously created S3 bucket objects will still be KMS generated DEKs
- CloudTrail (CT) Events will now show the bucket ARN instead of your object ARN
- Offloading KMS to S3 means fewer CT KMS events in the logs
- Bucket keys work with same-region and cross-region replication; the object encryption is maintained. When S3 replicates an encrypted object, it generally preserves the encryption settings
- If replicating plaintext to a bucket using bucket keys, the object is encrypted at the destination side (ETAG changes between source/destination)


## S3 Object Storage Classes
### S3 Standard
### S3 Standard-IA
### S3 One Zone-IA
### S3 Glacier
### S3 Glacier Deep Archive
### Intelligent-Tiering

### Standard
The Default. Stored objects stored across AT LEAST 3 AZs; can cope with multi-AZ failure; this provides 11 9's of durability (if store 10mil objects, on avg you might lose 1 object every 10,000 years).
- Should be used for frequently accessed data that is IMPORTANT and NON-REPLACEABLE
- Replication uses MD5 Checksums and Cyclic Redundancy Checks (CRCs) to detect and fix data corruption
- Successful receipt and storage in S3? S3 API endpoint returns 'HTTP/1.1 200 OK'
- Most balanced class when looking at cost and features
- First byte latency of milliseconds, objects can be made PUBLICLY AVAILABLE (using S3 permissions or static website hosting site for public internet)
#### Standard - Billing
- GB per Month fee for data stored
- $1 per GB charge for transfer OUT (transfer IN is always free)
- Price per 1,000 requests
- NO retrieval fee, NO minimum duration, NO min size
EXAM: S3 Standard should be used for frequently accessed data that is IMPORTANT and NON-REPLACEABLE

### S3 Standard-IA
IA = Infrequent Access. This class is designed for infrequently accessed data that needs reliability and durability.
Data replicated over 3 AZ's. Similar durability and first byte latency. Same checksum and CRCs. Objects can be made publicly available.
### Standard-IA Billing
- Big difference from Standard billing: Storage costs are cheaper than S3 standard
-- New cost component compared to Standard: RETRIEVAL FEE: for every byte retrieved, there is a cost to retrieve IN ADDITION to transfer fee
- MINIMUM DURATION charge: However long you store this class, you're billed minimum of 30 days
- MINIMUM CAPACITY charge: Per object, you are charged as if they are each at least 128KB in size; don't use IA to store lots of tiny objects
- Per request charge, data OUT charge, same as Standard
- Transfer IN is free
EXAM: S3 Standard-IA should be used for LONG-LIVED DATA which is IMPORTANT, but access is INFREQUENT

### S3 One Zone-IA
Similar to Standard-IA in many ways. Cheaper than both Std-IA and Std. The compromise for cost reduction: Data stored using this class is only stored in ONE Availability Zone
- Still retrieval fee, still 30 day minimum billing (like std-IA), still min cap of 128KB (like std-IA)
- One Zone-IA does not provide the multi-AZ resilience model, instead, one AZ used within the region; cheaper storage but greater risk of data loss
- SAME DURABILITY: 11 9's of durability (unless the AZ fails). Data still replicated in the one AZ
EXAM: Used for LONG-LIVED data that is INFREQUENTLY accessed, but for which is NON-CRITICAL and EASILY REPLACED

### S3 Glacier
S3 Glacier, instant access to your data; instant retrieval. Like S3 Standard-IA but cheaper storage, more expensive retrieval, longer minimums. Designed for when you need data instantly, but not very often (like once a month).
- Minimum storage duration charge: 90 days

### S3 Glacier Flexible
Same 3 zone AZ architecture, 11 9's of durability
- Trade-off compared to previous classes:
-- Think of the objects store here as "cold objects"; not ready for use; not immediately available, can't be made public; a RETRIEVAL PROCESS is required
--- Retrieval Jobs, 3 Types (faster = more $:
--- 1. Expedited: data available in 1-5 minutes
--- 2. Standard: available in 3-5 hours
--- 3. Bulk: 5-12 hours
- MINIMUM BILLABLE DURATION: 90 days
- MINIMUM BILLABLE SIZE: 40KB
- No Public Access
EXAM: First Byte latency = minutes or hours. No public access. Glacier Flexible is for situations where you need to store archival data where frequent/real-time access isn't required (like once a year access)

### S3 Glacier Deep Archive
The cheapest form of S3 storage. The most restrictions.
- If Glacier Flexible data is in "chilled" state, Glacier Deep Archive data is "frozen"
- MINIMUM BILLABLE DURATION: 180 days
- MINIMUM BILLABLE SIZE: 40KB
- Objects are not publicly accessible; retrieval job required
-- Retrieval Jobs:
-- 1. Standard - 12 hours
-- 2. Bulk - up to 48 hours
EXAM: First byte latency = hours or days. Used for archival data that is very rarely accessed, if ever. Good for data that requires retention length, or secondary long-term backups

### Intelligent-Tiering
Different from all previous classes; it contains five different storage tiers.
- When you move objects into this class, tier is determined by monitoring the data's usage
- Tiers:
-- Frequent Access (less than 30 days between access)
-- Infrequent Access (30+ days between access)
-- Archive Instant Access (90+ days between access)
-- Archive Access (90 -> 270)
-- Deep Archive (180 -> 730)
Instead of a retrieval cost, Intelligent Tiering has a monitoring and automation cost per 1,000 objects (management fee). Only use this when your app can tolerate asynchronous access patterns.
EXAM: Intelligent-Tiering is designed for long-lived data where usage is CHANGING or UNKNOWN. Ideal for uncertain access and low admin overhead
- https://aws.amazon.com/s3/pricing/
- https://aws.amazon.com/s3/storage-classes/


## S3 Lifecycle Configuration
Allows objects storage classes to be changed and objects deleted automatically. Step through S3 lifecycle management/configuration/rules both in theory and via an S3 console example
- You can create lifecycle rules on S3 buckets which can auto-transition or expire objects in a bucket. Great for objects that have a life cycle (activity on object is predictable)
- Lifecycle Configuration is a set of RULES that consist of ACTIONS. Rules can be applied to a whole Bucket or groups of objects in a bucket if defined by prefixes/tags
- Two types of Actions applied (both work on versions if Object Versions are enabled on bucket):
-- 1. Transition Actions: Change storage class of affected objects
-- 2. Expiration Actions: Delete objects/object versions
EXAM: S3 ONE ZONE-IA CANNOT transition into S3 Glacier-Instant Retrieval. Transition can't go up the waterfall of classes, only down. See waterfall visual
EXAM: Smaller objects can cost MORE (minimum size)
EXAM: If object initially placed in Standard class, there is 30 day minimum period where an object needs to remain on S3 Standard before transition down the waterfall
EXAM: A SINGLE rule CANNOT transition to Standard-IA or One Zone-IA and THEN to glacier classes within 30 days (duration minimum); must remain in IA class for min 30 days before moving to Glacier


## S3 Replication
S3 has two replication features which allow objects to be replicated between SOURCE and DESTINATION buckets in the same or different AWS accounts

### S3 Replication - Two Types:
- Cross-Region Replication (CRR) is the process used when Source and Destination are in different AWS regions
- Same-Region Replication (SRR) is used when the buckets are in the same region.

### S3 Replication - The Difference:
With Cross-Region Replication, The Destination Bucket, b/c it's in a different AWS account, doesn't trust the Source account or its IAM Role that gets created for Replication purposes by Source Bucket. If configuring replication between different accounts, you have to create a Bucket Policy in the Destination Bucket which allows the Source IAM role to write/replicate into the Destination bucket.

### S3 Replication - Options:
1st option: What you replicate. Default is entire Source bucket to Destination bucket (everything in it), OR subset.
- For subset, create a rule that adds a filter to filter objects by prefix or tags
2nd: Storage Class to be used. The Default is to use the same class, but you can choose a cheaper class if this data is secondary.
EXAM: Default Storage Class to use for S3 Replication is to maintain the same storage class as found on the Source Bucket, but you can override that in the replcation configuration (good if Destination Bucket will contain secondary data)
3rd: Ownership. Define ownership of objects in the Destination Bucket. Default is that dest buckets are owned by same entity that owns Source - This may not work if Source/Dest buckets are in different accounts (Dest bucket may not be able to read objects if objects are owned by Source).
4th: Replication Time Control (RTC): Adds guaranteed 15 minute SLA onto this process. This is used to make sure Source/Destination are in sync as closely as possible.
EXAM: 15 minute replication mentioned on exam? Then you know you need Replication Time Control (RTC)

### S3 Replication - Considerations:
EXAM:
- By Default, Replication is NOT retroactive and Versioning needs to be ON. Eg. If you enable Replication on a bucket that already has objects, those objects will not be replicated.
- Both Source AND Destination bucket need Versioning enabled
- You can use S3 Batch Replication to replicate pre-existing objects (since Replication is NOT retroactive by default)
- One-way replication: If you manually add objects to Destination Bucket, they will NOT be replicated to Source
-- Bi-directional replication is a recently added feature, but is an additional setting that needs to be configured
- Replication Capability: can handle unencrypted, SSE-S3 & SSE-KMS (with extra config), SSE-C
- Source Bucket Owner needs Permissions on the objects which will replicate
- Will NOT replicate: System events, Glacier, or Glacier Deep Archive
- NO DELETE markers are NOT replicated by Default. You can enable with DeleteMarkerReplication

### S3 Replication - Why Use It?
- For SRR (same region): For log aggregation, synchronize PROD and TEST accounts, resilience with strict sovereignty requirements (some data cannot leave specific regions)
- For CRR (cross region): Global resilience improvements, latency reduction

### S3 Replication - Resources:
- https://docs.aws.amazon.com/AmazonS3/latest/dev/replication.html
- https://aws.amazon.com/about-aws/whats-new/2019/11/amazon-s3-replication-time-control-for-predictable-replication-time-backed-by-sla/



## DEMO Cross-Region Replication of an S3 Static Website
Create 2 S3 buckets - one in N. Virginia, the other in N. California and configure Cross-Region Replication (CRR) between the two.

1. iamadmin account, N.VA region selected
2. Nav to S3 > Create Source Bucket > Create Bucket > name of source "sourcebucketta[random number]" > region us-east-1 > Create Bucket
3. Enable Static Website on Source > Properties Tab > Static website hosting: edit: Enable > type: static website > index doc "index.html"/error doc "index.html" > Save changes
4. Edit Source bucket Permissions for Public Access > Permissions tab > uncheck Block All Public Access > confirm > Save changes
5. To made Source Bucket public, add policy > Permissions tab > Bucket Policy "edit" > from lesson docs, paste JSON, replace Resource arn before the "/*" > Save
6. Create Destination Bucket & Set Permissions/Policy > Create Bucket > name of dest "destinationbucketta[random number]" > AWS Region: us-west-1 > uncheck Block All Public Access > Properties tab, Enable Static website hosting > Hosting type: static > index/error docs "index.html" > Save changes > Permissions tab, edit Bucket policy, paste JSON, update ARN, Save
7. Enable Cross-Region Replication (CRR): Source Bucket Management tab > Create replication rule > Enable Versioning > Replication rule name "staticwebsiteDR" > Status "Enabled" > Choose Rule Scope: "Apply to All objects in the bucket" > Destination: Browse S3, find destination bucket, enable versioning > IAM Role: dropdown "create new role" > Create replication rule > Replicate Existing Obejcts? No (as we have no pre-existing objects)
8. Clean Up: Empty/Delete Destination Bucket > Empty/Delete Source Bucket > IAM: locate role staring with "s3crr_role[...]"


# S3 PreSigned URLs
Presigned URL's are a feature of S3 which allows the system to generate a URL with access permissions encoded into it, for a specific bucket and object, valid for a certain time period
- PreSigned URLs can be used for downloads (GET) or Uploads (PUT)

Eg. S3 bucket with NO public access configured. Currently, a user would have to authenticate in IAM and be authorized to access resource. If you need to give an unauthenticated user access to the bucket, there are 3 [un-ideal] solutions 1) give mystery user AWS ID 2) give myst.user credentials 3) make object public.
- Better solution than all this is PreSigned URLs

NOTE: The PreSigned URL is used, the holder of the URL is interacting with S3 as the person who GENERATED the URL. In the example above, the mystery user would be iamadmin

EXAM: You can create a URL for an object that you have NO ACCESS TO. But, since you have no access, the PreSigned URL won't either. Not an applicable use case, but possible
EXAM: When using a PreSigned URL, the permissions are the same as the CURRENT permissions of Identity that generated the PreSigned URL. (So Access Denied could mean the generating ID never had access, or doesn't now)
EXAM: Don't generate PreSigned URLs using an IAM Role (temp credentials of a Role can expire before temp access to PreSigned URL)


 ## DEMO S3 Creating and using PreSigned URLs
 Create a bucket, upload an object and generate a presignedURL allowing access for any unauthenticated identities.

 1. Create bucket > name "animals4lifemedia[randomnumber]" > Create bucket
 2. Upload object > all5.jpv to new bucket
 3. Generate PreSigned ULR > Cloud Shell (terminal icon top right of AWS) > shell command "aws s3 presign s3://animals4lifemedia745675/all5.jpg --expires-in 180"
 - 180 is in seconds, 3 mins
 4. Clean up: Empty/delete bucket

 NOTE: Interesting Aspects...
 1. Try "aws s3 presign s3://animals4lifemedia745675/all5.jpg --expires-in 604,800"
 2. Nav to IAM > Users > iamadmin > Permissions: Add inline policy, copy JSON from lesson > save
 3. In CloudShell, try "aws s3 ls", you'll see Access Denied. This Explicit Deny overrules S3 permissions. Refresh PreSigned URL and see that access is now denied as the current permissions of iamadmin are restricted from S3
 4. iamadmin currently restricted from S3, but can still generated a PreSigned URL for it, even with no access.
 - You can also generate a PreSigned URL on a non-existent object
 - If you generate a PreSigned URL with an assumed Role, the URL will stop working with the temporary creds for the Role stop working
 - Can now create PreSigned URL from AWS Dashbord s3 > bucket > object > Object Actions dropdown "Share with a presigned URL"


## S3 Select and Glacier Select
EXAM: Understand this architecture
S3 and Glacier Select allow you to use a SQL-Like statements to retrieve partial objects from S3 and Glacier.
- Ways you can retrieve PARTS of objects rather than the entire object
-- Both S3 and Glacier super scalable. S3 can store objects up to 5TB and store infinite number of these objects. Often, you don't need to retrieve the entire 5TB object
- With S3 Select, filtering occurs on the service/the source (S3); The data delivered by S3 is pre-filtered WITHIN S3, making it quicker and reducing costs


## S3 Events
The Amazon S3 notification feature enables you to receive notifications when certain events happen in your bucket. To enable notifications, you must first add a notification configuration that identifies the events you want Amazon S3 to publish and the destinations where you want Amazon S3 to send the notifications. You store this configuration in the notification subresource that is associated with a bucket
- Notifications generated when events occur in a bucket
- Can be delivered to SNS Topics, SQS Queues and Lambda Functions
- Types of events: object Created (Put, Post, Copy, CompleteMultiPartUpload), object Delete (*, Delete, DeleteMarkerCreated), object Restore (Post (Initiated), Completed), Replication
- Events are generated by S3 Service, known as S3 Principal, so we also need to add Resource Policies to the destination services to allow S3 svc to interact
- Events are JSON objects
- S3 Event notifications are dated and limited features. Can also use EventBridge which supports more events and wider svc integration.
DEFAULT: use EventBridge as Default for S3 event notifications


## S3 Access Logs
Server access logging provides detailed records for the requests that are made to a bucket. Server access logs are useful for many applications. For example, access log information can be useful in security and access audits. It can also help you learn about your customer base and understand your Amazon S3 bill.
- You have a Source bucket where you want to track access. You have a Target bucket where you'll store tracked events. Can be enabled via Console UI or via PUT Bucket Logging
- S3 Logging managed by S3 Log Delivery Group
- Logs delivered as Log Files, consisting of Log Records
-- Each attribute within a record is space-delimited, and Records within in a file are newline-delimited
- Single Target bucket can be used for many Source buckets, separate logs using prefixes in Target bucket


## S3 Object Lock
You can use S3 Object Lock to store objects using a write-once-read-many (WORM) model. It can help you prevent objects from being deleted or overwritten for a fixed amount of time or indefinitely. You can use S3 Object Lock to meet regulatory requirements that require WORM storage, or add an extra layer of protection against object changes and deletion.
- WORM Model - wrote-once-read-many. Once Object Versions are created, they can't be overwritten or deleted (object versions are locked)
- User can enable on 'new' buckets, support ticket required for adding to existing bucket
- Object Lock required Versioning to be enabled. Once you create/enable Object Lock, you can't disable/delete OL or Versioning
- Can define Object Lock on objects, or a Bucket can have a default Object Lock Settings
- You can overlap the effects, Eg. Having a Legal Hold and Retention: Governance enabled on same object

Object Lock handles retention in TWO ways:
1. Retention Periods
2. Legal Holds
- Can have both, either, or none

### S3 Object Lock - Retention Period Methods - Retention Periods and Legal Holds
#### Retention Period: When you create lock, you specify retention period for DAYS / YEARS
Two Modes of Retention Period (EXAM):
- 1. Compliance Mode. Object version Can't be adjusted, deleted, overwritten for duration of period. Retention period duration can't be reduced. Retention Mode cannot be adjusted during period (EXAM: not even by Account Root User). This is the most strict Object Lock: Retention Period w/ Compliance Mode.
- 2. Governance Mode. Set a retention period, but special permissions can be granted allowing Lock Settings to be adjusted during the retention period
-- EXAM: s3:BypassGovernanceRetention in order to allow settings adjustment, along with header along with request "x-amz-bypass-governance-retention:true" (console ui default)

### S3 Object Lock - Lock Legal Hold
With Legal Hold, you don't set a Retention Period at all. Instead, for an Object Version, you set Legal Hold ON or OFF; binary. NO RETENTION.
- While Legal Hold flag is on, no deletes and no changes until Legal Hold is removed
-- s3:PutObjectLegalHold required to add or remove
- Legal Hold can be used to prevent accidental deletion of critical object versions. Or if you need to flag an object version for a legal case/project etc


## S3 Access Points
Amazon S3 Access Points, a feature of S3, simplifies managing data access at scale for applications using shared data sets on S3. Access points are unique hostnames that customers create to enforce distinct permissions and network controls for any request made through the access point.
- You can have 1 bucket with many access points, each access point can have different policies
- Access Points can be limited in terms of WHERE they can be accessed from. Eg. VPC or internet
- Every Access Point has its own endpoint address
- EXAM: Access Point created via Console or with this shell command:
-- aws s3control create-access-point --name [name] --account-id [account-id] --bucket [bucket-name]
- Access Points can be thought of as mini buckets or different views of the bucket
- Each Access Point has a unique DNS that would be given to the users using it
- Access Point Policies control permissions for access via Access Point and are functionally equivalent to a Bucket Policy. Access Point Policy can restruct identities to certain prefixes, tags, or actions based on need
- IMPORTANT: Any permissions defined on an Access Point need to also be defined on the Bucket Policy

### S3 Access Points Resource:
https://docs.aws.amazon.com/AmazonS3/latest/dev/creating-access-points.html#access-points-policies


## Demo S3 Multi-Region Access Points (MRAP)
Gain practical experience working with Multi-region access points

Amazon Simple Storage Service (S3) Multi-Region Access Points provide a global endpoint for routing Amazon S3 request traffic between AWS Regions. Each global endpoint routes Amazon S3 data request traffic from multiple sources, including traffic originating in Amazon Virtual Private Clouds (VPCs), from on-premises data centers over AWS PrivateLink, and from the public internet without building complex networking configurations with separate endpoints.

1. Create two buckets: S3 > Create bucket "multi-region-demo-sydney-[random-number]", region ap-southeast-2, Enable Bucket Versioning > Create > Create 2nd bucket "multi-region-demo-canada-[random-number]", region ca-central-1, Enable Bucket Versioning > Create
2. Create Multi-Region Access Point: S3 > Multi-Region Access Points > Create Multi-Region Access Points > name "reallyreallycriticalcatdata", add the 2 created buckets > Create (MRAP ARN arn:aws:s3::704310952405:accesspoint/m6s3xgw995fsb.mrap)
*NOTE: You CANNOT add or remove buckets to Multi-Region Access Point after it's cerated
3. Configure replication between the buckets: Access new MRAP > Replication & Failover tab > template:replicate among all specified buckets, Buckets: check both, Scope: Apply to all objects in bucket > Create replication rules
4. Test with CloudShell > Switch region to Tokyo > open CloudShell > enter "dd if=/dev/urandom of=test1.file bs=1M count=10" > copy ARN from MRAP dashboard, enter "aws s3 cp test1.file s3://[your-copied-mrap-arn]"
- Steps 3 and 4 generate a test file for upload, then uploads to the Sydney bucket. Replication of file to Canada bucket may take a few minutes
5. See remaining steps in the demo file in this repo
6. Clean up: s3 MRAP > select MRAP, delete > s3 buckets Empty and Delete


# VIRTUAL PRIVATE CLOUD (VPC) BASICS

## VPC Sizing and Structure
Step through the design choices around VPC design and IP planning. How to design an IP plan for a business; designing a VPC

One of the first things to decide on is IP range; the VPC CIDR.
- IMPORTANT: This planning is critical and is not easy to change later
- What size should VPC be? How many services need to fit, each service has an IP, each occupies space in VPC
- Are there any Networks we can't use, or need to interact with?
- Be mindful of IP ranges other VPC's used in other cloud env's in on-premise networks. Try to avoid IP ranges that other parties use that you might need to interact with
- Try to predict the future... How things may change
- VPC structure - Tiers, Resiliency (Availability) Zones

### VPC Sizing / Structure - Example: Animals4Life (A4L).
*NOTE: REVIEW IP RANGES: Network address, prefix, how they map to range of address
- 3 offices: London, NY, Seattle (3 IPs)
- Field workers (laptop, 3G, 4G, satellite, email, chat, file access, etc)
- Already has 3 existing networks. 192.168.10.0/24, 10.0.0.0/16, 172.31.0.0/16 (new AWS network design cannot use or overlap with these)
- Access/Migrate data
-- Avoid the following ranges:
--- 192.168.10.0/24 range is 192.168.10.0 -> 192.168.10.255
--- 10.0.0.0 (AWS) 10.0.0.0 -> 10.0.255.255
--- 172.31.0.0 (Azure) 172.31.0.0 -> 172.31.255.255 (this shares same IP address range as AWS defulat VPC, se we can't use default VPC for anthing production)
--- 192.168.15.0/24 (London) -> 192.168.15.255
--- 192.168.20.0/24 (NY) -> 192.168.20.255
--- 192.168.25.0/24 (Seattle) -> 192.168.15.255
--- 10.128.0.0/9 (google) -> 10.255.255.255
^ When designing an IP addressing plan, don't use any of the above

### What IP ranges? How many networks does A4L need?
- VPC min /26 (16 IPs). max /16 (65536 IPs)
- Avoid common ranges to avoid future issues. 10.1 and 10.0 are common, avoid up to 10.10. Start at 10.16 per Cantrill's recommendation
- How many ranges a business requires? First, how many regions does AWS operate in? Since we're pre-allocating, overestimate for a buffer. A4L we don't really know how many regions they'll operate in, but we can make educated guess then add buffer.
-- Suggest having at least 2 ranges in each regoin, in each AWS account
-- Assumed regions for A4L: 3 US, Europe, Australia (5) x2, and 4 AWS accounts. 3US + 1AU + 1EU = 5 Regions, 2 ranges ea. region, total of 10 IP ranges per account. Since there are 4 accounts, 10 ranges x 4 accounts = 40 IP ranges

#### IP Range Review:
- We're going avoid 10.0 - 10.10 (too commonly used)
- Start at 10.16 per Cantrill
- Can't use 10.128 -> 10.255 because Google Cloud uses it
- Our Range: 10.16 -> 10.127 inclusive

### VPC Sizing
VPC Sizing Chart: https://imgur.com/a/cJhXTxx
- Deciding which to use on this chart? Two important Questions:
-- How many subnets will you need in each VPC?
-- How many IPs total? How many IPs per subnet?

#### VPC Sizing - How many Subnets?
- Services inside a VPC use subnets, which are where IP addresses are allocated from
- VPC Services run from within subnets
- A subnet is located in ONE availability zone

##### How many Availability Zones will your VPC use?
- Start with 3 as DEFAULT, per Cantrill. And add at least 1 spare. DEFAULT: AT MINIMUM, always assume 4 AZ's
- Within VPCs, you also have tiers. Tiers for different types of infrastructure inside VPC; web tier, application tier, database tier... so 3, plus buffer. DEFAULT: assume 4 tiers.
-- 4 tiers, 4 AZ's. Each tier has a subnet in each AZ: 4x4 = 16 subnets. Using /16 VPC into 16 subnets, results in 1 smaller network ranges, each being /20. If we did /18 VPC prefix, each subnet would be /22
TOTAL: 16 subnets with /20 prefix

### VPC Sizing / Structure - Example: Animals4Life (A4L) - CONTINUED - PROPOSAL:
- A4L is a global org and could grow significantly (assume huge level of growth)
- Use the 10.16 -> 10.127 range (avoiding Google, common ranges, etc)
- 5 AZs
-- Start at 10.16 (US1), 10.32 (US2), 10.48 (US3), 10.64 (EU), 10.80 (AU) - each account has 1/4th of the range
--- total of 16 /16 network ranges for each region.
- 3 accounts: general, prod, dev. Add 1 more for buffer. 4 accounts total
-- Each account in each region gets 4 /16 ranges, enough for 4 VPCs per region per account
- /16 per VPC - 3AZ (+1), 3 tiers (+1) = 16 subnets for each VPC
- /16 splits into 16 subnets = /20 per subnet (4,091 IPs) - May seems excessive, but assume highest possible growth potential

### VPC Sizing & Structure Resources
https://aws.amazon.com/answers/networking/aws-single-vpc-design/
https://cloud.google.com/vpc/docs/vpc
https://github.com/acantril/aws-sa-associate-saac02/tree/master/07-VPC-Basics/01_vpc_sizing_and_structure


## Custom VPCs, includes DEMO
 Step through the architecture and features of Custom VPCs including the main issues which are raised in the exam
 - Learn to build a complex, mult-tier VPC

 In this multi-tier custom VPC build...
 - Using VPC us-east-1, 10.16.0.0/16
 - Inside VPC, 4 tiers in 4 AZs = 16 subnets.
 - We will create all 4 tiers: reserve, DB, app, web
 - We will only create 3 AZ's: A, B, C. We will not create subnets in the capacity reserved for the future AZ
 - We will be creating VPC, subnets, an internet gateway, NAT gateways, bastion host (using bastion host is bad practice - don't do it, not secure), NACLs


 ## DEMO - Custom VPCs - Create VPC - Overview
 - VPCs are regionally isolated and regionally resilient service. Operates from all AZs in that region.
 - Nothing is allowed IN or OUT of a VPC without explicit permission; provides isolated blast radius; if you have a proble inside a VPC, the impact is limited to that VPC and/or anything connected
 - Custom VPCs allow for simple or multi-tier; flexible configuration
 - Custom VPCs also provide Hybrid Networking
 - When you create VPC, you can pick DEFAULT or DEDICATED tenancy. AKA shared or dedicated hardware
 -- If you pick DEFAULT tenancy, you can choose on a per resource basis later on when provisioning resources whether it's shared or dedicated hardware
 -- If you pick DEDICATED tenancy at VPC level, it's locked in. Any resources created inside the VPC have to be on dedicated hardware (cost premium compared to Default)
 - By default, VPC uses IPv4 private/public IPs. The private CIDR block is main method of IP communication for VPC, & Puclic IPs (when you want make resources public)
 - VPC allocated ONE mandatory Private IPv4 CIDR Block
 -- Primary Block has two main restrictions: min /28 (16 IPs), max /16 (65,536 IPs)
 -- Optional to add secondary IPv4
 - Optional: VPC can use IPv6 by assigning /56 IPv6 CIDR to VPC (start appliny IPv6 as default as this is what's being adopted now)
 -- IMPORTANT: You can't pick a block of IP ranges like IPv4. Your range is either allocated by AWS, or customer can use their OWN IPv6 range
 -- IPv6 doesn't have Public/Private concept, the range is all Publicly routable by default

 ### DEMO - Custom VPCs - Create VPC - DNS
 VPCs also have DNS. provided by R53
 - DNS is 'Base IP + 2', so if VPC is 10.0.0.0, then DNS IP is 10.0.0.2
 EXAM:
 - Two critical options for how DNS functions in a VPC
 -- 1. First is a setting called enableDnsHostnames - Gives instances public DNS names
 -- 2. enableDnsSupport setting. Enables DNS resolution in VPC. Indicates whether DNS is enabled or disabled in VPC. If enabled, instances in VPC can use the DNS IP address

 ## DEMO pt.1 - Custom VPCs - Create/Configure VPC
 Steps through the architecture and features of Custom VPCs including the main issues which are raised in the exam

 ### STEPS pt.1
 1. Create the VPC: VPC > Your VPCs > Create VPC > select VPC Only > name tag "a4l-vpc1" > IPv4 CIDR "10.16.0.0/16" > IPv6 CIDR block "Amazon-provided IPv6 CIDR block", default us-east-1 > Tenancy set to Default > Create VPC
 2. VPC Settings: In VPC > Actions dropdown, "Edit VPC Settings" > DNS Settings check both Enable DNS Resolution and Enable DNS Hostnames < Save (for any resources in this custom VPC, if they have puclic IP addresses, they'll also get public DNS names)

 ## DEMO pt.2 - Custom VPCs - VPC Subnets
 Subnets are what services run from inside VPCs, within a particular Availability Zone. They're how you add function, structure, and resilience to VPCs
 NOTE: With AWS diagrams, color Blue is private and Green is for Public (green = Go = Public)
 - Subnets in a VPC start off Private and take config to make Public
 - Subnets are AZ Resilient. Created within on AZ and can never be changed. If AZ fails, subnet (and any contained services) fails
 EXAM: Subnet can NEVER be in multiple AZs. 1 subnet is in 1 AZ. An AZ can have 0 or more subnets
 - Default IP for subnet is IPv4 and is allocated an IPv$ CIDR, this CIDR is a subset of the VPC CIDR Block (has to be within VPC allocated range)
 EXAM: CIDR that a subnet uses cannot overlap with any other subnets in the VPC
 - Subnet can optionally be allocated IPv6 CIDR (/64 subset of the /56 VPC, space for 256 /64 ranges that each subnet can use. Note: VPC must also be config'd for IPv6
 - By default, subnets in a VPC can communicate with other subnets in the same VPC

 ### DEMO pt.2 - Custom VPCs - VPC Subnets - Subnet IP addressing
 - 5 IPs inside every VPC subnet are RESERVED
 -- Example: Subnet is 10.16.16.0/20, range of 10.16.16.0 -> 10.16.31.255
 --- Unusable Addresses: Network Address (10.16.16.0) - NOTE: Not just AWS, NOTHING uses first address on any IP networks
 --- Unusable Addresses: 'Network+1' Address (10.16.16.1) - VPC Router; logical network device that moves data between subnets
 --- Unusable Addresses: 'Network+2' Address (10.16.16.2) - Reserved VPC address, but generally for DNS
 --- Unusable Addresses: 'Network+3' Address (10.16.16.3) - Reserved Future Use
 --- Unusable Addresses: Network Broadcast Address (10.16.31.255) - LAST IP in subnet
 EXAM: if a subnet has 16 usable IPs... it actually only has 11, because 5 are reserved (3 for AWS (+1, +2, +3, 1 network (1st IP in range), one broadcast (last IP in range))
 - Dynamic Host Configuration Protocol (DHCP). VPC has a configuration object applied to it called DHCP Option Set. It's how computing devices receive IP address  automatically. 1 DHCP option set applied to a VPC at a time and flows through to Subnets. You can create DHCP option sets, but you CANNOT edit them. To change  settings, create a new DHCP and change the VPC allocation to the new DHCP Option Set.
 - On every subnet, you can define two IP Allocation Options: 1. auto-assign public IPv4 address 2. auto-assign an IPv6 address

 ### STEPS pt.2 - Creating lots of subnets
 3. Create Multiple Subnets with VPC multi-tier structure: VPC > Subnets > Create subnet > Select VPC (a4l-vpc1) > subnet name "sn-reserved-A" > IPv4 CIDR block "10.16.0.0/20" > IPv6 CIDR block, choose the one option, fill in unique IPv6 value for the respective subnet (00 for first one) > Add New Subnet > Repeat for each subnet in the AZ (4 total) > Verify Details in each > Create Subnet. Repeat for AZB, AZC.
 4. Auto allocate IPv6 Addressing: select sn-app-A > Actions drop down, "Edit Subnet Settings" > Auto-assign IP settings, check "Enable auto-assign IPv6 address" > Save > Do this for all new subnets

 ### Custom VPCs - Resources
 - VPC Limits https://docs.aws.amazon.com/vpc/latest/userguide/amazon-vpc-limits.html
 - Architecture https://raw.githubusercontent.com/acantril/aws-sa-associate-saac03/main/0800-VIRTUAL_PRIVATE_CLOUD(VPC)/00_LEARNINGAIDS/VPCStucture-1.png
 - CIDR review: https://aws.amazon.com/what-is/cidr/
 - Subnet Calculator : https://www.site24x7.com/tools/ipv4-subnetcalculator.html


 ## VPC Routing, Internet Gateway, & Bastion Hosts
Step through the architecture and functionality of Route Tables, Routes, Associations, the internet gateway and public IP v4 functionality within a VPC

### VPC Routing
#### VPC Router
- VPC Router routes traffic between subnets. In every subnet, router has IP of network+1 address
- Every VPC has a VPC Router - Highly Available
- Controlled by Route Tables which influence what to do with traffic. Each subnet has one
- VPC created with what's known as a Main Route Table - subnet default (if you don't explicity associate a route table with a subnet, it gets the Main Route Table of the VPC).
-- A subnet can only have ONE route table associated with it at any one time. But a Route Table can be associated with many subnets
-- If multiple routes match, the prefix is used as a priority. The higher the prefix value, the more specific the route, the more priority a route has. HOWEVER, Local Routes ALWAYS have priority.
-- All VPC's have at least one route: the local route. This matches the VPC CIDR Range

EXAM: Route tables are attached to 0 or more Subnets. A Subnet HAS to have a Route Table. It's either main route table of VPC or a custom route table. A route table controls what happens to data as it leaves the subnet(s). Local Routes are always present, un-editable, and match the VPC IPv4 or 6 CIDR range. For anything else, higher prefix values are more specific and have higher priority (except Local Route which always have highest priority)

### Internet Gateway
IGW is for data to exit-to and enter-from the Public Internet. A REGIONAL RESILIENT gateway attached to a VPC

EXAM: Internet Gateway (IGW) is a REGION RESILIENT gateway attached to a VPC. A VPC can have no IGW's or ONLY 1 IGW. An IGW can be created and not attached to a
VPC (but again, it can only EVER be attached to ONE VPC at a time)

- IGW runs within the AWS Public Zone. IGW runs from the border of the Public Zone and VPC
- Gateways traffic between the VPC and the Internet/AWS Public Zone (S3..SQS..SNS..etc)
- Managed gateway; AWS handles the performance

#### Using an IGW
1. Create IGW
2. Attach IGW to VPC
3. Create custom Route Table
4. Associate Route Table to subnets
5. Then add IPv4 (and optionally IPv6) default routes to the route table with target being IGW
6. Config subnets to allocate IPv4 addressess (and optionally IPv6 addresses by Default)

### How IPv4 Addressing works inside a VPC
EXAM EXAM EXAM
Example: IPv4 EC2 Instance <-> IGW <-> Linux Update Server
- EC2 instance trying to send updates to Linux server.
-> The IPv4 instance has the private IP of 10.16.16.20, and IPv4 Public IP of 43.250.192.20. However, this isn't how it really works. what actually happens with public IPv4.. they never touch the actual services in a VPC. When you allocate a public IPv4 address, for example to this EC2 instance, a record is created which the IGW maintains, linking the instances Private IP to it's allocated Public IP
-> A packet for transit has Source and Destination IP addresses. At this point, packet is not configured with any public addressing (not currently routable accross public internet, could not currently reach the Linux update srever). Packet leaves instance, follows Default route to IGW. IGW sees packet is from EC2 based on source IP, and IGW knows the associated IPv4 address for this Source IP and changes Source address to IPv4 to be routable across internet. Linux Update server receives packet from Source IPv4 address. On the way back, the inverse happens

EXAM: At no point is the O/S on the EC2 instance aware of the public IP, it just knows of its Private IP (no IGW translation)
NOTE: Since IPv6 is publicly routable, the O/S on the EC2 instance would know it and it gets passed through IGW to sent without changing to a different IP (unlike IPv4 in the example above)

### Bastion Hosts (Jumpbox)
Bastion Hosts = Jumpbox. Entry point for private-only VPCs
- Instance in a public subnet
- Architecturally incoming managements connections arrive there
-- Once connected, can then go on to access internal-only VPC resources
- Generally the only entry point to a highly secure VPC


## DEMO - Configuring A4L public subnets and Jumpbox
Implement an Internet Gateway, Route Tables and Routes within the Animals4life VPC to support the WEB public subnets. Once the WEB subnets are public, we create a bastion host with public IPv4 addressing and connect to it to test.

** Jumpboxes are bad - but you need to understand how to spot bad things **

Currently in our VPC, all subnets are private and can't be used for communication with the internet or AWS Public Zone. We're going to reconfig the three "web" subnets to be public.

1. Create IGW: VPC > Internet Gateways > Create internet gateway > name "a4l-vpc1-igw" > Create
2. Attach IGW to VPC: In a4l-vpc1-igw, Actions dropdown "Attach to VPC" > select your VPC > Attach
3a. Make subnets Public, create Route Table (two Routes per subnet, IPv6 and IPv4): VPC > Route Tables, Create route table > Name "a4l-vpc1-rt-web" > select a4l VPC > Create
3b. Make subnets Public, config subnets: Route Table > select a4l rt > Subnet associations tab > Edit subnet associations > select web subnets (A,B,C) > Save > Routes tab
4. Add additional routes to Route Table (default routes for IPv4/6): VPC > Route Tables > select a4l rt > Routes tab, Edit Routes > Add Route > destination for IPv4 0.0.0.0/0 > target: internet gateway, select yours > Add another route, destination "::/0" (targets all IPv6), target: IGW > Save changes
5. Allocate resources with IPv4 public addresses: Subnets > select web A > ACtions > Edit Subnet Settings > check "Enable auto-assign public IPv4 address" > Save> Repeat for web B and C
6. Test configuration: EC2 > Launch Instance > name "A4L-BASTION" > Quickstart: Amazon Linux 2023 > Architecture: 64 bit, instance type: t2 micro, keypair: a4l > Netowkr Settings, VPC: A4L-VPC1, Subnet "sn-web-a", auto assign IPv4/6 "Enable", select "creat esecurity group" and name/description "A4L-BASTION-SG" > Launch Instance
7. Connect to Instance: Right-click instance, "Connect" > EC2 Connect > Connect > SSH tab, copy ssh command > Open Terminal, CD to Downloads, paste command to connect > Yes for fingerprint thing
8. Cleanup: Select A4L instance, Instance State: Terminate > VPC, select A4L vpc, Actions > Delete VPC

NOTE: When connecting to EX2 instances that have IPv4 address, you can use EC2 instance connect or Local SSH client
- Session Manager can connect you if you don't have IPv4 addressing


## Stateful vs Stateless Firewalls
TCP and IP Review: They work together.
- Transmission Control Protocol. Connection based protocol. When you make a TCP connection, each side is sending IP packets to each other (they have a srouce/destination IP). TCP is a Layer 4 Protocol that lies on top of IP. It adds error correction with the idea of ports. HTTP is TCP Port 80, HTTPS is TCP port 443

EXAM: Every CONNECTION between user/server has two parts: 1. REQUEST (initiation) 2. RESPONSE.

What actually happens:
Client pick temporary "ephemeral" port 2. client initiates server connection REQUEST using well-known port number (like Port 443 HTTPS) 3. Server RESPONDS using source port of tcp/443 and ephemeral port picked by client 4.
- Directionality depends on your perspective. What is INBOUND/OUTBOUND -- Source/Dest swap depending on who's perspective.

### Stateless Firewalls
Ex. Server is within a stateless firewall; meaning that it doesn't understand the state of connections (it sees REQUEST/RESPONSE as separate parts, so you need 2 rules needed for each connection).
- TWO Rules needed for each connection, 1 IN 1 OUT
- Because firewall is stateless, it doesn't know which specific port is used for the response. You'll often have to allow the FULL RANGE of ephemeral ports to any destination
-- This makes security engineers uneasy, which is why Stateful Firewalls are preferred.

### Stateful Firewalls
A Stateful Firewall is intelligent enough to ID the REQUEST and RESPONSE components of a connection as being related
- ONE RULE per connection; Allowing the REQUEST (inbound or outbound) means the RESPONSE (IB or OB) is automatically allowed; this reduced admin overhead and the chance for mistakes
- You DO NOT need to allow full Ephemeral Port range


## Network Access Control Lists (NACLs)
A network access control list (ACL) is an optional layer of security for your VPC that acts as a firewall for controlling traffic in and out of one or more subnets. You might set up network ACLs with rules similar to your security groups in order to add an additional layer of security to your VPC.
- NACL only impacts data crossing the subnet boundary
- NACLs are STATELESS
- Can EXPLICITLY ALLOW AND EXPLICITLY DENY; you can block specific IPs/IP Ranges associated with bad actors
- NACLS not aware of Logical Resources. They only allow you to use IP and CIDR ranges, ports and protocols

First, NACLs are associated with Subnets. NACLs work with IB and OB traffic from VPC.
- Each network ACL contains TWO sets of rules. Inbound and Outbound rules/protocols. Rules match the destination (DST) IP/Range or the DST Port, together with the protocol and ALLOW or DENY based on that match
- NACL response to client requires using the ephemeral port range (chosen at random by client/requester)
- NACLs cannot be assigned to AWS resources, ONLY subnets
- Often used together with Security Groups to add an explicit DENY. Using SGs to ALLOW traffic, NACL to DENY
- Subnet can only have ONE NACL, but a NACL can be associated with many subnets

EXAM: NACLs filter traffic crossing the subnet boundary INBOUND or OUTBOUND. NACL only impacts data crossing the subnet boundary (communications between instances in the SAME subnet is not affected.
EXAM: NACLs offer both EXPLICIT ALLOWS and EXPLICIT DENIES. Rules are processed in order, lowest rule number first. Once a match occurs, processing STOPS. * is an implicit DENY if nothing else matches
EXAM: NACLs are stateless and require TWO RULES per connection: 1x OUTBOUND, 1x INBOUND

### NACLs and multi-tiered architecture (operating across multiple subnets)
Becomes more complex with multi-tiers. Internal communications also required IB/OB rules on the app subnet NACL. If you have a CLIENT (external), a WEB subnet and APP subnet, connection rules are required for all IB/OB movements whether in between web/app subnets or between client and web subnet
- For every single communication, the rule-pairs app port (IB) and ephemeral ports (OB) are needed on each NACL for each communication type which occurs 1) within a VPC 2) TO a VPC 3) FROM a VPC

### Default NACL. Default has IB/OB Rules with implicit deny (*) and a catch-all ALLOW ALL rule (0.0.0.0/0)
### Custom NACL. Created for a specific VPC and initially NOT associated with subnets. Only ONE IB/OB rule by default: implicit deny (*)--so at first, if you associate subnets, all traffic will be denied


## VPC Security Groups (SG)
Security Groups (SGs) are another security feature of AWS VPC ... only unlike NACLs they are attached to AWS resources, not VPC subnets. SGs offer a few advantages vs NACLs in that they can recognize AWS resources and filter based on them, they can reference other SGs and also themselves. But.. SGs are not capable of explicitly blocking traffic - so often require assistance from NACLs
- SGs are STATEFUL; if you allow IB/OB request, the response is automatically allowed
- Major limitation of SGs: no explicit deny. Can be used to allow traffic or NOT Allow traffic (which is an implicit Deny). This means they can't be used to block specific bad actors
-- This is why you use NACLs in conjunction with SGs, because NACLs are used to add the explicit denies
- Supports IP and CIDR, but also allows referencing AWS Logical Resources, including other SGs and ITSELF within rules
- SGs are NOT attached to Instances/Subnets, they are attached to Elastic Network Interfaces (ENI). An instance has a primary ENI

EXAM: Security groups are attached to ELASTIC NETWORK INTERFACES (AWS Resources), not instances/subnets
EXAM: SGs cannot EXPLICITLY DENY traffic, must be paired with NACL to have an Explicit Deny

### SG - Logical References
Ex. Within VPC, we have APP and WEB subnets. Both APP and WEB are protected by SGs. External User is accessing web app via port tcp/443, allowing 0.0.0.0/0. Web to App is using tcp/1337. How do you best allow communication between WEB and APP? To take advantage of extra SG features, we could reference the web security group within the APP SG. In this, the Source for the IB Rule on APP is specifically the logical resource reference of the WEB SG
- EXAM: An SG Reference applies to anything which has the SG attached. When you're referencing an SG from another SG, you're actually referencing any resources which have the SG associated with them

### SG - Self Referencing
Ex. Private Subnet in AWS with ever-changing number of app instances. An IB Rule in each instance can have its own SG referenced, allowing traffic between any other instances with that SG.
EXAM: SG Self referencing handles IP changes automatically
EXAM: Also allows for simplified management of any intra-app communications (Eg. Microsoft Domain Controls, or apps with high availability within clusters
EXAM: SGs cannot EXPLICITLY DENY traffic. Pair with NACL to explicitly deny bad actors


NOTE: A logical resource is an abstraction that doesn't cost you anything.  It's a definition.  Something becomes a physical resource when it starts to cost you in terms of compute and store. In terms of cloud formation, you can define logical resources that are then used to create physical resources.  Within the template, you refer to things using the logical name.  Once things are deployed, you'll see deployed resources having physical IDs. In essence, a physical resource in AWS is a realized resource that consumes AWS infrastructure and services rather than a logical representation of one.


## NAT (Network Address Translation) and NAT Gateway
What is NAT? A process of giving a private resource outgoing-only access to the internet. Set of processes which adjusts IP packets by changing their source or destination IP addresses from the private IPs to the Public NAT Gateway IP
- IGW performs a "Static NAT"; how a resource can be allocated with a public IPv4 address
- IP Masquerading. A subset of NAT that hides private CIDR Blocks behind ONE IP
- NAT is many private IPs to one single IP, this is popular as IPv4 addresses are running out.
- Gives Private CIDR ranges OUTGOING internet access or AWS public services
- NAT is not required for IPv6, only IPv4. All IPv6 addresses are PUBLICLY ROUTABLE
- Need bi-directional connectivity on an instance? use IPv6 default route and point to IGW as target: ::/0 Route+IGW
- Outgoing ONLY access for an IPv6 instance? You need ::/0 Route + "Egress-Only IGW"

AWS can provide NAT services in TWO ways:
1. EC2 instance config'd with NAT (cheaper)
2. NAT Gateway - Configured inside VPC (better)

### NAT Gateway (we'll use IP Masquerading interchangeably)
NAT Gateway is provisioned into a PUBLIC subnet (like WEB subnet, in our examples), which can use public IP addresses. The Private Subnet has a route table that can point all its instances to the NAT Gateway within the WEB subnet.
- NATGW contains a Translation Table, where all required packet data is stored: IP address, src, dst, port #, etc
- Has to be run from a PUBLIC subnet (obviously). To have Public Subnets, you need an IGW, IPv4 allocation enabled on subnets, and default routes for the subnets pointing at IGW
- Elastic IPs - NAT Gateways use Elastic IPs. These are IPv4 addresses that are static and don't change. NATGW is the only AWS service that uses Elastic IPs
- NATGW's are an AZ resilient service. To attain Region Resilience, you need a NATGW in EACH AZ, and have a Route Table in each AZ with that NATGW as the target. So, for every AZ you use, you need one NAT Gateway and one Route Table pointing at said NATGW

EXAM: NATGW's are a managed service. Scales to 45 Gbps.
EXAM: NATGW's Billing: Hourly charge for running it (like 4 cents per hour, and partial hours are billed as full hours), data processing charge (per GB of processed data)
EXAM: FALSE - Exam may suggest 1 NATGW is sufficient, that 1 is regionally resilient. FALSE. If you want regional resilience, you have to deploy NATGW into each AZ you use.
EXAM: If you want to allow an EC2 instance to function as a NAT instance, Disable SOURCE/DESTINATION CHECKS
EXAM: NAT/NATGW isn't required/doesn't work with IPv6
EXAM: NATGW's are AVAILABILITY ZONE RESILIENT. If you want regional resilience, you have to deploy NATGW into each AZ you use.

### Scenarios where a NAT instance may be preferred over EC2+NATGW:
- If you value availability, bandwidth, low maintenance, and high performance choose NATGW
- NAT Instance will fail if AZ fails. A NATGW is highly available in 1 AZ--highly available (automatically recover and scale), but will still fail entirely if AZ fails entirely. For MAX Availability, have a NATGW in every AZ you use.
- If Cost is the primary issue, a NAT Instance can be cheaper. Especially at high volumes.

EXAM: NAT Instance can be used as a Bastion Server
EXAM: NATGW CANNOT be used as Bastion Server, cannot do port-forwarding, b/c you can't connect to its operating sysytem (AWS Managed)
EXAM: NATGW does NOT support Security Groups; you can only used NACLs with NATGW
EXAM: NATGW is NOT Free Tier eligible
EXAM: NAT Instances are just EC2 instances


## DEMO - NAT Gateways - Implementing private internet access using NAT Gateways
Implement a highly-available regionally resilient NAT Gateway solution within the Animals4life VPC. You will create three Nat Gateways, Route tables and Default Routes with the Nat Gateway as a target and finally associate those Route Tables with the Reserved, App and DB subnets in AZ A, B and C before testing the solution using the internal instance.

1. One-click deployment: click lesson link > acknowledge
2. Confirm resources done provisioning: CFN > Stacks Resources > A4L Resources tab > Click Instance ID for A4LINTERNATEST > On EC2, Connect to instance with Session Manager -- You'll see no internet connectoin
NOTE: Session Mgr allows connection to an EC2 instance that has no public internet connectivity
3. Connect to Internet with NATGW: VPC > NATGQ, Create NATGW > name "a4l-vpc1-natgw-A", subnet sn-web-A, Elastic IP: click 'Allocate' > Create NATGW > Repeat for B, C
4. Configure Routing, Route Table: VPC > Route Tables > Create route table > select VPC a4l-vpc1, name "a4l-vpc1-rt-privateA" > Create > repeat for B,C
5. Create Default route in each RT: select RT "privateA" > Routes tab > Edit routes > Add route > DST 0.0.0.0/0, target NATGW A > Save Changes > Repeat for B, C
6. Associate Route Table with subnets: VPC Route Tables, select web-A, Edit subnet associations > select private subnets (app, db, reserved) > Save associations > Repeat for B, C
7. Cleanup: Edit subnet associations > uncheck all > save (x3) > Delete RTs > NATGWs: actions: delete (x3) > Elastic IPs: Release (x3) > CFN: Delete A4L stack



# EC2 Basics

## Virtualization
Emulated Virtualization
Paravirtualization
Hardware Assisted Virtualization
SR-IOV

EC2 provides virtualization as a service (IaaS). It is dealing with the process of running more than one O/S on a piece of physical hardware. Within an O/S, parts of it, the kernel run in what's called Priveleged Mode -- meaning it can interact with the system's hardware. Above the O/S are applications that run in User Mode (or un-priveleged mode) (cannot interact with hardware). An app would have to make a SYSTEM CALL to the kernel to interact with hardware. IF anything but the O/S attempts to make a priveleged call, the system will detect and cause a system-wide error, generally crashing the system (or at min the app) <- THIS IS HOW IT WORKS WITHOUT VIRTUALIZATION
- Virtualization is a single piece of hardware running multiple O/S's
- Nowadays, with multiple O/S's on a single bit of hardware, all O/S's expect to be priveleged and this conflict can cause crashes -- Virtualization is the solution to this problem
- Virtualization used to have to be done as software and was slow
-- First way was EMULATED VIRTUALIZATION (included hypervisor capability performing Binary Translation, creating Virtual Machines) - super slow
-- PARA-VIRTUALIZATION. O/S's running in virtual machines, but instead of Binary Translation, they modify the guest O/S's to make Hypercalls. This requires O/S modification

### Hardware Assisted Virtualization
The major improvement to virtualization as it made the physical hardware became virtualization aware. When guest O/S's attempt priveleged instructions, they're trapped by CPU (which expects this) so the system does not halt.

### SR-IOV
Single-root IO Virtualization. Allows a network card to present itself as several "mini cards". Splits a physical card into several logical cards to present to guest O/S's

SR-IOV is a method of device virtualization that provides higher I/O performance and lower CPU utilization when compared to traditional virtualized network interfaces. Enhanced networking provides higher bandwidth, higher packet per second (PPS) performance, and consistently lower inter-instance latencies. There is no additional charge for using enhanced networking. SR-IOV enables network traffic to bypass the software switch layer of the Hyper-V virtualization stack.

### Virtualization Resources
http://www.brendangregg.com/blog/2017-11-29/aws-ec2-virtualization-2017.html


## EC2 Architecture and Resilience
Looking specifically at EC2 Hosts, how they are physically architected, why they are AZ resilient, and how the resilience of the Elastic Block Store (EBS) factors into our decisions as Solutions Architects.
- EC2 instances are Virtual Machines (VMs = O/S + Resources)
- EC2 instances run on EC2 Hosts, they're either SHARED (across different AWS customers, Shared is Default) or DEDICATED hosts
- EC2 is AZ resilient service. If AZ fails, Host Fails, Instances Fail

### EC2 Hosts
EC2 hosts have some local hardware--CPU and memory, but also local storage called Instance Store.
- They have two types of networking:
1. Storage Networking
2. Data Networking
When instances are provisioned into a specfic subnet within a VPC, a primary Elastic Network Interface is provisioned in a subnet which maps to the physical hardware on the EC2 host.
- EC2 Host can connect to the Elastic Block Store (EBS). EBS also AZ Resilient. EBS let's you allocate volumes of portions of persistent storage, and these are allocated to instances in the same AZ.
- EBS = Network based storage
- An Instance runs on a specific host and if you restart the instance, it will stay on that host. An instance will stay on a host unless one of 2 things happens:
-- 1. If the host fails or is taken down for maintenance by AWS
-- 2. If an instance is STOPPED, then restarted (different than just restarting)

EXAM: An EC2 Host runs within a SINGLE AZ. They are AZ Resilient.
EXAM: EC2 Instances are locked inside one sepcific AZ. Same with EBS volumes
- Migrations to new AZs are 'possible', but it's copying an instance into a new AZ (snapshots and AMIs)
- Instances runnings on an EC2 Host share the host's resources. You can have instances of different size sharing host, but generally same size/type of EC2 instance shares a host

### What's EC2 Good For?
For traditional style workloads, for consistency, if you require an O/S...
- Great for when you have traditional O/S+Application compute needs
- Great for Long Running Conmpute needs.
- Server style application (traditional app in an o/s awaiting incoming connections)
- Great for occasional bursts in traffic and steady state load requirements
- For monolithic application stacks
- For migrating application workloads
- Disaster Recovery (creating this dis.rec. env)


## EC2 Instance Types
EC2 instance Categories, how to decode the instance type names (family, generation, features & size), hints and tips on remembering the Instance type differences
- Reminder: EC2 instance = O/S + allocation of resources
- You can select instance type/size for more control

Choosing a different instance type influences a few things...
- The raw amount of resources you get: virtual CPU, memory, local storage capacity, and type of storage
- Resource Ratios
- Storage and Data Network Bandwidth
- Influences system architecture and vendor
- Additional feature and capabilities differ between Instance Types. Ex. allocation of GPUs, certain capacity of field programmable gate arrays (FGPAs)

### EC2 Instances - Grouped into 5 Main Categories:
1 - General Purpose (Default): Diverse workloads, equal resource ratios
2 - Compute Optimized: Designed for media processing, high performance computing, modeling, gaming, ML; access to the latest high performance CPUs. Resource Ratio where more CPU is offered the memory
3 - Memory Optimized: Inverse of Compute Optimized. Processing large in-memory datasets (Ex. in-memory caching), some database workloads
4 - Accelerated Computing: Dedicated GPUs for high scale parallel processing and modeling, custom programmable hardware known as field programmable gate arrays (FGPAs). Accelerated Computing category is often for niche requirements; you'll know when you need this category
5 - Storage Optimized: Large amounts of super fast, local storage. Massive amounts of IO operations/second, scale out transactional databases, data warehousing, Elasticsearch, analytics workloads. The Storage Optimized category is great for applications that have serious demands on sequential and random IO.

### EC2 Istance Types: Decoding the naming scheme
Ex. R5dn.8xlarge. <- Example of type of EC2 instance
- This is known as an Instance Type. If ops team member asks what instance type we need? You'd provide this full name
- Start letter, R, is the INSTANCE FAMILY
- 2nd character, 5, is the INSTANCE GENERATION. For example, a C4 would be the 4th generation of the C family of instance. Always select the most recent generation, with exception
- "8xlarge" is the size of the instance. Sizes: Nano, mirco, small, medium. large, xl, 2xl, 4xl, 8xl, and so on... Price premium on higher end... often better to scale system with large number of small sizes
- "dn" can vary... this collection of letters between family-generation and size may not always be present. These letters denote add'l capabilities. Ex. 'a' signifies AMD CPUs (you don't need to memorize these letters for the exam)

* Table / Visual of Instance Categories/Types/Details and Notes: https://imgur.com/a/LXpddQS
** 'c' stands for computer. Compute Optimized
** 'r' stands for RAM. Memory Optimized
** 'I' stands for I/O. Storage Optimized
** 'D' Dense Storage. Storage Optimized
** 'G' GPU. Accelerated Computing
** 'P' Parallel Processing. Accelerated Computing

### EC2 Instance Type Resources
- https://aws.amazon.com/ec2/instance-types/
- https://ec2instances.info/
- Table / Visual of Instance Categories/Types/Details and Notes: https://imgur.com/a/LXpddQS


## DEMO - EC2 SSH vs EC2 Instance Connect
Amazon EC2 Instance Connect provides a simple and secure way to connect to your Linux instances using Secure Shell (SSH). With EC2 Instance Connect, you use AWS Identity and Access Management (IAM) policies and principals to control SSH access to your instances, removing the need to share and manage SSH keys.

1. Make keypair for SSH: EC2 > Key Pairs, Create key pair > since we already have 'A4L' kp, we're good
2. 1-Click Deploy: Click 1-Click Deploy lesson link > Create Stack, Acknowledge, Create stack
3. Connect to Instance via SSH: EC2 > Instances > A4L, Connect, SSH Client > Open your Terminal > cd to directory with Key Pair .pem file > Paste command, Enter, 'Yes' for fingerprint
4. Connect with EC2 Instance Connect:  EC2 > Instances > A4L, Connect, EC2 Instance Connect
- NOTE: EC2 Instance Connect is not originating connections through your machine (not your IP)
5. Clean up > CFN > Delete Stack


## Storage Refresher
### Key Terms:
- DIRECT (local) attached storage: Storage on the EC2 Host
- NETWORK attached storage: Volumes are created and attached to a device over the network. In AWS, uses EBS (Elastic Block Store). Highly resilient, separate from instance hardware
- EPHEMERAL storage: Temporary storage, non-persistent. This is the Instance Store, physical storage attached to an EC2 Host
- PERSISTENT storage: Permanent storage that lives past the lifetime of an instance.
EXAM: An example of Persistent Storage in AWS is the networked attached storage delivered by EBS. Know which types of storage are Ephemeral and Persistent

### Categories of Storage:
- BLOCK storage: Create a Volume (Ex. inside EBS) that is presented to the OS as a collection of blocks; NO STRUCTURE beyond that. Mountable. Bootable.
- FILE storage: Presented as a file share/file server WITH STRUCTURE. Mountable. NOT bootable.
- OBJECT Storage: Collection of objects. NO STRUCTURE; flat. NOT mountable. NOT bootable.

### Storage Performance
These items don't exist in isolation. IOPS is like speed of engine a racecar runs at (revolutions per second), IO block size is like the size of the car's wheels, throughput is the top-speed of the racecar.
- IO BLOCK SIZE: Size of the data you're writing to disk.
- IOPS: Measures the number of I/O operations a storage system supports in a second (how many read/writes in a second)
- THROUGHPUT: Amount of data that can be transferred in a given second, MB/s.
* IO x IOPS = Throughput
** Ex. 16KB IO block size x 100IOPS = 1.6MB/s throughput


## EC2 - EBS Service Architecture
Amazon Elastic Block Store (Amazon EBS) provides block level storage volumes for use with EC2 instances. EBS volumes behave like raw, unformatted block devices. You can mount these volumes as devices on your instances. EBS volumes that are attached to an instance are exposed as storage volumes that persist independently from the life of the instance. You can create a file system on top of these volumes, or use them in any way you would use a block device (such as a hard drive).
- EBS can be encrypted using KMS
- When you attach a volume to an EC2 instance, the instance sees a Block Device, so raw storage.
- EBS volumes appear just like any other storage device to an EC2 instance
- EBS Volumes are attached to ONE instance at a time. However, can be detached and re-attached to a new instance. They are not lifecycle linked to one instance, they're persistent; if an instance moves to a new EC2 host, the volume follows it. EBS is persistent until you delete the volume (separate from the instance)
- Snapshot into S3: You can create a backup of a volume with a Snapshot into S3. This can be used to migrate volumes between AZs.
- EBS can provision volumes based on different physical storage types: SSD, high-performance SSD, volumes based on mechanical disks, different size volumes, different performance profiles
- BILLING: Gigabyte/Month metric (and in some cases, performance)

EXAM: Storage is provisioned in ONE AVAILABILITY ZONE; Resilient in that AZ
EXAM: Snapshots are now REGIONALLY RESILIENT


### EBS Example - 1 region, 2 AZs (AZA, AZB), 1 S3 bucket.
EBS is AZ-based. So, with two AZs you have two separate EBSs. Same as EC2 hosts--per AZ
- EBS replicated data within an AZ. Failure of an entire AZ means failure of all volumes in that AZ. To fight this, you can Snapshot volumes into S3, creating more resilience, and you can create another volume in a new AZ from this snapshot (or even to a new region)
- For Global Resilience on volumes, copy snapshots over to different regions


## EC2 - EBS Volume Types
General Purpose SSD — Provides a balance of price and performance. We recommend these volumes for most workloads.
- Volumes can very in size from 1GB -> 16TB
- When created, a volume is given an I/O credit allocation

### EBS Volume Types - General Purpose (GP):
1. GP2. GP2 is the default general purpose SSD based storage provided by EBS. CREDIT ARCHITECTURE
- GP2 gets 3 IO credits per second, per GB of volume size
- "Burst Rate": GP2 volume can burst up to 3,000 IOPS
- Max IOPS for GP2 is currently 16,000 IO credits per second (baseline performance) - Any volumes > 5.33TB in size achieves this rate constantly
- Great for: boot volumes, low latency interactive apps, dev/test environments
- GP2 auto scales on size

2. GP3. SSD based, but removed the credit architecture GP2
- Every GP3 volume, regardless of size starts with 3,000 IOPS and 125MiB/s
- ~20% cheaper than GP2
- Need more performance? Can pay for up 1o 16,000 IOPS or 1,000 MiB/s
- GP3 does NOT auto-scale, you have to enable the upgrades

#### IO Credit. When you create a volume (size ranging from 1GB -> 16TB), it is created with an IO credit allocation.
- An IO is one input/output operation
- IO credit is a 16KB chuck of data
- An IOP is one chuck of 16KB in one second
- Ex. If transferring a 160KB file, that's 10 IO blocks of data. If this is all done in 1 second, that's 10IOPS. (IO x IOPS = Throughput -> 10 x 1 = 10IOPS)
- 1 IOPS is 1 IO in 1 second
- IF you have NO credits in your IO "bucket" in the volume, you can't perform any IO on the disc
- IO Bucket has capacity of 5.4 million IO credits and "Fills at the rate of Baseline Performance"
- "Fills at the rate of Baseline Performance"... what does this mean? Every volume has baseline performance based on size, with a minimum
-- IO Bucket bills with minimum of 100 IO Credits per second REGARDLESS OF VOLUME SIZE

## EC2 - EBS Volume Types - Provisioned IOPS (io1, io2, io2 Block Express)
Provisioned IOPS SSD — Provides high performance for mission-critical, low-latency, or high-throughput workloads.
- Three types of provisioned IOPs SSD: io1, io2, io2 Block Express
- IOPS are configurable independent of volume size and designed for super high-performance situations
- Max 64,000 IOPS/volume
- io1/io2, 1,000MB/s throughput
- io2 Block Express: 256,000 IOPS, 4,000MB/s throughput
- Size: 4BG -> 16TB for io1/io2. io2 Block Express 4GB -> 64TB
- Size-to-performance ratio maximums: io1 50IOPS/GB, io2 500IOPS/GB, io2 Block Express 1000IOPS/GB
- Per Instance Performance restriction: the max performance between the EBS svc and an EC2 instance
- NUMBERS (all the specs for Provisioned IOPS): https://imgur.com/a/zYQk7G1

EXAM: Provisioned IOPS: Most consistent low latency and jitter.
EXAM: Prov.IOPS for sub-millisecond latency, consistent latency, and higher performance.


### EC2 - EBS Volume Types - HDD-Based*
* Slower, only for specific situations
Types:
1. Throughput Optimized HDD (st1) — A low-cost HDD designed for frequently accessed, throughput-intensive workloads. For sequentially accessed data like streaming
-- Big data, data warehouses, log processing
2. Cold HDD (sc1) — The lowest-cost HDD design for less frequently accessed workloads.
-- geared for max economy (lowest EBS cost option) with lowest performance

HDD Based EBS Volume Type METRICS: https://imgur.com/a/EcGVrx8


## EC2 - Instance Store Volumes - Architecture
An instance store provides TEMPORARY block-level storage devices for your instance. This storage is located on disks that are physically attached to the host computer. Instance store is ideal for TEMPORARY storage of information that changes frequently, such as buffers, caches, scratch data, and other temporary content, or for data that is replicated across a fleet of instances, such as a load-balanced pool of web servers.

An instance store consists of one or more instance store volumes exposed as block devices. The size of an instance store as well as the number of devices available varies by instance type.

The virtual devices for instance store volumes are `ephemeral[0-23]`. Instance types that support one instance store volume have ephemeral0. Instance types that support two instance store volumes have `ephemeral0` and `ephemeral1`, and so on.

- ISV = HIGHEST STORAGE PERFORMANCE in AWS
- Physically connected to ONE EC2 host - isolated to host
- If instance moves between host, data that was stored on attached ephemeral[X] is lost and instance is re-attached to new ephemeral[X]
- Instance Store Volumes should NOT be used for anything the requires persistence
- More IOPS and Throughput VS EBS

EXAM: Local to an EC2 Host
EXAM: Data stored on Instance Store Volumes is lost on instance MOVE, RESIZE, or HARDWARE FAILURE
EXAM: HIGHEST STORAGE PERFORMANCE storage option in AWS, but can't provide persistence. TEMPORARY, for replaceable data
EXAM: Instance Store Volumes have to be ATTACHED AT LAUNCH OF INSTANCE, cannot happen after. Instances on this host only can access them

## Choosing between the EC2 Instance Store Volumes (ISV) and EBS
Resource: https://aws.amazon.com/ec2/instance-types/

Need...
Persistence? EBS (avoid ISV)
Resilience? EBS (avoid ISV)
Isolated from Instance Life Cycles? (to be able to un-attach and re-attach) EBS (avoid ISV)
Resilience w/App In-Built Replication... it depends
High Performance? Depends (ISV is super high performance)
Cost is main factor? ISV (it's often included in the price)

REMEMBER ALL OF THIS:
EXAM: Cost Efficacy? ISV ST1 or ISV SC1. For throughput + streaming? ST1
EXAM: Boot EC2 instances? NOT st1 or sc1
EXAM: GP2 / GP3: Has a max performance of 16,000 IOPS
EXAM: IO1 / IO2: Has max 64,000 IOPS (256,000 IOPS in io2 Block Express) - Max EBS performance with large instance (that is capable of providing this performance)
EXAM: RAID0 + EBS: Has max 260,000 IOPS
EXAM: Need anything greater than 260,000 IOPS? use ISV, not EBS. *No persistence
EXAM: EBS Automated Backups? Amazon Data Lifecycle Manager: To automate the creation, retention, and deletion of Amazon EBS snapshots

TL;DR EBS Volume VS Instance Store
- EBS volume is network attached drive which results in slow performance but data is persistent meaning even if you reboot the instance data will be there.
- Instance store instance store provides temporary block-level storage for your instance. This storage is located on disks that are physically attached to the host computer.
-- Data on an instance store volume persists only during the life of the associated instance; if an instance is stopped or terminated, any data on instance store volumes is lost.

SSD: General Purpose (gp2, gp3), Provisioned IOPS SSD volumes (io1, io2, io2 Block Express)
HDD: st1, sc1

## EC2 - EBS Snapshots, Restore & Fast Snapshot Restore (FSR)
- EBS Snapshots are backups of data consumed within EBS Volumes - Stored on S3.
- Snapshots are incremental, the FIRST COPY being a full backup - and any future snapshots being incremental. No massive risk of losing incremental backups (each increment is self-sufficient)
- Snapshots can be used to migrate data to different availability zones in a region, or to different regions of AWS.
- AZ Resilient (vulnerable to issues which impact entire AZ), but with a snapshot the data becomes Region Resilient
- Good for EBS Volume cloning, even moving / copying them across AZs
- BILLING: Gigabyte-month cost; but you're only paying for USED data, not allocated data

EXAM: Snapshot doesn't need to be initialized in a new EBS Volume, it's built-in
EXAM: Snapshots are restored LAZILY; fetched gradually
EXAM: Requested blocks are fetched immediately, you can do this initially to force rapid initialization so users have quickest access up front
EXAM: Fast Snapshot Restore (FSR): A setting to Enable that allows immediate restores instead of gradual
EXAM: Up to 50 FSRs per region. Set on the Snap & AZ, so 50 between AZs
EXAM: FSR costs extra


## DEMO - EC2 -  EBS Volumes
Commands for Terminal: https://learn-cantrill-labs.s3.amazonaws.com/awscoursedemos/0004-aws-associate-ec2-ebs-demo/lesson_commands.txt
1. Create an EBS Volume: 1-Click Deploy link > Create Stack > EC2 EBS > Create Volume > select GP2, 10 GiB size, AZ us-east-1a, tag: kay "Name" value "EBSTestVolume" > Create
2. Mount it to an EC2 instance: Select new EBS Volume > Actions: Attach Volume > Choose Instance1 > Attach
3. Create and Mount a file system: Ec2 Instance > select A4L-EBS-INSTANCE1-AZB, Connect > EC2 Instance Connect > `sudo mkfs -t xfs /dev/xvdf`, Enter
4. Generate a test file: EC2 Connect > `sudo mkdir /ebstest`, Enter > Mount dev/xvdf to /ebstest directory `sudo mount /dev/xvdf /ebstest` > cd /esbstest > `sudo nano amazingtestfile.txt` > write text, ctrol+o, enter, ctrl+x > Reboot instance `sudo reboot`
5. Migrate volume with Snapshot: EC2 > Instances > Stop AZA Instance 1 and 2 > when stopped, Volumes: Detach Volume > right click EBS Volume, Create Snapshot > Right click Snapshot, Create Volume from Snapshot > Zone us-east-1b > Tag key "Name" value "EBSTestVolume-AZB" > Create
6. Attach Volume to AZB instance: Volume > right click, Attach > ABZ Instance 1 > ATtach
7. Verify the filesystem and file are intact > EC2 Instance Connet on AZB Instance 1 > `lsblk` > `sudo mkdir /ebstest` > `sudo mount /dev/xvdf /ebstest`
8. Stop AZB Instance > Detach EBS Volume
9. Clean up > Detele Snapshopt > Volumes: delete test volumes > CloudFormation: Delete Stack
* The remaining DEMO is not FREE TIER
* On Instance Store Volumes, Instance reboot does not cause the data to be lost or moving to new host, but a Stop/Start changes hosts and you lose data


## EC2 - EBS Encryption
EBS Encryption provides AT REST encryption for volumes and snapshots.
- Uses KMS: AWS/EBS Keys or Customer Managed Keys
- Uses DEK

EXAM: AWS Accounts can be set to encrypt by default - Default KMS Key
EXAM: Each Volume uses ONE unique DEK. Snapshots and future volumes use the SAME DEK. Volume from scratch? New DEK
EXAM: There is NO WAY To remove an encryption from a volume, unless you clone data to a new volume
EXAM: O/S is not aware of the encryption (no performance loss)


## EC2 - Networks Interfaces, Instance IPs and DNS
Elastic Network Interfaces (ENIs) which can be allocated to EC2 instances - and the DNS, public, private and elastic IPs which can be assigned to those ENIs
- Each EC2 Instance starts with one ENI (primary ENI). You can attach more ENI's, but to different subnets
- Lots of things are attached to ENIs and not instances: Security groups, lots of IP stuff, Source/Destination checks
- You can detach secondary ENIs and move them to different instances
- ENIs contain...
-- Primary Private IPv4 address
-- Secondary Private IPv4 address
-- Optionally, 1 public IPv4 address
-- Optionally, 1 or more Elastic IP addresses

### EC2 - Elastic IP address
Allocated to your AWS account. If Elastic IP assigned, it removes the Public IPv4 and replaces with the Elastic IP

EXAM: If you assign Elastic IP and remove it, can you get the original, replaced IPv4 address back? NO, you get a different one back
EXAM: Secondary ENIs + MAC addresses = Licensing that can move between instances
EXAM: Multi-homed (subnets) Management & Data: An instance with an ENI in two different subnets (maybe use one for management and one for data)
EXAM: Security Groups are attached to ENIs, not instances. Different rules needed for different groups? Set up multiple ENIs with SGs on each
EXAM: THE OPERATING SYSTEM NEVER SEES THE PUBLIC IPv4; it's configured on the ENI
EXAM: IPv4 Public IPs are DYNAMIC... Stop/Start instance means IP de-allocation/changes. Restarting instance maintains same IP. To avoid this, assign Elastic IP address
EXAM: Public DNS given to the instance for the public IPv4 IP address resolves to the PRIMARY PRIVATE IPv4 address from within the VPC. This happens so that if you've got instance-to-instance communication, it never leaves the VPC. Outside the VPC, DNS will resolve to the PUBLIC address


## DEMO - EC2 -  Manual Install of Wordpress on EC2 - NOTE-INCOMPLETE DEMO, IT BROKE
Use EC2, install MariaDB, Apache & libraries and then download and install wordpress.
- Learning how NOT to do things through a manual installation

Steps:
1. 1-Click Deployment in lesson > Wait for stack to hit CREATE COMPLETE
2. Install WP: EC2 > Instances Running > right-click A4L, Connect, Instance Connect
3. Create Variables in Console >
DBName='a4lwordpress'
DBUser='a4lwordpress'
DBPassword='4n1m4l$4L1f3'
DBRootPassword='4n1m4l$4L1f3'
> Paste each, press Enter, paste the next, Enter
4. Install system software - including Web and DB: `sudo yum install -y mariadb-server httpd wget` > install PHP/MariaDB `sudo amazon-linux-extras install -y lamp-mariadb10.2-php7.2 php7.2`
5. Web and DB Servers Online - and set to startup:
sudo systemctl enable httpd >
sudo systemctl enable mariadb >
sudo systemctl start httpd >
sudo systemctl start mariadb
6. Set Mariadb Root Password: `mysqladmin -u root password $DBRootPassword`
7. Install Wordpress: `sudo wget http://wordpress.org/latest.tar.gz -P /var/www/html` > `cd /var/www/html` > `sudo tar -zxvf latest.tar.gz` (to extract tar file) > `sudo cp -rvf wordpress/* .` (copy data from WP file to current file '.') > `sudo rm -R wordpress` > `sudo rm latest.tar.gz`
8. Configure Wordpress:
sudo cp ./wp-config-sample.php ./wp-config.php (rename template config file to be actual) >
sudo sed -i "s/'database_name_here'/'$DBName'/g" wp-config.php (search and replace to update config file >)
sudo sed -i "s/'username_here'/'$DBUser'/g" wp-config.php >
sudo sed -i "s/'password_here'/'$DBPassword'/g" wp-config.php >
sudo chown apache:apache * -R (making sure web server has access to all file folders, owned by apache)
9. Create Wordpress DB:
echo "CREATE DATABASE $DBName;" >> /tmp/db.setup (create WP DB) >
echo "CREATE USER '$DBUser'@'localhost' IDENTIFIED BY '$DBPassword';" >> /tmp/db.setup >
echo "GRANT ALL ON $DBName.* TO '$DBUser'@'localhost';" >> /tmp/db.setup >
echo "FLUSH PRIVILEGES;" >> /tmp/db.setup >
mysql -u root --password=$DBRootPassword < /tmp/db.setup
sudo rm /tmp/db.setup
*** UNSUCCESSFUL DEMO--Somewhere this messed up and the system couldn't see tmp/db.setup, then it could, so the commands got duplicated -
10. Clean up Account: CFN > delete stack


## EC2 - Amazon Machine Image (AMI)
Amazon Machine Images (AMI) are the images which can create EC2 instances of a certain configuration. In addition to using AMI's to launch instances, you can customize an EC2 instance to your bespoke business requirements and then generate a template AMI which can be used to create any number of customized EC2 instances.
- AMIs are used to launch EC2 instances, even the Default EC2 instance launch is used via AMI. AMI's can be AWS or Community Provided
- Marketplace AMIs are available
- AMIs are REGIONAL... Unique ID for each AMI in each region Eg. "ami-0a887...."
- AMI controls permissions (scope: Public, Your Account, Specific Accounts)
- Not only can you create EC2 Instance from AMI, can create AMI from EC2 instance you want to template
- BILLING: billed for the storage cost... the data of the EBS snapshots contained

AMI Lifecycle:
1. Launch Instance: AMI launches EC2 instance.
2. Configure Instance: Can take launched instance and provide customizations (Eg. O/S, instance with config'd volumes, etc).
3. Create New AMI: Can create an AMI from your configured/customized Instance (make a template)
4. Launch NEW Template instance: Launch new instance with templace AMI

EXAM: AMI = ONE REGION. Only works in that region
EXAM: AMI Baking: Creating an AMI from a configured instance + application
EXAM: AMI CAN NOT be edited. Instead, launch instance, change configs, make new AMI
EXAM: AMI CAN be COPIED between regions (includes its EBS Volume Snapshots)
EXAM: Default AMI permissions: Default is your account only. (Can be private, public, or grant access to specific accounts)


## DEMO - EC2 -  Creating A4L AMI (AMI Baking)
Create WP EC2 instance. Improve EC2 login screen. Create AMI from custom instance and deploy a new instance.

Steps:
1. Set up WP Instance: https://learn-cantrill-labs.s3.amazonaws.com/awscoursedemos/0007-aws-associate-ec2-ami-demo/lesson_commands.txt > Create Stack
***UNSUCCESSFUL DEMO: Failed to complete. Cantrill says it works but I couldn't get it


## EC2 Purchase Options (Launch Types)
ON-DEMAND: Default/Shared. Per second billing. Resources like consume capacity bill regardless of instance state. Price defined up front, no discounts
-- Suitable for short term workloads, or unknown workloads

SPOT: Spot pricing is AWS selling unused EC2 Host Capacity for up to 90% discount. Spot price based on the space capacity at a given time
-- Customer sets max price they're willing to pay. If a Spot price exceeds your max willing payment, you'll lose the Spot
-- NEVER use a Spot for workloads which can't tolerate interruptions
-- Best for things that are non-time critical. Anything which can tolerate interruption and just be rerun. Anything that has a bursty capacity need.

RESERVED: Form a part of most larger deployments in AWS. For long-term, consistent usage of EC2. Purchase a reservation to remove/reduce the per second price.
-- An unused reservation is still billed. Can be locked to AZ or region. Partial coverage of a larger instance, not billed for full thing.
-- Reservations terms: 1 year or 3 years. You pay for the entire term up front (no per/s fee, greatest discount of all reserved options). Or Partial Upfront, or No-Upfront (per/s fee)
-- For when you need lowest cost, consistent usage, and can't tolerate any interruption

DEDICATED INSTANCES: Instances run on an EC2 host that you don't own or share. Extra charges for instances, but dedicated hardware
-- Fees: 1 off hourly fee for any regions using dedicated instances. Fee for the instances themselves
-- For when you can't share infrastructure

DEDICATED HOST: EC2 host allocated to you in its entirety. You need to manage capacity, however, and unused capacity is wasted.
-- 'Host Affinity' links instances to hosts
-- For Strict Licensing requirements. Reason to use this purchase option: For socket and core licensing requirements
-- You pay for the HOST, no instance charges.

EXAM: On demand, reserved, spot


## EC2 - Reserved Instances - The Rest
Scheduled Reserved Instances, the differences between zonal and regional reservations and on-demand capacity Reservations. For if you need access to the cheapest EC2 that runs 24/7/365.

### Scheduled Reserved Instances: For long term useage which doesn't run constantly. Eg. Batch processing running daily for 5 hours. Eg 2 weekly data, like every friday for 24 hours
- DOES NOT support all instance types
- 1,200 hours min per year (100 hours per month)
- 1 year minimum

### Zonal: Only applies to one Availability Zone, providing billing discounts and capacity reservation in that one AZ
- 1 or 3 year term

### Regional: Provides a billing discount for valid instances launched in any AZ in that region
- While flexible, they don't reserve capacity within an AZ, which is risky during major faults when capacity can be limited
- 1 or 3 year term

### On-Demand Capacity Reservations: Can be booked to ensure you always have access to capacity in an AZ when you need it, but at FULL ON-DEMAND price.
- NO TERM LIMITS, but you pay whether or not you use it

### Savings Plan: Kind of like a reserved instance purchase, but instead of particular type of instance, it's a 1 to 3 year commit to AWS in terms of hourly spend. Eg. Minimum spend 20$/hr for 1 or 3 years, you get a reduction in price. If you go above your savings plan ($20), you begin paying
- Can make a reservation of general compute amounts, 60% discount
- EC2 savings plan, which must be used for EC2 but 72% discount
- General Compute valid for things like EC2, fargate, lambda. These products have both on-demand rate and savings plan rate


## EC2 - Instance Status Checks & Auto Recovery
Amazon EC2 performs automated checks on every running EC2 instance to identify hardware and software issues. You can view the results of these status checks to identify specific and detectable problems.

You can create an Amazon CloudWatch alarm that monitors an Amazon EC2 instance and automatically recovers the instance if it becomes impaired due to an underlying hardware failure or a problem that requires AWS involvement to repair.
- Terminated instances cannot be recovered.
- A recovered instance is identical to the original instance, including the instance ID, private IP addresses, Elastic IP addresses, and all instance metadata

### Short Demo - When you first start an instance, these are the "2/2 checks passed"
Each of these checks is a separate set of tests.  First, system status check. Second, instance status check.
- If there's a failure, you can set Auto Recover and other actions. Other actions like setting notification alarms (you can include actions in this alarm; recover, reboot, stop, terminate)
- Auto-Recovery ONLY works on EBS Volumes, not instance store


## DEMO - EC2 - Shutdown, Terminate & Termination Protection
Right-click instance > Instance Settings > Change Termination Protection > Enable
- role separation: can permit users to disable termination protection, and permit users to terminate
- Error if not permitted: "Failed to terminate instance: The instance [id] may not be terminated. Modify its 'disableApiTermination' instance and try again"


## EC2 - Horizontal & Vertical Scaling
Two ways which systems have to deal with increasing or decreasing user-side load. Each has pros and cons but handles the act of scaling radically differently.
- Adding or removing resources from a system

### Vertical Scaling
Resizing an EC2 instance when you scale, which can cause DOWNTIME. Can only scale during pre-agreed times, like outage windows, which can cause DISRUPTION
CONS: Larger instances carry a premium. There is an upper cap on performance; instance size
PROS: No app modification required. Works for ALL applications, even monoliths (since it all runs on one instance)

### Horizontal Scaling
Instead of increasing the size of the instance, HS adds more instances.
- Many copies of the instance running together and sharing the load; need LOAD BALANCER
- It's all about SESSIONS (state of your interaction with a session, like browsing YouTube). With HS, sessions don't work great since you move between instances during your interaction
CONS: Requires off-host sessions to save Session data. HS instances are 'dumb' instances
PROS: Balances / Evens out the load. No disruption while scaling, even when scaling down. No real limit to scaling horizontally. Often less expensive (since using many small instances). More granular; can increase in smaller increments.


## EC2 - Instance Metadata - EXAM
Instance metadata is data about your instance that you can use to configure or manage the running instance. Instance metadata is divided into categories, for example, host name, events, and security groups.
- EC2 svc provides data to instances. Accessible to all instances.


EXAM: IP Address to access Instance Metadata: 169.254.169.254
- URL http://169.254.169.254/latest/meta-data/
EXAM: Meta data service is NOT AUTHENTICATED and NOT ENCRYPTED; anyone who can connect to an instance and gain access to Linux Shell can access meta data

### DEMO - Instance Metadata
1. 1-Click Deploy. 2600:1f18:5421:7603:dc5e:6920:45eb:8f84
Commands for EC2 Connect session: https://learn-cantrill-labs.s3.amazonaws.com/awscoursedemos/0009-aws-associate-ec2-instance-metadata/lesson_commands.txt
2. Download Instance Metadata functionality:
- wget http://s3.amazonaws.com/ec2metadata/ec2-metadata (download)
- chmod u+x ec2-metadata (make usable)
- ec2-metadata --help (see list of commands)

EXAM: Never within lifecycle of instance is the public IPv4 address within the O/S. Remember, the internet gateway handles the public IPv4
- Can use meta data commands to make public IP visible
