

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
can we externalise this? - the answer, the Cloud


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
- ==Cloud services used by a single organisation, not exposed to the public==
- Complete Control
- Security for sensitive application
- Meet specific business needs
- Example: rackspace
#### Public Cloud
- ==Cloud resources owned and operated by third-party cloud service provider delivered over the internet==
- Six Advantages of Cloud Computing ( )
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