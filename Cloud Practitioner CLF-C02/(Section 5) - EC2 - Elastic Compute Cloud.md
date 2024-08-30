

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