

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

### SSH Troubleshooting
- **There's a connection timeout**
	- This is a security group issue. Any timeout (not just for SSH) is related to security groups or a firewall. Ensure your security group looks like this and correctly assigned to your EC2 instance.
- **There's still a connection timeout issue**
	- If your security group is properly configured as above, and you still have connection timeout issues, then that means a corporate firewall or a personal firewall is blocking the connection. **Please use EC2 Instance Connect as described in the next lecture.**
- **SSH does not work on Windows**
	- If it says: `ssh command not found`, that means you have to use Putty
	- Try to use EC2 Instance Connect
- **There's a connection refused**
	- This means the instance is reachable, but no SSH utility is running on the instance
		- Try to restart the instance
		-  If it doesn't work, terminate the instance and create a new one. Make sure you're using **Amazon Linux 2**
- **Permission denied (publickey,gssapi-keyex,gssapi-with-mic)**
	- You are using the wrong security key or not using a security key. Please look at your EC2 instance configuration to make sure you have assigned the correct key to it.
	-  You are using the wrong user. Make sure you have started an **Amazon Linux 2 EC2 instance**, and make sure you're using the user **ec2-user.** This is something you specify when doing `**ec2-user@**<public-ip>` (ex: `ec2-user@35.180.242.162`) in your SSH command or your Putty configuration


### EC2 Instances Purchasing Options
- ==On-Demand Instances==:
	- short workload
	- predictable pricing
	- pay by second
- ==Reserved== ( 1 & 3 years ):
	- Reserved Instances
		- long workloads
	- Convertible Reserved instances
		- long workloads with flexible instances
- ==Saving Plans== ( 1 & 3 years ):
	- commitment to a amount of usage
	- long workloads
- ==Spot Instances==:
	- short workloads
	- cheap
	- can lose instances ( less reliable )
- ==Dedicated Hosts==:
	- book an entire physical sever
	- control instance placements
- ==Dedicated Instances==:
	- no other customers will share your hardware
- ==Capacity Reservations==:
	- reserve capacity in specific AZ for any duration


### EC2 On Demand
- Pay for what you use:
	- Linux or Windows - billing per second, after the first minute
	- All other operating systems - billing per hour
- Has the highest cost but no upfront payment
- No long-term commitment 
- Recommended for short-term and un-interrupted workloads, where you can't predict how the application will behave

### EC2 Reserved
- XX% (right now up to 72%, but can change ) discount compared to On-demand
- You reserve a specific instance attributes ( Instance Types, Region, Tenancy, OS )
- Reservation period
	- 1 year ( discount + )
	- 3 years ( discount +++ )
- Payment options
	- No upfront ( + )
	- Partial upfront ( ++ )
	- All upfront ( +++ )
- Reserved Instance's Scopes
	- Regional
	- Zonal ( reserved capacity in an AZ )
- Recommended for steady-state usage applications ( think databases )
- You can buy and sell in Reserved Instance Marketplace

#### Convertible Reserved Instances
- Can change the EC2 instance type, instance family, OS scope and tenancy
- less discount then regular Reserved instances ( up to 54% right now )

### EC2 Savings Plans
- Get a discount based on long-term usage ( save discount as RIs )
- Commit to a certain type of usage ( $10/hour for 1 or 3 years : example )
- Usage beyond EC2 Savings Plans is billed at the On-Demand price
- Locked to a specific instance family & AWS region ( e.g M5 in us-east-1 )
- Flexible across:
	- Instance Size ( e.g m5.xlarge, m5.2xlarge)
	- OS ( e.g Linux, Windows)
	- Tenancy ( Host, Dedicated, Default )


###  EC2 Sport Instances
- Can get a discount of up to 90% compared to On-demand
- Instances that you can "lose" at any point of time if your max price is less than the current spot price
- The Most cost-efficient instances in AWS
- Useful for workloads that are resilient to failure
	- Batch job
	- Data analysis
	- Image processing
	- Any distributed workloads
	- Workloads with flexible start and end time
- Not suitable for critical jobs or databases

### EC2 Dedicated Hosts

- A physical server with EC2 instance capacity fully dedicated to your use
- Allows you address compliance requirements and use your existing server-bound software licenses ( per-socket, per-core, per-VM software licenses )
- Purchasing Options:
    - On-demand - pay per second for active Dedicated Host
    - Reserved - 1 or 3 years ( No Upfront, Partial Upfront, All Upfront )
- The most expensive option
- Useful for software that have complicated licensing model ( BYOL - Bring Your Own License )
- Or for companies that have strong regulatory or compliance needs

### EC2 Dedicated Instances
- Instances run on hardware that's dedicated to you
- May share hardware with other instances in same account
- No control over instance placements ( can move hardware after Start / Stop )

| Characteristic                                         | Dedicated Instances | Dedicated Hosts |
| ------------------------------------------------------ | ------------------- | --------------- |
| Enables the use of dedicated physical servers          | X                   | X               |
| Per Instance billing ( subject to a $2 per region fee) | X                   |                 |
| Per host billing                                       |                     | X               |
| Visibility of sockets, cores, host ID                  |                     | X               |
| Affinity between host and instance                     |                     | X               |
| Targeted instance placements                           |                     | X               |
| Automatic instance placement                           | X                   | X               |
| Add capacity using an allocation request               |                     | X               |

### EC2 Capacity Reservations
- Reserve On-Demand instances capacity in a specific AZ for any duration
- You always have access to EC2 capacity when you need it
- No time commitment (create / cancel anytime ), no billing discounts
- Combine with Regional Reserved Instances and Saving Plans to benefit from billing discounts
- You're charged at On-Demand rate whether you run instances or not
- Suitable for short-term, uninterrupted workloads that needs to be in a specific AZ



### Price Comparison
#### Example - m4.large - us-east-1

| Price Type                               | Price ( per hour )                             |
| ---------------------------------------- | ---------------------------------------------- |
| On-Demand                                | $0.10                                          |
| Spot Instances ( Spot Price )            | $0.038 - $0.039 ( up to 61% off)               |
| Reserved Instances ( 1 year )            | $0.062 ( No Upfront ) - $0.058 ( All Upfront ) |
| Reserved Instances ( 3 years )           | $0.043 ( No Upfront ) - $0.037 ( All Upfront ) |
| EC2 Savings Plan ( 1 year )              | $0.062 ( No Upfront ) - $0.058 ( All Upfront ) |
| Reserved Convertible Instance ( 1 year ) | $0.071 ( No Upfront ) - $0.066 ( All Upfront ) |
| Dedicated Host                           | On-Demand Price                                |
| Dedicated Host Reservation               | Up to 70% off                                  |
| Capacity Reservation                     | On-Demand Price                                |

### Shared Responsibility Model for EC2
- AWS
	- Infrastructure ( global network security )
	- Isolation on physical hosts
	- Replacing faulty hardware
	- Compliance validation
- You
	- Security Group rules
	- Operating-system patches and updates
	- Software and utilities installed on EC2 instances
	- IAM Roles assigned to EC2 & IAM user access management
	- Data security on your instance


### EC2 Section - Summary
- EC2 Instances: AMI ( OS ) + Instance Size ( CPU + RAM ) + Storage + security groups + EC2 User Data
- Security Group: Firewall attached to the EC2 instance
- User Data: script launched at the first launch of the instance
- SSH: start of terminal into our EC2 instances ( port 22 )
- EC2 Instance roles: link to IAM roles
- Purchasing Options: On-Demand, Sport, Reserver ( Standard + Convertible ), Dedicated Host, Dedicated Instance