# Custom-VPC-creation-

Built a custom AWS network from scratch

# Project Overview
This project demonstrates the creation of a custom AWS VPC with a highly available network architecture consisting of:

1.1 Custom VPC
2.2 Public Subnets
3.2 Private Subnets
4.Internet Gateway (IGW)
5.NAT Gateway with Elastic IP
6.Public & Private Route Tables
7.Security Groups
8.EC2 Web Server (Apache)
9.SSH Access using Key Pair

The architecture enables public internet access for web servers while allowing private resources to securely access the internet through a NAT Gateway

# Architecture Diagram 
<img width="1536" height="1024" alt="51" src="https://github.com/user-attachments/assets/00f2a259-d6b6-4d2f-a7ef-38733fc69356" />

# Network Design
VPC

Resource	CIDR
Custom VPC	10.0.0.0/16

Public Subnets

Subnet	CIDR	Availability Zone
Public Subnet A	10.0.1.0/24	AZ-A
Public Subnet B	10.0.2.0/24	AZ-B

Private Subnets

Subnet	CIDR	Availability Zone
Private Subnet A	10.0.3.0/24	AZ-A
Private Subnet B	10.0.4.0/24	AZ-B



# Services Used
1.Amazon VPC
2.Amazon EC2
3.Internet Gateway
4.NAT Gateway
5.Elastic IP
6.Route Tables
7.Security Groups
8.Apache HTTP Server (httpd)

# Implementation steps -

1. Create Custom VPC
            CIDR Block:10.0.0.0/16 
2. Create 2 public subnets
            CIDR block: 10.0.1.0/16 (A)  and 10.0.2.0/16(B)
3. Create 2 private subnets
            CIDR block: 10.0.3.0/16 (A)  and 10.0.4.0/16(B)
4. Create and Attach Internet Gateway
            Attach the Internet Gateway to the VPC to provide interent connectivity.
5. Create Public Route table
            Add routes: 10.0.0.0/16 --> local and 0.0.0.0/0 --> Internet Gateway
   Associate with:
   Public Subnet A
   Public Subnet B

7. Create Elastic IP
            Allocate an Elastic IP for the NAT Gateway.

8. Create Private route table
            10.0.0.0/16 --> local  and 0.0.0.0/0 ---> NAT gateway
   Associate with:
   Private Subnet A
   Private Subnet B

9. Create Security Group
            Inbound rules that say SSH ---> 22 --> MyIp(source)
             HTTP ---> 80 ---> anywhere(0.0.0.0/0)(source)
 
10. Launch EC2 Instance
    Amazon Linux 2
    Custom VPC
    Public Subnet
    Attach Security Group
    Use Key Pair for SSH Access  

11. Install Apache Web Server
        sudo yum update -y
        sudo yum install httpd -y

12. Start and Enable Apache
        sudo systemctl start httpd
        sudo systemctl enable httpd
13. Create Test Web Page
        echo "<h1>Hello myself amarjit paul and this is my ec2</h1>" | sudo tee /var/www/html/index.html
14. Verify Deployment
        http://<Public-IP>


# Security Features
1.Private resources are isolated in private subnets.
2.Internet access for private subnets is provided through NAT Gateway.
3.SSH access restricted to the administrator's IP.
4.HTTP access allowed for public web traffic.

# Project Outcome
1.Created a custom VPC with CIDR 10.0.0.0/16
2.Configured 2 Public Subnets across different Availability Zones
3.Configured 2 Private Subnets across different Availability Zones
4.Attached Internet Gateway for public internet access
5.Configured NAT Gateway for secure outbound internet access from private subnets
6.Created Public and Private Route Tables
7.Launched and configured an EC2 Apache Web Server
8.Successfully hosted a website accessible through the EC2 Public IP

# To avoid AWS charges:
1.Terminate EC2 Instances
2.Delete NAT Gateway
3.Release Elastic IP
4.Delete Route Tables
5.Delete Subnets
6.Detach and Delete Internet Gateway
7.Delete Security Groups (if unused)
8.Delete VPC

# Some mistakes i made 
  while using myip in ssh configuration in inbound rules , i find that i am not able to connect my EC2 . The reson behind this is that the myip that u may use      chances are there , it is not same with the actual ip at that point of time , as we all know ip chnages so before adding this u need to check whether the ip in   myIp is the same as your current ip so i have to change it to anywhere(0.0.0.0/0) or u can edut your ip wuth the cureent one to work .


# Screenshots

1. Creating VPC with CIDR 10
   <img width="940" height="433" alt="image" src="https://github.com/user-attachments/assets/6cf2a4fc-118b-4b93-9e02-c42a6e9c4a4f" />

2. Creation of public subnet
<img width="940" height="432" alt="image" src="https://github.com/user-attachments/assets/507b84ac-401a-4a21-858c-894816f7e218" />

3. Creation of private subnet
<img width="940" height="388" alt="image" src="https://github.com/user-attachments/assets/921a8b74-155b-4e54-8a4c-6c909a039789" />

4. 2 public and 2 private
<img width="940" height="435" alt="image" src="https://github.com/user-attachments/assets/ebd10c47-3a31-4bb5-9b0c-23e3fd087866" />

5. Creating internet gateway for internet connectivity
<img width="940" height="423" alt="image" src="https://github.com/user-attachments/assets/6f80e98b-9740-426b-ae47-6bcf5de404f9" />

6. Public Route-table
<img width="940" height="431" alt="image" src="https://github.com/user-attachments/assets/038925fa-bdc4-4405-a1e4-f8df1c49f81d" />

7. Creating NAT gateway
<img width="940" height="441" alt="image" src="https://github.com/user-attachments/assets/148d2302-5596-46aa-9300-6399833cdcf1" />

8.Elastic IP for NAT gateway
<img width="940" height="428" alt="image" src="https://github.com/user-attachments/assets/b74ce154-298b-431c-8afd-22529348ac83" />

9. Private Route Table
<img width="940" height="429" alt="image" src="https://github.com/user-attachments/assets/f07d17d9-774c-4d68-820f-1d660bf99c0f" />

10. Creating Security Groups
<img width="940" height="412" alt="image" src="https://github.com/user-attachments/assets/72192b77-b26c-47a3-b6da-189075354fb1" />

11. Creating EC2 instance
<img width="940" height="412" alt="image" src="https://github.com/user-attachments/assets/45672be7-b0a0-4be9-b80b-c783cd201817" />


12. Installing appache with starting and enabling
<img width="940" height="437" alt="image" src="https://github.com/user-attachments/assets/389f69d1-e9bf-464a-b377-b66f5a7b9c6e" />

13. Deployment
<img width="940" height="501" alt="image" src="https://github.com/user-attachments/assets/0fd1b231-1ecc-43cc-b510-7859b5efa7ba" />


