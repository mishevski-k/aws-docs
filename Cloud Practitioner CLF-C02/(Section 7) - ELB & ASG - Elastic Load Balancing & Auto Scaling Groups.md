
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
