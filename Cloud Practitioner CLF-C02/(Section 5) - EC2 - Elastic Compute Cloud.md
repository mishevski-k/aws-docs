

### Amazon EC2
- EC2  is one of the most popular AWS offering
- EC2 = Elastic Compute Cloud = Infrastructure as a Service
- It mainly consists in the capability of:
	- Renting virtual machines ( ==EC2== )
	- Storing data on virtual drives ( ==EBS== )
	- Distributing load across machines ( ==ELB== )
	- Scaling the service using an auto-scale group( ==ASG== )
- ==Knowing EC2 is fundamental to understand how the Cloud works==


### EC2 sizing & configuration options
- operating system ( OS ):
	- Linux
	- Windows
	- Mac OS
- How much compute power & cores ( CPU )
- How much random-access memory ( RAM )
- How much storage space:
	- Network-attached ( EBS & EFS )
	- Hardware ( EC2 Instance Store)
- Networking card: speed of the card, Public IP Address
- Firewall rules: ==security group==
- Bootstrap script ( configure at first launch ): ==EC2 User Data==

### EC2 User Data
- It is possible to bootstrap our instances using an ==EC2 User Data== script
- ==bootstrapping== means launching commands when a machine starts
- That script is only run ==once== at the instance ==first start==
- EC2 user data is used to automate boot tasks such as:
	- Installing updates
	- Installing software
	- Downloading common files from the internet
	- Anything you can think of
- The EC2 User Data script runs with the root user ( ==sudo== )

### EC2 instance types example

| Instance    | vCPU | Memory ( GiB ) | Storage          | Network performance | EBS Bandwidth ( Mbps ) |
| ----------- | ---- | -------------- | ---------------- | ------------------- | ---------------------- |
| t2.micro    | 1    | 1              | EBS Only         | Low to Moderate     |                        |
| t2.xlarge   | 4    | 16             | EBS Only         | Moderate            |                        |
| c5d.4xlarge | 16   | 32             | 1 x 400 NVMe SSD | Up to 10 Gpbs       | 4, 750                 |
| r5.16xlarge | 64   | 512            | EBS Only         | 20 Gbps             | 13,600                 |
| m5.8xlarge  | 32   | 128            | EBS Only         | 10 Gbps             | 6,800                  |
==t2.micro is part of the AWS Free Tier ( up to 750 hours per month )==


### EC2 creation using EC2 User Data
```
#!/bin/bash
# Use this for you user data ( script from top to bottom )
# install httpd ( Linux 2 version )
yum update -y
yum install -y httpd
systemctl start httpd
systemctl enable httpd
echo "<h1>Hello world from $(hostname -f)</h1>" > /var/www/html/index.html
```


### EC2 Instance Types - Overview
- You can use different types of EC2 instances that are optimised for different use cases
	- https://aws.amazon.com/ec2/instance-types/
- AWS has the following naming convention:
	- example: m5.2xlarge
		- m: instance class
		- 5: generation ( AWS improves them over time )
		- 2xlarge: size within the instance class
- AWS has 8 types of instances
	- General Purpose
	- Compute Optimised
	- Memory Optimised
	- Accelerated Computing
	- Storage Optimised
	- HPC Optimised
	- Instance Features
	- Measuring Instance Performance

### EC2 Instance Types - General Purpose
- Great for a diversity of workloads such as web servers or code repositories
- Balance between:
	- Compute
	- Memory
	- Networking

### EC2 Instance Types - Compute Optimized
- Great for compute-intensive tasks that require high performance processors
- Use cases:
	- Batch processing workloads
	- Media transcoding
	- High performance web servers
	- High performance computing ( HPC )
	- Scientific modeling & machine learning
	- Dedicated gaming servers
- Class Starts with "c"

### EC2 Instance Types - Memory Optimized
- Fast performance for workloads that process large data sets in memory
- Use cases:
	- High performance, relational / non-relational database
	- Distributed web scale cache stores
	- In-memory databases optimized for BI ( business intelligence )
	- Applications performing real-time processing of big unstructured data
- Class starts with "R" most of the time, but can be X, z and High memory

### EC2 Instance Types - Storage Optimized
- Great for storage-intensive tasks that require high, sequential read and write access to large data sets on local storage
- Use cases:
	- High Frequency online transaction processing ( OLTP ) systems
	- Relational & NoSQL databases
	- Cache for in-memory databases ( for example, Redis )
	- Data warehousing applications
	- Distributed file systems

#### ==Great website to compare EC2 instances==
https://www.ec2instances.info/


### Introduction to Security Groups
- Security Groups are the fundamental of network security in AWS
- They control how traffic is  allowed into or out of our EC2 instances
- Security groups only contain ==allow== rules
- Security groups rules can reference by IP or by security group

### Security Groups Deeper Dive
- Security groups are acting as a "firewall" on EC2 instances
- They regulate:
	- Access to Ports
	- Authorized IP ranges - IPv4 and IPv6
	- Control of inbound network ( from other to the instance )
	- Control of outbound network ( from the instance to other )


| Type            | Protocol | Port Range | Source            | Description    |
| --------------- | -------- | ---------- | ----------------- | -------------- |
| HTTP            | TCP      | 80         | 0.0.0.0/0         | test http page |
| SSH             | TCP      | 22         | 122.149.196.85/32 |                |
| Custom TCP Rule | TCP      | 4567       | 0.0.0.0/0         | java app       |


### Security Groups Good to know
- Can be attached to multiple instances
- Locked down to region / VPC combination
- Does live "outside" the EC2 - if traffic is blocked the EC2 instance won't see it
- ==It's good to maintain one separate security group for SSH access==
- If your application is not accessible ( time out ), then it's a security group issue
- If your application gives a "connection refused" error, then it's an application error or it's not launched
- All inbound traffic is ==blocked== by default
- All outbound traffic is ==authorized== by default

### Classic Ports to know
- 22 = SSH ( Secure Shell ) - log into a Linux instance
- 21 = FTP ( File Transfer Protocol ) - upload files into a file share
- 22 = SFTP ( Secure File Transfer Protocol ) - upload files using SSH
- 80 = HTTP - access unsecured websites
- 443 = HTTPS - access secured websites
- 3389 = RDP ( Remote Desktop Protocol ) - log into a Windows instance