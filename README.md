# Setting up Splunk Enterprise on AWS
![SplunkDiagram](https://github.com/createdbymp/splunk/assets/87043765/8863b30e-f185-4f22-8e51-281f69109f1e)

## Introduction

Setting up Splunk Enterprise on AWS introduces a dynamic synergy between a leading log management platform and a cloud environment designed for agility and scale. This strategic integration empowers organizations to efficiently manage their data, enabling them to actionable insights and drive business outcomes. In this guide, we will walk through the process of deploying Splunk Enterprise on AWS, from selecting the appropriate instance type and configuring security groups, to optimizing storage options and ensuring high availability.

## Resources

Resources used to complete this project and additional documentation. 

 - Setup your AWS account [here](https://aws.amazon.com/free/?trk=be77f66f-da84-4f51-9483-df3858616660&sc_channel=ps&s_kwcid=AL!4422!10!71124885882248!71125409442309&ef_id=9b15d8ea24a7116f0317bdc13040336b:G:s&all-free-tier.sort-by=item.additionalFields.SortRank&all-free-tier.sort-order=asc&awsf.Free%20Tier%20Types=*all&awsf.Free%20Tier%20Categories=*all)
 - AWS Resources being used
	 - [VPC](https://docs.aws.amazon.com/vpc/latest/userguide/how-it-works.html)
	 - [Subnets](https://docs.aws.amazon.com/vpc/latest/userguide/configure-subnets.html)
	 - [Security Group](https://docs.aws.amazon.com/vpc/latest/userguide/security-groups.html)
	 - [EC2](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/concepts.html)
 - [Splunk Enterprise documentation](https://www.splunk.com/en_us/pdfs/tech-brief/deploying-splunk-enterprise-on-amazon-web-services.pdf)
 - Create Splunk account [here](https://www.splunk.com/en_us/download/splunk-enterprise.html) for installation package

## Setting up AWS account

 1. Login into your AWS account. If you need the login url check the **Resources** section.
 2.  Once you are logged in search VPC and click on VPC in the middle of the console to create a new one.
 3. Create your private and public subnets to configure with your VPC. [Hint] You can select 'VPC only' or 'VPC or more' to create VPC and subnets in multiple AZs together.    
 
![vpc](https://github.com/createdbymp/splunk/assets/87043765/33e259ec-45a2-4c7f-9c7b-e59874c7704a)

 4. When you create your Security Group make sure your inbound rules are as the diagram so you can SSH into your EC2 instance. Also, you will need to have port 8000 because by default this is the web port for Splunk. Outbound is not needed.

![sg](https://github.com/createdbymp/splunk/assets/87043765/079832ad-57e1-4c38-92b8-c3f772bdc91b)

 5. In this demonstration we will be using the Amazon Linux AMI for our EC2 instance. For more information on EC2 AMis following this [link.](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AMIs.html). Depending on how much compute power (CPU, Memory, Bandwidth) you use as your Instance Type determines how efficient your Splunk server runs. For this demonstration we will be using the '**t2.xlarge**' Instance Type. Make sure to create a key pair. You will need this in order SSH into the server. It is highly recommended. For more information on EC2 key pairs follow this [link](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html). Edit 'Network Settings' to select the existing Security Group and VPC you previously created and select a public subnet for your EC2 instance. 

**Beware! Running your EC2 instance does cost money**. Unless you use the free tier. 

![ec2](https://github.com/createdbymp/splunk/assets/87043765/d2c04039-2cc6-40fd-ba79-8e36248317fa)

![ec2 2](https://github.com/createdbymp/splunk/assets/87043765/c7e19ae7-8272-43a0-b020-2fc105472240)

Depending on how much data you intend to ingest into your EC2 instance determines your storage size.

![ec2storage](https://github.com/createdbymp/splunk_installation/assets/87043765/bc6c2fb4-786c-4b93-9f26-6ff15cd322c7)

## Installing Splunk on EC2 instance

 1. Create a Splunk account. In the **Resources** section, click on the 'Create Splunk account here' link. Once logged in go to Products and click on Splunk Enterprise. In this demonstration we selected a Linux EC2 instance so we will be downloading a Linux installation package, specifically the '**.tgz**' one. Copy and paste the Command Line for later use. 

![splunk1](https://github.com/createdbymp/splunk/assets/87043765/9a6c86f6-bcac-4899-844b-ea1af132c2dc)

![splunk2](https://github.com/createdbymp/splunk/assets/87043765/4a2311e8-19ce-42f1-b94d-341d2d73546d)

![wget](https://github.com/createdbymp/splunk_installation/assets/87043765/2edf4439-b6b4-486b-9a10-bc0a0eedbcf6)

 2. Now it is time to SSH into your EC2 instance. Go to your EC2 instance you previously created and click on the Instance ID. Click on 'Connect', open a terminal and please follow the instructions from the screenshot below. Make sure to use the change directory **(cd)** command to locate to your private key. Then use the SSH example to connect to your EC2 instance.

![ec2connect](https://github.com/createdbymp/splunk_installation/assets/87043765/07979597-be09-402b-9297-a9e927d894cf)

 3. 
