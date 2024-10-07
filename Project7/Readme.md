# AWS VPC Project

## What is a VPC?

A VPC (Virtual Private Cloud) in AWS (Amazon Web Services) is a service that allows you to launch AWS resources in a logically isolated virtual network that you define. Here are the key components and features of an AWS VPC:

1. **Subnets**: A VPC can be divided into multiple subnets, which are sections of the VPC IP address range where you can place groups of isolated resources. Subnets can be either public (with access to the internet) or private (isolated from the internet).

2. **IP Addressing**: You can choose your own IP address range for the VPC using IPv4 or IPv6 addresses.

3. **Route Tables**: Control the routing of network traffic within the VPC and between subnets. You can create custom route tables to direct traffic as needed.

4. **Internet Gateway**: A VPC component that allows communication between instances in your VPC and the internet. You need to attach an Internet Gateway to a VPC to enable internet access for your instances.

5. **NAT Gateway and NAT Instances**: These allow instances in a private subnet to connect to the internet or other AWS services without exposing themselves to incoming traffic from the internet.

6. **Security Groups**: Act as virtual firewalls for your instances to control inbound and outbound traffic at the instance level.

7. **Network ACLs (Access Control Lists)**: Provide an additional layer of security, controlling traffic at the subnet level.

8. **VPC Peering**: Allows you to connect one VPC with another VPC to route traffic between them using private IP addresses.

9. **VPN Gateway**: Enables you to establish a secure connection between your VPC and your on-premises network.

10. **VPC Endpoints**: Allow you to privately connect your VPC to supported AWS services and VPC endpoint services powered by AWS PrivateLink without requiring an Internet Gateway, NAT device, VPN connection, or AWS Direct Connect connection.

11. **AWS Direct Connect**: Provides a dedicated network connection from your premises to AWS, enhancing security and reducing network costs.



# Understand VPC Requirements
As a DevOps engineer, you need to understand the VPC requirements by asking questions to the relevant teams.

When working in real projects, following are some of the important questions that will help you understand the VPC requirements better.

1. Identifying Your Hosting Needs: What do you want to host?
2. Meeting Compliance Standards: What are its compliance requirements?
3. Handling Sensitive Information: Does it have applications dealing with PCI/PII data?
4. Public vs. Private Accessibility: Are the applications internet-facing?
5. Connecting to On-Premise Systems: Does the VPC require a Hybrid connectivity to an on-premise environment? If yes, is it DNS or IP-based connectivity?
6. User Accessibility to VPC Services: How are users going to connect to the services hosted in VPC?
7. VPC to VPC Connectivity: Does it need access to services hosted on other VPCs that are part of organizations network?
It is always best to document these requirements.

Note: Organizations typically keep a questionnaire to understand the VPC requirements from network, security, and compliance perspectives.

# VPC Network Design
Ideally in most organizations the VPC is created and managed by a dedicated Network team. However, devops engineers working with the application team need to come up with the VPC requirements that can host all the required applications.