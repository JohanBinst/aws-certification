# 13 - Advanced Storage

## EFS
The Elastic File System (EFS) is an AWS managed implementation of NFS (NFSv4) which allows for the creation of shared 'filesystems' which can be mounted within multi EC2 instances. By doing so EC2 instance becomes more stateless.
- For scalability / resiliency
- EFS is an implementation of NSFv4 (network file system version 4)
- Can be mounted in EC2 linux and **shared** between many EC2 instances
- EFS is private service
- EFS is accessed using mounts targets inside a VPC (mount targets run from subnet inside VPC) -> for HA you need mount target in every AZ you use
- Can be accessed from on-premises via VPN or AWS Direct Connect (DX) -> connect also using mount target via VPN or DX
- Uses POSIX permissions (a linux thing)

- EXAM: EFS is Linux ONLY
- EXAM: 2 performance modes: 
    1. General Purpose (default): latency intesive use cases, web servers, Content Management Systems (CMS), home directories or general file servers
    2. Max I/O : high IOPS but tradeoff is increased latency. Use for Big Data media processing
- EXAM: 2 throughput modes: 
    1. Bursting : throughput scales with file system size: the more data you store the more capacity you need and throughput performance increased with size.
    2. Provisioned : pay for fixed throughput independant of filesharing size
- EXAM: 2 storage classes: 
    1. Standard (default)
    2. Infrequent Access (IA) - Lifecycle policies can be used with these

## DEMO - Implementing EFS
Implement a simple EFS file system in a VPC, configure mount targets and configure two EC2 instances to mount the file system within a mount point.

Video: https://learn.cantrill.io/courses/1820301/lectures/41301666

Steps:
1. 1 click deploy
2. Create EFS: EFS > Create File System > Customize > name "A4L-EFS", storage class Standard, disable Encryption of data at rest, pPrformance Settings: Bursting > Next
3. EFS Network Settings: Create mount targets > Delete default SG's (blue bloxes) > Attach APP subnets: us-east-1a, "sn-app-A" etc > Security Group x3 "IMPLEMENTINGEFS[...]" > Next > Skip File System policy (optional) > Next > Review and CREATE
NOTE: any AZs within a VPC you're consuming the services provided by EFS, you should be creating a mount target
4. EC2 Instances > duplicate EC2 instance tab > tab 1, EC2 connect to instance A, tab 2 connect to B
5. EC2 Connect Instance A > `sudo mkdir -p /efs/wp-content` (creates file as well as any paths like /efs/ with the -p) >
`sudo dnf -y install amazon-efs-utils` package of tools which allows this instance to interact with EFS >
`cd /etc` >
`sudo nano /etc/fstab` >
Paste this into 3rd line of nano: `file-system-id:/ /efs/wp-content efs _netdev,tls,iam 0 0` >
6. Paste EFS file system ID of A4L EFS into the nano text above, replacing 'file-system-id`
7. Save Nano: ctrl+o to save, Enter, ctrl+x to exit
8. `df -k` still not showing anything. Time to mount file system: `sudo mount /efs/wp-content`, now `df -k` will show it >
`cd /efs/wp-content` (move into new file system) >
`sudo touch amazingtestfile.txt` (create test file)
9. Instance B Connect:
df -k >
sudo dnf -y install amazon-efs-utils >
sudo mkdir -p /efs/wp-content >
sudo nano /etc/fstab >
file-system-id:/ /efs/wp-content efs _netdev,tls,iam 0 0 >
sudo mount /efs/wp-content >
cd /efs/wp-content/ >
ls -la -- you'll see amazingtestfile.txt in the directory which was created in instance A
10. Clean up: EFS > Delete file system > Cloudformation > Delete stack

## FSx for Windows Servers
FSx for Windows Servers provides a native windows file system as a service which can be used within AWS, or from on-premises environments via VPN or Direct Connect
- FSx is an advanced shared file system accessible over SMB, and integrates with Active Directory (supports AWS MS Active Directory or on-premise Active Directory).
- It provides advanced features such as Data de-duplication, backups, encryption at rest and forced encryption in transit and VSS (user driven resotores of previous version)
- Integrats with Directory Service or Self-Managed Active Directory
- Single or Multi-AZ mode within a VPC
- can do on-demand or scheduled backups
- accessible using VPC, peering, VPN, Direct Connect
- FSx is fileshare system dedicated to Windows Environments, the similar EFS is for Linux/Unix
- File level versioning; support volume shadow copies; file-level restores

EXAM - Key words to look for:
- VSS (user driven restores)
- native file system over SMB (SMB=windows)
- uses Windows permissions model of folders and files
- supports DFS (distributed file system) -> scale-out easily file share structure easily in Windows enivironment
- integrates with Directory Service and YOUR OWN directory

## FSx For Lustre
FSx for Lustre is a managed file system which uses the FSx product designed for high performance computing on Linux clients (POSIX)
- It delivers extreme performance for scenarios such as BIG DATA, MACHINE LEARNING and FINANCIAL MODELING
 - FSx for Lustre is a managed Lustre high compute system. Linux clients (POSIX)
- Two deploment types: Persistent or Scratch
 - Scratch: highliy optimized for short-term. No replication and fast. not HA
 - Persistent: Longer term, high avail in one AZ, self-healing
- Accessible over VPN or Direct Connect
EXAM - If Lustre, POSIX mentioned... FSx for Lustre, ML/big data/fin-modeling, SageMaker

## FSx vs EFS

