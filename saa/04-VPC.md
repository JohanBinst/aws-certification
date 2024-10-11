# VPC
## VPC Sizing and structure

## Custom VPC's

## VPC subnets
Subnets are what AWS services run from inside the VPC's and are used to add structure, functionality and resilience to your VPC's.

Subnets when created in AWS are private by default and can be made public through configuration.

- A subnet is a subnetwork of a VPC within a particular Availabilty Zone (if AZ fails, subnet fails and so all ressources in that subnet fail).
1 Subnet is in 1 Availability Zone (important for exam) and can never be in more than 1 AZ. But 1 AZ can have multiple subnets.
- The IPv4 CIDR block is a subset of the VPC CIDR block.
- The IPv4 CIDR block of the subnet can't overlap with a CIDR block of another subnet in the same VPC.
- IPv6 CIDR blocks are also supported if enabled on the VPC. Default is /64 subset of the /56 VPC block.
- Subnets can communicate with other subnets in the same VPC by default.

### Subnet IP adressing
- Every subnet has 5 IP addresses reserved by AWS:
  - Network address (the first IP address of the subnet: x.x.x.0)
  - VPC router (the second IP address of the subnet: x.x.x.1 Network +1)
  - DNS server (the third IP address of the subnet: x.x.x.2 Network +2)
  - Reserved by AWS for future use (the fourth IP address of the subnet: x.x.x.3 Network +3)
  - Network broadcast address (the last IP address of the subnet: x.x.x.255)

## VPC Routing, Internet Gateway and Bastion Hosts
- Every VPC has a VPC router that is highly available and managed by AWS. It runs in all the AZ that the VPC uses.
- A VPC has a Main route table and the optional subnet route table can be associated with the main route table. A subnet can only be associated with one route table at a time. But a route table can be associated with multiple subnets.
The destination column in a route table is the CIDR block of the destination network. The target is the target for the traffic. The target can be:
  - Local: The subnet itself
  - Internet Gateway: The internet
  - Virtual Private Gateway: A VPN connection
  - Direct Connect Gateway: A Direct Connect connection
  - Peering Connection: A VPC peering connection
  - NAT Gateway: A NAT gateway
  - Egress Only Internet Gateway: An egress-only internet gateway
  - Gateway VPC Endpoint: A gateway VPC endpoint
  - Interface VPC Endpoint: An interface VPC endpoint
  - VPC Endpoint Service: An endpoint service
  - Prefix List: A prefix list

The priority of the route is determined by the most specific route. If there are multiple routes that match the same destination, the most specific route is used. For example if there is a route for 0.0.0.0/0 (all IP adresses) and a route for 127.31.0.0/16, the route for 127.31.12.25 will be the 127.31.0.0/16 as it is more specific.
==> Higher prefix values are more specific = higher priority (/32 is 1 IP address so it is the most specific)

### Internet Gateway
- An Internet Gateway is a **regional resiliant** service that allows communication between instances in your VPC and the internet. ***Exam tip: You don't need an internet gateway per AZ as it is a regional service.***
- 1 to 1 relationship between a VPC and an Internet Gateway. A VPC can have 0 to 1 Internet Gateway and an Internet Gateway can be attached to 0 to 1 VPC.
- The internet gateway runs from within the AWS public zone and thus allows services in the VPC to communicate with the internet using public IP addresses.
- IGW is managed by AWS so AWS manages the performance

Using an Internet Gateway:
1. Create an Internet Gateway
2. Attach the Internet Gateway to the VPC
3. Create custom route table
4. Associate the route table with the subnet
5. Add a default route (0.0.0.0/0) that points all traffic to the Internet Gateway
6. Subnet allocate IPv4 (or IPv6) public IP addresses to instances (Nakijken want niet duidelijk)

### IPv4 addressing
The service in the subnet is **never aware** of it's public IPv4 address. The Internet Gateway uses a record to translate the public IPv4 address to the private IPv4 address of the instance.
**Exam tip:** Never be tricked to try to assign the public IPv4 address of an EC2 instance directly to the Operating System. The OS is never aware of the public IP address. **The public IP address is managed by the Internet Gateway.**

### IPv6 addressing
IPv6 addresses are public by default and are assigned to the instance directly. The instance is aware of it's public IPv6 address. The Internet Gateway is just passing the traffic to the instance, it's not doing any translation.

### Bastion Hosts and Jump Boxes
Bastion hosts are instances that sit in a public subnet inside a VPC and are used to manage incomming connections. And then they access the internal VPC ressources. Bastion hosts are used to secure the VPC by not allowing direct access to the internal ressources. Bastion hosts are also used to monitor and log all the connections to the VPC.
