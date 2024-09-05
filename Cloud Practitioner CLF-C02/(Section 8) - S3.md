
### Intro
- Amazon S3 is one of the main building blocks of AWS
- It's advertised as "infinity scaling" storage
- Many websites use Amazon S3 as a backbone
- Many AWS services use Amazon S3 an an integration as well

### Amazon S3 Use cases
- Backup and Storage
- Disaster Recovery
- Achieve 
- Hybrid Cloud Storage
- Application hosting
- Media hosting
- Data lakes & big data analytics
- Software delivery
- Static website

### Amazon S3 - Buckets
- Amazon S3 allows people to store objects ( file ) in "buckets" ( directories )
- Buckets must have a globally unique name ( across all regions all accounts )
- Buckets are defined at the region level
- S3 looks like a global service but buckets are created in a region
- Naming convention
	- No uppercase, No underscore
	- 3 - 63 characters long
	- Not an IP
	- Must start with lowercase letter or number
	- Must ==NOT== start with prefix ==xn--==
	- Must ==NOT== end with suffix ==-s3alias==


### Amazon S3 - Objects
- Objects ( files ) have a key
- The ==key== is the full ==FULL== path:
	- s3://my-bucket/my_file.txt
	- s3://my-bucket/my_folder/another_folder/my_file.txt
- The key is compromised of a prefix + object name
- There's no concept of "directories" within buckets ( although the UI will trick you to think otherwise )
- Just keys with very long names that contain slashes ( "/" )

### Amazon S3 - Objects ( Content )
- Objects values are the content of the body:
	- Max Object Size is 5TB
	- If uploading more than 5GB, must use "multi-part upload"
- Metadata ( list of text key / value pairs - system or user metadata )
- Tags ( Unicode key / value pair - up to 10) - useful for security / lifecycle
- Version ID ( if versioning is enabled )

### Amazon S3 - Security
- User-Based 
	- IAM Policies - which API calls should be allowed for specific user from iAM
- Resource-Based
	- Bucket policies - bucket wide rules from the S3 console - allow cross account
	- Object Access Control List ( ==ACL== ) - finer grain ( can be disabled )
	- Bucket Access Control List ( ==ACL== ) - less common ( can be disabled )
- Note: an IAM principal can access an S3 object if
	- The user iAM permissions ALLOW it OR the resource policy ALLOWS it AND there's no DENY
- Encrypt: encrypt objects in Amazon S3 using encryption keys


### S3 Bucket Policies
- JSON based policies
	- Resources: buckets and objects
	- Effect: Allow / Deny
	- Actions: Set of API to Allow or Deny
	- Principal: The account or user to apply the policy to
- Use S3 Bucket Policy to
	- Grand public access to the bucket
	- Force objects to be encrypted on upload
	- Grand access to another account ( Cross Account )

```
{
	"Version": "2012-10-17",
	"Statement": [
		{
			"Sid": "PublicRead",
			"Effect": "Allow",
			"Principal": "*",
			"Actions": [
				"s3:GetObject"
			],
			"Resources": [
				"arn:aws:s3:::examplebucket/*"
			]
		}
	] 
}
```


### Bucket Settings for Block Public Access
- Block all public access
- These settings were created to prevent company data leaks
- If you know your buckets should never be public, leaves this on
- Can be set at the account level


### Amazon S3 - Static Website Hosting
- S3 can host static websites and have them accessible on the internet
- The Url will be ( depending on the region )
	- http://bucket-name.s3-website-aws-region.amazonaws.com
	- http://bucket-name.s3-website.aws-region.amazonaws.com
- Public read must be enabled, if not we are getting 403 error


### Amazon S3 - Versioning
- You can version your files in Amazon S3
- It is enabled at the bucket level
- Same key overwrite will change the "version": 1, 2, 3, ...
- It is best practice to version your buckets
	- Protect against unintended deletes ( ability to restore a version )
	- Easy rollback to previous version
- Notes
	- Any file that is not versioned prior enabling versioning will have version "null"
	- Suspending versioning does not delete previous versions


### Amazon S3 - Replication ( CRR & SRR )
- Must enable Versioning in source and destination buckets
- Cross-Region Replication ( ==CRR== )
- Same-Region Replication
- Buckets can be in different AWS accounts
- Copying is asynchronous
- Must give proper IAM permissions to S3
- Use cases:
	- CRR - compliance, lower latency access, replicate across accounts
	- SRR - log aggregation, live replication between production and test accounts


### S3 Storage Classes
- Amazon S3 Standard - General Purpose
- Amazon S3 Standard-infrequent Access ( ==IA== )
- Amazon S3 One Zone-infrequent  Access
- Amazon S3 Glacier Instant Retrieval
- Amazon S3 Glacier Flexible Retrieval
- Amazon S3 Glacier Deep Achieve
- Amazon S3 Inteligent Tiering
- Can move between classes manually or using S3 Lifecycle configurations

### S3 Durability and Availability
- Durability 
	- High durability ( 99.99999999999 , 11 9's ) of objects across multiple AZ
	- if you store 10,000,000 objects with Amazon S3, you can on average expect to incur a loss of single object once every 10,000 years
	- Same for all storage classes
- Availability
	- Measures how readily available a service is
	- Varies depending on storage class
	- Example: S3 standard has 99.99% availability = not available 53 minutes a year

### S3 Standard - General Purpose
- 99.99% Availability
- Used for frequently accessed data
- Low latency and high throughput
- Sustain 2 concurrent facility failures
- Use Cases
	- Big Data analytics
	- mobile & gaming applications
	- content distributions ...

### S3 Storage Classes - Infrequent Access
- For data that is less frequently accessed, but required rapid access when needed
- Lower cost than S3 Standard
- Amazon S3 Standard-Infrequent Access ( S3 Standard-IA )
	- 99.9% Availability
	- Use cases
		- Disaster recovery
		- Backups
- Amazon S3 One Zone-Infrequent Access ( S3 One Zone-IA )
	- High durability ( 99,99999999999% ) in a single AZ, lost data when AZ Is destroyed
	- 99.5% Availability
	- Use cases
		- Storing secondary backup copies of on-premise data, or data you can recreate

### Amazon S3 Glacier Storage Classes
- Low-cost object storing meant for archiving / backup
- Pricing: price for storage + object retrieval cost
- Types
	- Amazon S3 Glacier Instant Retrieval
		- Milliseconds retrieval, great for data accessed once a quarter
		- Minimum storage duration of 90days
	- Amazon S3 Glacier Flexible Retrieval ( formerly Amazon S3 Glacier )
		- Tiers
			- Expedited ( 1 to 5 minutes )
			- Standard ( 3 to 5 hours )
			- Bulk ( 5 to 12 hours ) - free
		- Minimum storage duration of 90 days
	- Amazon S3 Glacier Deep Archive - for long term storage
		- Tiers
			- Standard ( 12 hours )
			- Bulk ( 48 hours )
		- Minimum storage duration of 180 days

### S3 Intelligent-Tiering
- Small monthly monitoring and auto-tiering fee
- Moves objects automatically between Access tiers based on usage
- There are no retrieval charges in S3 Intelligent-Tiering
- Tiers
	- Frequent Access tier ( automatic ): default tier
	- Infrequent Access tier ( automatic ): objects not accessed for 30 days
	- Archive Instant Access tier ( automatic ): objects not accessed for 90days
	- Archive Access tier ( optional ): configurable from 90 days to 700+ days
	- Deep Archive Access tier ( optional ): configurable from 180 days to 700+ days


### IAM Access Analyser for S3
- Ensures that only intended people have access to your S3 buckets
- Example: publicly accessible bucket, bucket shared with other AWS account . . .
- Evaluates S3 Bucket Policies, S3 ACLs, S3 Access Point Policies
- Powered by IAM Access Analyser

### Shared Responsibility Model for S3
- AWS
	- Infrastructure ( global security, durability, availability, sustain concurrent loss of data in two facilities )
	- Configuration and vulnerability analyses
	- Compliance validation
- You
	- S3 Versioning
	- S3 Bucket Policies
	- S3 Replication Setup
	- Logging & Monitoring
	- S3 Storage Classes
	- Data encryption at rest and in transit


### AWS Snow Family
- High-secure, portable devices to collect and process data at the edge, and migrate into and out of AWS
- Types
	- Snowcone
	- Snowball Edge

|                  | Snowcone              | Snowball Edge   |
| ---------------- | --------------------- | --------------- |
| Storage Capacity | 8 TB HDD -  14 TB SSD | 80 TB - 210 TB  |
| Migration Size   | Up to terabytes       | Up to petabytes |


### Data Migrations with AWS Snow Family
- Challenges
	- Limited connectivity
	- Limited bandwidth
	- High network cost
	- Shared bandwidth ( can't maximise the line )
	- Connection stability
- AWS Snow Family is a offline device to perform data migrations
	- If it takes more than a week to transfer over the network, use Snowball devices


### Snow Family - Usage Process
1. Request Snowball device from AWS console for delivery
2. Install the snowball client / AWS OpsHub on your servers
3. Connect the snowball to your servers and copy files using the client
4. Ship back the device when you're done ( goes to the right AWS facility )
5. Data will be loaded into a S3 bucket
6. Snowball is completely wiped ( will be send to a new customer )


### What is Edge Computing
- Process data while it's being created on an edge location
	- A truck on the road, a ship on the sea, mining station underground
- These locations may have limited internet and no access to computing power
- We setup a Snowball Edge / Snowcone device to do edge computing
	- Snowcone: 2 CPUs, 4 GB of memory, wired or wireless access
	- Showball Edge: Computing Optimised ( dedicated for that use case ) & Storage Optimised
	- Run EC2 Instances or Lambda functions at the edge
- Use cases
	- preprocess data
	- machine learning
	- transcoding media


### Snowball Edge Pricing
- You pay for device usage and data transfers ==OUT== of AWS
- Data transfers ==IN== to Amazon S3 is free
- Types
	- On-Demand
		- includes a one-time service fee per job which includes
			- 10 days of usage for Snowball Edge Storage Optimised 80 TB
			- 15 days of usage for Snowball Edge Storage Optimised 210 TB
		- Shipping days are ==NOT== counted towards the included 10 or 15 days
		- Pay per day for any additional days
	- Committed Upfront
		- Pay in advance for monthly 1-year and 3-years of usage ( Edge Computing )
		- Up to 62% discount pricing



### Hybrid Cloud for Storage
- AWS pushing for "hybrid cloud"
	- Part of your infrastructure is on-premise
	- Part of your infrastructure is on the cloud
- This can be due to
	- Long cloud migrations 
	- Security requirements 
	- Compliance requirements
	- IT strategy
- S3 is propriety storage technology ( unlike EFS / NFS ), so you need to use a AWS Storage Gateway to expose the S3 data on-premise


### AWS Storage Cloud Native Options
- Block
	- Amazon EBS
	- EC2 Instance Store
- File
	- Amazon EFS
- Object 
	- Amazon S3
	- Glacier


### AWS Storage Gateway
- Bridge between on-premise data and cloud data in S3
- Hybrid storage service to allow on-premises to seamlessly use the AWS Cloud
- Use cases
	- disaster recovery
	- backup & restore
	- tiered storage
- Types of Storage Gateway
	- File Gateway
	- Volume Gateway
	- Tape Gateway
- Out of scope for exam other than knowing what a storage gateway is and usecase


### Amazon S3 - Summary
- Buckets vs Objects: global unique name, tied to a region
- S3 Security: IAM policy, S3 Bucker policy ( public access ), S3 Encryption
- S3 Websites: host a static websiti on S3
- S3 Versioning: multiple versions for files, prevent accidental deletes
- S3 Replication: same-region or cross-region, must enable versioning
- S3 Storage Classes: Standard, IA, 1Z-IA, Intelligent, Glacier ( Instant, Flexible, Deep )
- Snow Family: import data onto S3 through a physical device, edge computing
- OpsHub: desktop application to manage Snow Family Devices
- Storage Gateway: hybrid solution to extend on-premises storage to S3

