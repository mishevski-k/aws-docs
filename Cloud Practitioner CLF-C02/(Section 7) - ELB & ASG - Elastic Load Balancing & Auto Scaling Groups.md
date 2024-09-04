
### Scalability & High availability 
- Scalability means that an application / system can handle greater loads by adapting
- There are two kinds of scalability
	- Vertical Scalability
	- Horizontal Scalability ( = elasticity )
- Scalability is linked but different to High Availability 

### Vertical Scalability 
- Vertical scalability means increasing the size of the instance
- For example, you application runs on t2.micro
	- Scaling the application means running it on a t2.large
- Vertical scalability is very common for non distributed systems, such as databases
- There's usually a limit to how much you can vertically scale ( hardware limit )

### Horizontal Scalability 
- Horizontal scalability means increasing the number of instances / systems for you application
- Horizontal scalability implies distributed systems
- This is very common for web applications / modern applications


### High Availability 
- High Availability usually goes hand in hand with horizontal scaling
- High Availability means running your application / system in at least 2 Availability Zones
- The goal of high availability is to survive a data center loss ( disaster )

### High Availability & Scalability for EC2
- Vertical Scaling: Increase instance size ( = scale up / down )
	- From: t2.nano - 0.5GB of Ram, 1 vCPU
	- To: 12tbl.metal - 12.3TB of Ram, 448 vCPUs
- Horizontal Scaling: Increase number of instances ( = scale out / in )
	- Auto Scaling Group
	- Load Balancer
- High Availability: Run instances for the same application across multi AZ
	- Auto Scaling Group multi AZ
	- Load Balancer multi AZ

### Scalability vs Elasticity ( vs Agility )
- Scalability: ability to accommodate a larger load by making the hardware stronger ( scape up ), or by adding nodes ( scale out )
- Elasticity: once a system i scalable, elasticity means that there will be some "auto-scaling" so that the system can scale based on the load. This is "cloud-friendly": pay-per-use, match demand, optimise cost
- Agility: ( not related to scalability - distractor ) new IT resources are only one click away, which means that you can reduce the time to make those resources available to your developers from weeks to just minutes

### What is load balancing?
- Load balancers are servers that forward internet traffic to multiple servers ( EC2 Instances ) downstream

### Why use a load balancer?
- Spread load across multiple downstream instances
- Expose a single point of access ( DNS ) to your application
- Seamlessly handle failures of downstream instances
- Do regular health checks to your instances
- Provide SSL termination ( HTTPS ) for your website
- High availability across zones

### Why use an Elastic Load Balancer?
- an ==ELB== ( Elastic Load Balancer ) is a managed load balancer
	- AWS guarantees that it will be working
	- AWS takes care of upgrades, maintenance, high availability
	- AWS provides only a few configuration knobs
- It costs less to setup your own load balancer but it will be a lot more effort on your end ( maintenance, integrations)
- 4 kinds of load balancers offered by AWS:
	- Application Load Balancer ( HTTP /. HTPPS only ) - Layer 7
	- Network Load Balancer ( ultra-high performance, allows TCP ) - Layer 4
	- Gateway Load Balancer - Layer 3
	- Classic Load Balancer ( retired 2023 ) - Layer 4 & 7


| Application Load Balancer                 | Network Load Balancer                             | Gateway                                                     |
| ----------------------------------------- | ------------------------------------------------- | ----------------------------------------------------------- |
| HTTP / HTTPS / gRPC protocols ( Layer 7 ) | TCP / UDP protocols ( Layer 4 )                   | GENEVE Protocol on IP Packets ( Layer 3 )                   |
| HTTP routing features                     | High performance: millions of request per seconds | Route Traffic to Firewalls that you manage on EC2 Instances |
| Static DNS ( URL )                        | Static IP through Elastic IP                      | Intrusion detection                                         |

### What's an Auto Scaling Group
- In real-life, the load on your websites and application can change
- In the cloud, you can create and get rid of servers very quickly
- The goal of an Auto Scaling Group ( ==ASG== ) is to:
	- Scale out ( add EC2 instances ) to match increased load
	- Scale in ( remove EC2 instances ) to match decreased load
	- Ensure we have an minimum and maximum number of machines running
	- Automatically register new instances to load balancer
	- Replace unhealthy instances
- Cost Savings: only run at an optimal capacity ( principle of the cloud )

### Auto Scaling Group consists
- Minimum amount instances
- Desired amount of instances
- Maximum amount instances

### Auto Scaling Groups - Scaling Strategies 
- Manual Scaling: Update the size of an ASG manually
- Dynamic Scaling:
	- Simple / Step Scaling
		- When a CloudWatch alarm is triggered ( example CPU > 70% ), then add units
		- When a CloudWatch alarm is triggered ( example CPU < 30% ), then remove 1
	- Target Tracking Scaling
		- Example: I want the average ASG CPU to stay at around 40%
	- Scheduled Scaling
		- Anticipate a scaling based on know usage patterns
		- Example: increase the min. capacity to 10 at 5pm on Fridays
- Predictive Scaling
	- Use Machine Learning to predict future traffic ahead of time
	- Automatically provisions the right number of EC2 instances in advance
	- Useful when you load has predictable time based patterns

### ELB & ASG - Summary
- High Availability vs Scalability ( vertical vs horizontal ) vs Elasticity vs Agility in the cloud
- Elastic Load Balances ( ==ELB== )
	- Distribute traffic across backend EC2 instances, can be Multi-AZ
	- Support health checks
	- 4 types: 
		- Classic ( old - depreciated )
		- Application ( HTTP & HTTPS - Layer 7 )
		- Network ( UTP & TCP - Layer 4 )
		- Gateway ( Layer 3 )
- Auto Scaling Groups ( ==ASG== )
	- Implement elasticity for you application across multiple AZ
	- Scale EC2 instances based on demand on your system, replace unhealthy
	- Integrate with the ELB



	