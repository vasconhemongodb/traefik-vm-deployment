# Deployment Instructions

This folder contains a CloudFormation template to deploy an EC2 instance pre-configured with Docker and Docker Compose, ready to host Traefik and your applications.

## Resources Created

- **EC2 Instance**: Amazon Linux 2023 with Docker and Docker Compose installed via UserData.
- **Security Group**: Allows inbound traffic on ports 80 (HTTP), 443 (HTTPS), and 22 (SSH).
- **Elastic IP**: Provides a stable public IP address for your server.

## Parameters

- `InstanceType`: The EC2 instance type (default: `t3.small`).
- `KeyName`: The name of an existing EC2 Key Pair for SSH access.
- `VpcId`: The ID of your existing VPC.
- `SubnetId`: The ID of an existing subnet in your VPC.
- `AvailabilityZone`: The Availability Zone where the instance will be launched.
- `SSHLocation`: The IP range allowed to SSH into the instance (default: `0.0.0.0/0`).
- `ProjectName`: A name used for tagging resources (default: `Traefik-Deployment`).

## How to Deploy

1.  Log in to the AWS Management Console.
2.  Navigate to **CloudFormation**.
3.  Click **Create stack** -> **With new resources (standard)**.
4.  Choose **Upload a template file** and select `cloudformation.yaml`.
5.  Fill in the parameters.
6.  Once the stack is created, find the **PublicIP** in the **Outputs** tab.

## Post-Deployment Steps

1.  SSH into your instance:
    ```bash
    ssh -i your-key.pem ec2-user@<PublicIP>
    ```
2.  The `ec2-user` is already part of the `docker` group. You may need to log out and log back in for this to take effect if you try to run docker immediately.
3.  Clone this repository (or your project) into `/home/ec2-user/app`:
    ```bash
    cd /home/ec2-user/app
    # git clone <your-repo-url> .
    ```
4.  Configure your `.env` file based on `.env.example`.
5.  Run your applications:
    ```bash
    docker-compose up -d
    ```
