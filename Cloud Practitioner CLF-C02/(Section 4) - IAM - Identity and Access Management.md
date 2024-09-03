

### IAM: Users & Groups
- IAM = Identity and Access Management
- Root account created by default on signup, shouldn't be used or shared
- Users are people within your organisation, and can be grouped
- Groups only contain users, not other groups
- Users don't have to belong to a group ( not best practice ), and users can belong to multiple groups

### IAM: Permissions
- Users or Groups can be assigned JSON documents called policies
- These policies define the permissions of the user
- In AWS you apply the ==least privilege principle==: don't give more permissions than a user needs

```
{
	"Version": "2012-10-17",
	"Statement": [
		{
			"Effect": "Allow",
			"Action": "ec2:Describe*",
			"Resources": "*"
		},
		{
			"Effect": "Allow",
			"Action": "elasticloadbalancing:Describe*",
			"Resources": "*"
		},
				{
			"Effect": "Allow",
			"Action": [
				"cloudwatch:ListMetrics",
				"cloudwatch:GetMetricStatistics",
				"cloudwatch:Describe*",
			],
			"Resources": "*"
		}
	]
}
```


### IAM Policies Structure
- Consists of 
	- ==Version==: policy language version, always include "2012-10-17"
	- ==Id==: and identifier for the policy ( optional )
	- ==Statement==: one or more individual statements
- Statement consists of
	- ==Sid==: an identifier for the statement ( optional )
	- ==Effect==: whatever the statement allows or denies access ( Allow, Deny )
	- ==Principal==: account / user / role to which this policy is applied to
	- ==Action==: list of actions this policy allows or denies
	- ==Resource==: list of resources to which the actions applied to
	- ==Condition==: conditions for when this policy is in effect ( optional )

### IAM - Password Policy
- String passwords = higher security of your account
- In AWS, you can  setup a password policy:
	- Set minimum password length
	- Require specific character types:
		- including uppercase letters
		- lowercase letters
		- numbers
		- non-alphanumeric characters
	- Allow all IAM users to change their own passwords
	- Require users to change their password after some time ( password expiration )
	- Prevent password re-use

### Multi Factor Authentication - MFA
- Users have access to your account and can possibly change configurations or delete resources in your AWS account
- You want to protect your Root Accounts and IAM users
- MFA = password you know + security device you own
- ==Main benefit of MFA==:
	- if a password is stolen or hacked, the account is not compromised


### How can users access AWS?
- To access AWS, you have three options:
	- AWS Management Console ( protected by password + MFA )
	- AWS Command Line Interface ( ==CLI== ): protected by access keys
	- AWS Software Development Kit ( ==SDK== ) - for code: protected by access keys
- Access keys are generated through the AWS Console
- Users manage their own access keys
- ==Access keys are secret, just like password, Don't share them==
- Access Key ID ~= username
- Secret Access Key ~= password


### What's the AWS CLI
- A tool that enables you to interact with AWS services using commands in you command-line shell
- Direct access to public APIs of AWS services
- You can develop scripts to manage your resources
- It's open source https://github.com/aws/aws-cli
- Alternative to using AWS Management Console

### What's the AWS SDK
- AWS Software Development Kit ( AWS SDK )
- Language-specific APIs ( set of libraries )
- Enables you to access and manage AWS services programatically 
- Embedded within you application
- Supports
	- SDKs ( Javascript, Python, PHP, .NET, Ruby, Java, GO, Node.js, c++ ...)
	- Mobile SDKs ( Android, iOS, ...)
	- IoT Device SDKs ( Embedded C, Arduino, ...)
- Example: AWS CLI is build on AWS SDK for Python

### Link to install AWS CLI 
https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html

### Link to AWS SDKs
https://aws.amazon.com/developer/tools/


### IAM Roles for Services
- Some AWS Services will need to perform actions on your behalf
- To do so, we will assign permissions to AWS Services with IAM Roles
- Common Roles:
	- EC2 Instance Roles
	- Lambda Function Roles
	- Roles for CloudFormation


### IAM Security Tools
- IAM Credentials Report ( account-level )
	- a report that lists all your account's users and the status of their various credentials
- IAM Access Advisor ( user-level )
	- Access advisor shows the service permissions granted to a user and when those services were last  accessed
	- You can use this information to revise your policies


### ==IAM Guidelines & Best Practices==
- Don't use the root account except for AWS account setup
- ==ONE== physical user = ==ONE== AWS user
- Assign users to groups and assign permissions to groups
- Create a strong password policy
- Use and enforce the use of Multi Factor Authentication ( ==MFA== )
- Create and use Roles for giving permissions to AWS Services
- Use Access Keys for Programmatic Access ( ==CLI== / ==SDK== )
- Audit permission of your account using IAM Credentials Report & IAM Access Advisor
- ==Never share IAM users & Access Keys==


### Shared Responsibility Model for IAM
- AWS
	- Infrastructure ( global network security )
	- Configuration and vulnerability analysis
	- Compliance validation
- You
	- Users, Groups, Roles, Policies management and monitoring
	- Enable MFA on all accounts
	- Rotate all your keys often
	- Use IAM tool to apply appropriate permissions
	- Analyse access patterns & review permissions


### IAM Section - Summary
- ==Users==: mapped to a physical user, has password for AWS Console.
- ==Groups==: contains users only
- ==Policies==: Json document that outlines permissions for users or groups
- ==Roles==: for EC2 instances of AWS Services
- ==Security==: MFA + Password Policy
- ==AWS CLI==: manage AWS services using the command-line
- ==AWS SDK==: manage AWS services using programming language
- ==Access Keys==: access AWS using the CLI or SDK
- ==Audit==: IAM Credential Report and IAM Access Advisor