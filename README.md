# AWS CloudFormation VPC Networking Project

## Project Overview

This project demonstrates an Infrastructure as Code (IaC) deployment utilizing AWS CloudFormation to provision a secure, multi-tier Virtual Private Cloud (VPC) architecture in the Sydney Region (ap-southeast-2).
The infrastructure separates public-facing resources from private backend services using a combination of public and private subnets, an Internet Gateway, and a NAT Gateway, ensuring high security and controlled outbound internet access.

## Architecture

<img width="1536" height="1024" alt="AWS CloudFormation VPC Architecture Diagram" src="https://github.com/user-attachments/assets/1582895b-1007-44ae-b308-9f35075f648f" />


## AWS Services Used

- Amazon VPC
- AWS CloudFormation
- Amazon EC2
- Internet Gateway
- NAT Gateway
- Elastic IP
- Route Tables and Subnet Associations
- Security Groups

## Network Configuration

| Component | Configuration |
|---|---|
| VPC | `VPC_CF_Demo` |
| VPC CIDR | `192.168.0.0/16` |
| Public App Subnet | `192.168.1.0/24` |
| Private Database Subnet | `192.168.2.0/24` |
| Region | Sydney (`ap-southeast-2`) |
| EC2 Instance Type | `t3.micro` |
| Operating System | Amazon Linux 2023 |
| Key Pair | `rohakey` |

## EC2 Instances

### App Server
- Deployed in the public subnet.
- Uses a public IP address.
- Instance type: `t3.micro`.

### Database Server
- Deployed in the private subnet.
- Does not have a public IP address.
- Uses the NAT Gateway for outbound internet access.

Note: The Database Server is an EC2 instance; a database engine is not installed by this template.

## Routing

- The public route table routes internet-bound traffic through the Internet Gateway.
- The private route table routes outbound internet traffic through the NAT Gateway.
- Both subnets retain the local route for VPC communication.

## Deployment

1. Sign in to the AWS Management Console.
2. Select the Sydney region (`ap-southeast-2`).
3. Open AWS CloudFormation.
4. Create a stack and upload `vpc-cf-demo.yaml`.
5. Provide the existing EC2 key pair name `rohakey`.
6. Review the configuration and create the stack.
7. Verify the stack status and resources after deployment.

## Security Considerations

The demonstration security group allows SSH and all inbound traffic from `0.0.0.0/0`, which is overly permissive. For production use, restrict SSH to trusted IP addresses and allow only required application ports.

## Cleanup

Delete the CloudFormation stack after completing the demonstration. Verify that the NAT Gateway, Elastic IP, EC2 instances, and other billable resources have been removed.

## Learning Outcomes

- Infrastructure as Code using AWS CloudFormation and YAML.
- VPC and subnet configuration.
- Public and private routing.
- Internet Gateway and NAT Gateway configuration.
- EC2 deployment and security group configuration.

## Disclaimer

This project is intended for learning and demonstration purposes. AWS charges may apply to resources such as NAT Gateways and Elastic IPs.

