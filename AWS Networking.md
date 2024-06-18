# Lecture AWS Networking

## 主要知识点
[1. VPC 简介（Virtual Private Cloud）](#1-vpc-简介virtual-private-cloud)  
[2. 网络安全基础](#2-网络安全基础)  
[3. AWS VPC 的定义和示例](#3-aws-vpc-的定义和示例)  
[4. 图示讲解 VPC 整个框架](#4-图示讲解-vpc-整个框架)  
[5. 内部 IP 范围](#5-演示如何在-vpc-中分配内部-ip-地址范围)  
[6. VPC Peering 简介](#6-vpc-peering-简介)  
[7. 子网（Subntet）](#7-子网（Subntet）) 
[8. 互联网网关（Internet Gateway）](#8-互联网网关internet-gateway)  
[9. 路由表（Route Table）](#9-路由表route-table)  
[10. VPC 端点（VPC Endpoints）](#10-vpc-端点vpc-endpoints)  
[11. VPC wrap-up](#11-vpc-wrap-up)  

## 1. VPC 简介（Virtual Private Cloud）

### 定义
A Virtual Private Cloud (VPC) is a virtual network dedicated to your AWS account. It is logically isolated from other virtual networks in the AWS Cloud, providing you full control over your virtual networking environment, including resource placement, connectivity, and security.

### 关键特性和优势
- **Isolation:** Provides logical isolation of resources.
- **Customization:** Offers customizable network configurations.
- **Security:** Enhances security through security groups and network ACLs.
- **Scalability:** Scales seamlessly with AWS resources.

## 2. 网络安全基础

### 基本概念
- **Firewall:** A network security system that monitors and controls incoming and outgoing network traffic.
- **Security Groups:** Virtual firewalls that control inbound and outbound traffic for AWS resources.
- **Subnet:**  Organise Resources and apply different network policies and access controls.
- **Network ACL (Access Control List):** A set of rules used to control incoming and outgoing traffic at the subnet level. It acts as a stateless firewall.
- **Internet Gateway:** A horizontally scaled, redundant, and highly available VPC component that allows communication between instances in your VPC and the internet.
- **VPN (Virtual Private Network):** A service that enables you to establish a secure and private connection over a public network (such as the internet) by encrypting your internet traffic.
- **Elastic IP Address:** A static, public IPv4 address designed for dynamic cloud computing. 
- **Peering Connections:** Direct network links between separate networks to exchange traffic efficiently outside the public internet.
- **Route Tables:** Network device configurations that determine paths for data packets based on defined routing rules.

## 3. AWS VPC 的定义和示例

### 示例和工作原理
A VPC typically includes subnets, route tables, internet gateways, and security groups. Here is a simplified example:



## 4.图示讲解-vpc-整个框架
![image](https://github.com/australiaitgroup/Data-Engineer-Fullstack-Wiki/assets/141289683/b2836d4a-9acf-4a62-a2d1-1a11c6542ba7)



## 5. 内部 IP 范围
- 10.0.0.0 to 10.255.255.255 (10.0.0.0/8 range)
- 172.16.0.0 to 172.31.255.255 (172.16.0.0/12 range)
- 192.168.0.0 to 192.168.255.255 (192.168.0.0/16 range)

## 6. VPC Peering 简介
VPC peering in AWS enables you to connect two Virtual Private Clouds (VPCs) together privately, allowing them to communicate using private IP addresses. Key aspects of VPC peering include:

- **Private Connectivity**: Establishes a private network connection between VPCs, keeping traffic within the AWS network without traversing the internet.

- **Non-Transitive**: Peering connections do not extend beyond the directly peered VPCs. Additional peering connections are required for indirect communications.

- **Security**: Controlled by security groups and network ACLs, ensuring secure communication between VPCs.

- **Region Support**: Can be set up within the same AWS region or across different regions globally.

- **Use Cases**: Facilitates architectures such as connecting different environments (e.g., development, production), integrating multi-tier applications, and sharing resources across VPCs.

- **Limitation**:  Overlapping CIDR blocks between peered VPC are not allowed.

## 7. 子网（Subntet）
# Key Features of Subnets

Subnets are subdivisions of a Virtual Private Cloud (VPC) in AWS that allow you to organize and segment your resources. Here are the key features of subnets:

## CIDR Block

Every subnet is associated with a Classless Inter-Domain Routing (CIDR) block, which defines the range of IP addresses available for that subnet. For example, a CIDR block of `10.0.1.0/24` provides IP addresses from `10.0.1.0` to `10.0.1.255`.

## Availability Zone (AZ)

Subnets are created within a specific AWS region and can be associated with one or more Availability Zones (AZs) within that region. An AZ is a physically distinct location with independent power, cooling, and networking. Placing subnets in different AZs provides fault tolerance and high availability for your applications.

## Public Subnet

A public subnet is a subnet that has a route to the internet gateway (IGW) attached to the VPC. Instances in a public subnet can have public IP addresses and can communicate directly with the internet. Public subnets are typically used for resources that need to be accessible from the internet, such as web servers.

## Private Subnet

A private subnet does not have a direct route to the internet. Instances in a private subnet can communicate with the internet or other AWS services through a Network Address Translation (NAT) gateway or NAT instance in a public subnet. Private subnets are commonly used for resources that should not be directly accessible from the internet, such as databases or application servers that only need internal communication or access to specific services.

---

## 8. 互联网网关（Internet Gateway）
An Internet Gateway (IGW) is a horizontally scaled, redundant, and highly available VPC component that allows communication between instances in your VPC and the internet. Here are the key aspects of an Internet Gateway:

## Key Features

### Enabling Internet Access

- **Internet Connectivity**: An IGW enables instances in a VPC to connect to the internet. Without an IGW, resources in your VPC cannot directly access the internet.
- **Bidirectional Communication**: Facilitates both inbound and outbound traffic, allowing instances to receive requests from the internet and send responses back.

### High Availability and Redundancy

- **Scalable**: Designed to be highly available and scalable, the IGW can handle the varying levels of internet traffic without any manual intervention.
- **Redundant**: Automatically redundant across multiple Availability Zones in a region, ensuring continuous availability and reliability.

### Integration with Route Tables

- **Routing**: For instances in a subnet to access the internet, the subnet's route table must have a route directing internet-bound traffic (0.0.0.0/0) to the IGW.
- **Public Subnets**: Typically, subnets with a route to the IGW are considered public subnets, where instances can have public IP addresses and direct internet access.

### Security Considerations

- **Security Groups and Network ACLs**: Control inbound and outbound traffic to instances via security groups and network ACLs, providing an additional layer of security.
- **NAT Gateway/Instance**: For private subnets, use a NAT gateway or NAT instance in a public subnet to allow outbound internet traffic while keeping instances private.

## Use Cases

- **Web Servers**: Deploy web servers in public subnets to serve internet users.
- **Bastion Hosts**: Set up bastion hosts in public subnets for secure SSH/RDP access to instances in private subnets.
- **Outbound Access**: Allow instances in private subnets to access the internet for software updates or external services via a NAT gateway or instance.

## Setting Up an Internet Gateway

1. **Create an IGW**: Use the AWS Management Console, CLI, or SDKs to create an Internet Gateway.
2. **Attach to VPC**: Attach the IGW to your VPC.
3. **Update Route Tables**: Modify the route tables of your public subnets to include a route to the IGW (0.0.0.0/0).



## 9. 路由表（Route Table）
# Route Table

A route table in AWS is a set of rules, called routes, that are used to determine where network traffic from your subnets is directed. Here are the key aspects of a route table:

## Key Features

### Basic Concept

- **Routing Rules**: Each route table contains a set of rules, known as routes, that specify the paths network traffic should take to reach various destinations.
- **Subnets Association**: Route tables are associated with one or more subnets within a VPC. Each subnet must be associated with a route table, which controls the routing for that subnet.

### Default Route Table

- **Main Route Table**: Each VPC has a main route table that all subnets are initially associated with by default. You can modify the main route table or create additional custom route tables as needed.

### Custom Route Tables

- **Creating Custom Tables**: You can create custom route tables to manage specific routing needs for different subnets. This allows for more granular control over network traffic within your VPC.
- **Route Propagation**: You can enable route propagation for route tables to automatically add routes managed by a VPN connection or AWS Direct Connect.

### Route Entries

- **Destination CIDR Blocks**: Each route in a route table specifies a destination CIDR block (e.g., 0.0.0.0/0 for all IP addresses) and a target (e.g., internet gateway, NAT gateway, VPC peering connection).
- **Local Route**: Every route table has an implicit local route for communication within the VPC (e.g., VPC CIDR block).

### Routing Targets

- **Internet Gateway (IGW)**: Enables direct internet access for instances in the subnet.
- **NAT Gateway/Instance**: Allows instances in a private subnet to send outbound traffic to the internet.
- **Virtual Private Gateway (VGW)**: Connects your VPC to a VPN connection.
- **VPC Peering Connection**: Routes traffic between peered VPCs.
- **Transit Gateway**: Central hub for connecting VPCs and on-premises networks.

## Security Considerations

- **Segmentation**: Use separate route tables to segment network traffic for different subnets, improving security and traffic management.
- **Access Control**: Combine route tables with security groups and network ACLs to enforce fine-grained control over network access.

## Use Cases

- **Public Subnets**: Route tables for public subnets typically have a route directing internet-bound traffic (0.0.0.0/0) to an internet gateway.
- **Private Subnets**: Route tables for private subnets may have routes directing internet-bound traffic to a NAT gateway or instance.
- **Hybrid Environments**: Use route tables to direct traffic between your VPC and on-premises network via a VPN connection or AWS Direct Connect.

## Managing Route Tables

1. **Create Route Table**: Use the AWS Management Console, CLI, or SDKs to create a new route table.
2. **Add Routes**: Add routing rules specifying the destination CIDR blocks and targets.
3. **Associate Subnets**: Associate the route table with one or more subnets within your VPC.
4. **Modify as Needed**: Update the routes or associations as your network architecture evolves.



## 10. VPC 端点（VPC Endpoints）
# VPC Endpoint

A VPC Endpoint allows you to privately connect your VPC to supported AWS services and VPC endpoint services powered by AWS PrivateLink without requiring an internet gateway, NAT device, VPN connection, or AWS Direct Connect connection. Here are the key aspects of a VPC endpoint:

## Key Features

### Private Connectivity

- **Private Access**: VPC endpoints enable you to privately access services hosted in AWS directly from your VPC without sending traffic over the public internet.
- **Enhanced Security**: By keeping traffic within the AWS network, VPC endpoints reduce exposure to security risks associated with internet traffic.

### Types of VPC Endpoints

1. **Interface Endpoints**
   - **Description**: Elastic Network Interfaces (ENIs) with private IP addresses that serve as entry points for traffic destined to supported services.
   - **Use Cases**: Typically used to connect to AWS services like Amazon S3, Amazon DynamoDB, AWS Secrets Manager, etc.
   
2. **Gateway Endpoints**
   - **Description**: Specialized route table targets used to access AWS services. Currently, only Amazon S3 and DynamoDB support gateway endpoints.
   - **Use Cases**: Mainly used to connect to Amazon S3 and DynamoDB without traversing the internet.

### Integration with Route Tables

- **Route Tables**: For gateway endpoints, you need to update route tables to direct traffic to the endpoint. Interface endpoints do not require route table updates since they are accessed via DNS names.

### DNS Integration

- **DNS Names**: AWS automatically creates private DNS names for your endpoints. You can also enable private DNS for interface endpoints to access services using their standard public DNS names, which resolve to the private IP addresses of the endpoints.

### Security Groups

- **Access Control**: Interface endpoints can be associated with security groups to control access to the endpoint. This allows you to define fine-grained access policies.

### High Availability

- **Redundancy**: VPC endpoints are highly available and scalable within an Availability Zone. Interface endpoints automatically scale to accommodate traffic levels.

## Use Cases

- **Secure Access**: Enable secure and private access to AWS services without requiring an internet gateway or NAT.
- **Compliance**: Helps meet regulatory requirements by keeping data within the AWS network.
- **Cost Optimization**: Reduces data transfer costs associated with using public IPs for accessing AWS services.

## 11. VPC wrap-up


