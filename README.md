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

## Step by Step

 1. Login into your AWS account. If you need the login url check the **Resources** section.
 2.  Once you are logged in search VPC and click on VPC in the middle of the console to create a new one.
 3. Create your private and public subnets to configure with your VPC.
![vpc](https://github.com/createdbymp/splunk/assets/87043765/b6d62170-55dc-46d0-9fdf-62105f2ea3c8) 
 
 4. Create your Security Group
 5. Create your EC2 instance
 6. Create a Splunk account

