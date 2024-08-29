

### How Websites Work?
- Client make request to a Server via a Network, the Server sends responses back via the same Network to the Client.
- The Client and the Server have unique IP addresses which we can use to connect them together to send requests and receive responses. To visually it better its a similar to how mailbox in real live work, you put a post mail inside you mailbox ( Client ) and then the Mail man ( Network ) delivers you post mail to your friends mailbox ( Server ), in this scenario the location of the mailboxes is the IP addresses.

### What is a Server compose of?
- Compute: CPU ( Central Processing Unit ) 
- Memory: RAM ( Read only Memory
- Storage: Data
- Database: Store data in a structured way
- Network: Routers, DNS server, switch

### IT Terminology 
- Network: cables, router and servers connected with each other
- Router: A networking device that forwards data packages between computer networks. They know where to send you packets over the internet!
- Switch: Takes a packet and send it to the correct server / client on you network

### Traditionally, how to build infrastructure 
- Used to be hosted in home or garage
- Once demand increased, you would need to put more and / or bigger servers in your house
- When it became too much, you would rent a office and put the servers in a separate room called a 'Data Center'
- Pay for rent for the Data Center
- Pay for power supply, cooling, maintance
- Expansion was expensive, since you needed a complete new server or upgrade some parts of the server every time you needed to scale.
- Slow scaling and limited, since you needed to wait for parts.
- Hire 24/7 team to monitor the infrastructure

### The question
can we externalize this? - the answer, the Cloud


### What is Cloud Computing?
- ==Cloud computing is the on-demand delivery of computing power, database storage, application and other IT-services==
- ==Through a cloud services platform with pay-as-go pricing ( you pay for what you use )==
- ==You can provision exactly the right type of size of computing resource you need==
- ==You can access as many resources as you need, almost instantly==
- ==Simple way to access servers, storage, databases and set of application services==
- ==AWS (Amazon Web Services) owns and maintains the network-connected hardware required for these application services, while you provision, and use what you need via a web application==

### You have been using Cloud Services already
- Gmail: E-mail Cloud Service, Pay for ONLY your email store ( no infrastructure, etc)
- Dropbox: Cloud Storage Service, Originally build on AWS
- Netflix: Build on AWS, Video on Demand
Very different from AWS, but still good to mention to get a better idea for cloud computing

### The Deployment Methods of the Cloud
#### Private Cloud (Out of Scope for this course, but good to know)
- ==Cloud services used by a single organization, not exposed to the public==
- Complete Control
- Security for sensitive application
- Meet specific business needs
- Example: Rackspace
#### Public Cloud
- ==Cloud resources owned and operated by third-party cloud service provider delivered over the internet==
- [[#Six Advantages of Cloud Computing]]
- Example: AWS ( Amazon Web Services ), GCP ( Google Cloud Platform), Microsoft Azure
#### Hybrid Cloud
- Keep some servers on premise and extend some capabilities to the Cloud
- Control over sensitive assets in you private infrastructure
- Flexibility and cost effectiveness of the public cloud
- Example: have some private servers, but domain services through AWS


### The Five Characteristics of Cloud Computing
1.  ==On-demand self service==
	- ==User can provision resources  and use them without human interaction from the service provider ==
2. ==Broad Network access
	- ==Resources available over the network, and can be accessed by diverse client platforms
3. ==Multi-tenancy and resource pooling
	- ==Multiple customers can share the same infrastructure and applications with security and privacy
	- ==Multiple customers are services from the same physical resources
4. ==Rapid elasticity and scalability
	- ==Automatically and quickly acquire and dispose resources when needed
	- ==Quickly and easily scale based on demand
5. ==Measured service
	- ==Usage is measured, users pay correctly for what they used

### Six Advantages of Cloud Computing
1. Trade capital expenses ( ==CAPEX== ) for operational expenses ( ==OPEX== )
	1. Pay On-Demand: don't own hardware
	2. Reduced Total Cost of Ownership ( ==TCO== ) & Operational Expenses ( ==OPEX== )
2. ==Benefit from massive economies of scale
	1. Prices are reduced as AWS is more efficient due to large scale
3. Stop guessing capacity
	1. Scale based on actual measured usage
4. Increased speed and agility
5. Stop spending money running and maintaining data centres
6. Go global in minutes: Leverage the ==AWS global infrastructure==


### Problems solver by the Cloud
- ==Flexibility==: change resource types when needed
- ==Cost-Effectiveness==: pay as you go, for what you use
- ==Scalability==: accommodate larger loads by making hardware stronger or adding additional nodes
- ==Elasticity==: ability to scale out and scale-in when needed
- ==High-availability and fault-tolerance==: build across data centers
- ==Agility==: rapidly develop, test and launch software applications


### Types of Cloud Computing
- Infrastructure as a Service ( ==IaaS== )
	- Provide building blocks for cloud IT
	- Provides networking, computers, data storage space
	- Highest level of flexibility
	- Easy parallel with traditional on-premises IT
- Platform as a Service ( ==PaaS== )
	- Removes the need for your organization to manage the underlying infrastructure
	- Focus of the deployment and management of your applications
- Software as a Service ( ==SaaS== )
	- Completed product that is run and managed by the service provider



| On-premises                                                    | IaaS                                                          | Pass                                                          | SaaS                                                          |
| -------------------------------------------------------------- | ------------------------------------------------------------- | ------------------------------------------------------------- | ------------------------------------------------------------- |
| <span style="color: rgb(124, 147, 195);">Application</span>    | <span style="color: rgb(124, 147, 195);">Application</span>   | <span style="color: rgb(124, 147, 195);">Application</span>   | <span style="color: rgb(255, 131, 67);">Application</span>    |
| <span style="color: rgb(124, 147, 195);">Data</span>           | <span style="color: rgb(124, 147, 195);">Data</span>          | <span style="color: rgb(124, 147, 195);">Data</span>          | <span style="color: rgb(255, 131, 67);">Data</span>           |
| <span style="color: rgb(124, 147, 195);">Runtime</span>        | <span style="color: rgb(124, 147, 195);">Runtime</span>       | <span style="color: rgb(255, 131, 67);">Runtime</span>        | <span style="color: rgb(255, 131, 67);">Runtime</span>        |
| <span style="color: rgb(124, 147, 195);">Middleware</span>     | <span style="color: rgb(124, 147, 195);">Middleware</span>    | <span style="color: rgb(255, 131, 67);">Middleware</span>     | <span style="color: rgb(255, 131, 67);">Middleware</span>     |
| <span style="color: rgb(124, 147, 195);">O/S</span>            | <span style="color: rgb(124, 147, 195);">O/S</span>           | <span style="color: rgb(255, 131, 67);">O/S</span>            | <span style="color: rgb(255, 131, 67);">O/S</span>            |
| <span style="color: rgb(124, 147, 195);">Virtualization</span> | <span style="color: rgb(255, 131, 67);">Virtualization</span> | <span style="color: rgb(255, 131, 67);">Virtualization</span> | <span style="color: rgb(255, 131, 67);">Virtualization</span> |
| <span style="color: rgb(124, 147, 195);">Servers</span>        | <span style="color: rgb(255, 131, 67);">Servers</span>        | <span style="color: rgb(255, 131, 67);">Servers</span>        | <span style="color: rgb(255, 131, 67);">Servers</span>        |
| <span style="color: rgb(124, 147, 195);">Storage</span>        | <span style="color: rgb(255, 131, 67);">Storage</span>        | <span style="color: rgb(255, 131, 67);">Storage</span>        | <span style="color: rgb(255, 131, 67);">Storage</span>        |
| <span style="color: rgb(124, 147, 195);">Networking</span>     | <span style="color: rgb(255, 131, 67);">Networking</span>     | <span style="color: rgb(255, 131, 67);">Networking</span>     | <span style="color: rgb(255, 131, 67);">Networking</span>     |
<span style="color: rgb(255, 131, 67);">Managed by others</span>   <span style="color: rgb(124, 147, 195);">Managed by you</span>


### Example of Cloud Computing Types
- Infrastructure as a Service
	- ==Amazon EC2== ( on AWS )
	- GCP, Azure, Rackspace, Digital Ocean, Linode
- Platform as a Service
	- ==Elastic Beanstalk== ( on AWS )
	- Heroku, Google App Engine ( GCP ), Windows Azure ( Microsoft )
- Software as a Service
	- Many AWS services ( ex: Rekognition for Machine Learning )
	- Google Apps ( Gmail ), Dropbox, Zoom

### Pricing of the Cloud - Quick Overview
- AWS has 3 pricing fundamentals, following the pay-as-you-go pricing model
- ==Compute==
	- Pay for compute time
- ==Storage==
	- Pay for data store in the Cloud
- ==Data transfer OUT of the Cloud
	- Data transfer IN is free
- Solves the expensive issue of traditional IT


### AWS Cloud Number Facts
- In 2019, AWS has $35.02 billion in annual revenue
- AWS accounts for 47% of the market in 2019 ( Microsoft is 2nd with 22% )
- Pioneer and Leader of the AWS Cloud Market for the 9th consecutive year
- Over 1,000,000 active users

### AWS Cloud Use Cases
- AWS enables you to build sophisticated, scalable applications
- Applicable to a diverse set of industries
- Use cases include
	- Enterprise IT, Backup & Storage, Big Data analytics
	- Website hosting, Mobile & Social Apps
	- Gaming

### ==AWS Global Infrastructure==
- AWS ==Regions==
- AWS ==Availability Zone==
- AWS ==Data Centers== 
- AWS ==Edge Locations / Point of Presence==

### Link to AWS Global Infrastructure
https://infrastructure.aws/


### ==AWS Regions==
- AWS has Regions all around the world
- Names can be us-east-I, eu-west-3 ...
- A region is a cluster of data centers
- Most AWS services are region-scoped


## How to Choose an AWS Region?
#### If you need to launch a new application where should you do it?
- It depends

### Things to consider when choosing a Region
- ==Compliance== with data governance and legal requirements: data never leaves a region without your explicit permission
- ==Proximity== to customers: reduced latency
- ==Available services== within a Region: new services and new features aren't available in every Region
- ==Pricing==: pricing varies region to region and is transparent in the service pricing page

### ==AWS Availability Zones==
- Each region has many availability zones ( usually 3, min is 3, max is 6 ). Example
	- ap-southeast-2a
	- ap-southeast-2b
	- ap-southeast-2c
- Each availability zone ( AZ ) is one or more discrete data centers with redundant power, networking, and connectivity
- They're separate from each other, so that they're isolated from disasters
- They're connected with high bandwidth, ultra-low latency networking


### ===AWS Points of Presence ( Edge Locations )
- Amazon has 400+ Points of Presence ( 400+ Edge Locations & 10+ Regional Caches ) in 90+ cities across 40+ countries
- Content is delivered to end users with lower latency
- https://aws.amazon.com/cloudfront/features/

Tour of the AWS Console
- AWS has Global Services
	- Identity and Access Management ( ==IAM==  )
	- ==Route 53== ( DNS service )
	- ==CloudFront== ( Content Delivery Network )
	- ==WAF== ( Web Application Firewall )
- Most AWS services are Region-scoped
	- ==Amazon EC2== ( Infrastructure as a Service )
	- Elastic Bean ( Platform as a Service )
	- ==Lambda== ( Function as a Service )
	- Rekognition ( Software as a Service )
- Region Table
	- https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services

### ==Shared Responsibility Model diagram==
- CUSTOMER = Responsibility for the security ==IN== the Cloud
	- Customer Data
	- Platform, Applications, Identity & Access Management
	- Operating System, Network & Firewall Configuration
	- Client-Side Data Encryption & Data Integrity authentication
	- Server-Side Encryption ( File System And / Or Data )
	- Networking Traffic Protection ( Encryption, Integrity, Identity )
- AWS = Responsibility for the security ==OF== the Cloud
	- Software
		- Compute
		- Storage
		- Database
		- Networking
	- Hardware / AWS Global Infrastructure
		- Regions
		- Availability zones
		- Edge locations
- https://aws.amazon.com/compliance/shared-responsibility-model


### AWS Acceptable Use Policy'
- https://aws.amazon.com/aup
- No Illegal, Harmful, or Offensive Use or Content
- No Network Abuse
- No E-Mail or Other Message Abuse


