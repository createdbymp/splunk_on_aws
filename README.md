# Setting up Splunk Enterprise on AWS

![splunk_aws](https://github.com/createdbymp/splunk_on_aws/assets/87043765/4b25d364-d15c-4f34-ad4e-368cfebdb88e)

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
 
![vpc](https://github.com/createdbymp/splunk_on_aws/assets/87043765/f0beae17-a52d-4555-ae5d-3f6cc90c8e83)

 4. When you create your Security Group make sure your inbound rules are as the diagram so you can SSH into your EC2 instance. Also, you will need to have port 8000 because by default this is the web port for Splunk. Outbound is not needed.

![sg](https://github.com/createdbymp/splunk_on_aws/assets/87043765/b3b91bce-fdcc-48f9-b56f-48db89e057b7)

 5. In this demonstration we will be using the Amazon Linux AMI for our EC2 instance. For more information on EC2 AMis following this [link.](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AMIs.html). Depending on how much compute power (CPU, Memory, Bandwidth) you use as your Instance Type determines how efficient your Splunk server runs. For this demonstration we will be using the '**t2.xlarge**' Instance Type. Make sure to create a key pair. You will need this in order SSH into the server. It is highly recommended. For more information on EC2 key pairs follow this [link](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html). Edit 'Network Settings' to select the existing Security Group and VPC you previously created and select a public subnet for your EC2 instance. 

**Beware! Running your EC2 instance does cost money. Please make sure to Hibernate your instance when not in use.** 

![ec2](https://github.com/createdbymp/splunk_on_aws/assets/87043765/af8d00ec-9b4d-46e2-b6b3-0d8574945dc5)

![ec2 2](https://github.com/createdbymp/splunk_on_aws/assets/87043765/7070b0f8-0f81-4b9c-8e92-7959bdcfb032)

Depending on how much data you intend to ingest into your EC2 instance determines your storage size.

![ec2storage](https://github.com/createdbymp/splunk_on_aws/assets/87043765/c15088e4-6f66-4e9e-98a0-3464eed2ee81)

## Installing Splunk on EC2 instance

 1. Create a Splunk account. In the **Resources** section, click on the 'Create Splunk account here' link. Once logged in go to Products and click on Splunk Enterprise. In this demonstration we selected a Linux EC2 instance so we will be downloading a Linux installation package, specifically the '**.tgz**' one. Copy and paste the Command Line for later use. 

![splunk1](https://github.com/createdbymp/splunk_on_aws/assets/87043765/05eff846-a3e0-4b5c-bfab-4de1a52010ea)

![splunk2](https://github.com/createdbymp/splunk_on_aws/assets/87043765/9f11ebb6-d14d-4f55-ae76-d6b91298c6b7)

![wget](https://github.com/createdbymp/splunk_on_aws/assets/87043765/1f9f9a81-bbd9-434c-8422-e92660dc61e9)

 2. Now it is time to SSH into your EC2 instance. Go to your EC2 instance you previously created and click on the Instance ID. Click on 'Connect', open a terminal and please follow the instructions from the screenshot below. Make sure to use the change directory **(cd)** command to locate to your private key. Then use the SSH example to connect to your EC2 instance.

![ec2connect](https://github.com/createdbymp/splunk_on_aws/assets/87043765/2307df7b-835f-41c8-afdb-8f0b981eb88f)

 3. Once you execute the ssh command to remote into your EC2 server, you should have a welcome screen like below. Now it is time to make a folder for Splunk installation package to be extracted into. Use the command **`sudo mkdir /opt/splunk`** (Linux) for Windows you would be **`/Program Files/splunk`**. Then make your **ec2-user** the owner of that directory. To do use the command **`sudo chown ec2-user /opt/splunk`**.

![ec2login](https://github.com/createdbymp/splunk_on_aws/assets/87043765/eaa71244-f256-4550-845e-be89afed0de6)

 4. It is finally time to use the wget command we saved earlier for the Splunk installation. Make sure you cd into /opt/splunk folder then paste the wget command and run it! 

Here it is if you missed it - **`wget -O splunk-9.1.1-64e843ea36b1-Linux-x86_64.tgz "https://download.splunk.com/products/splunk/releases/9.1.1/linux/splunk-9.1.1-64e843ea36b1-Linux-x86_64.tgz"`**

 5. Once it is complete do the 'ls' command to see the .tgz file inside your `/opt/splunk` directory. Now you have to extract that file. Make sure you are in the /opt/splunk directory before doing so.

Here is the command to extract the zip file - **`tar -xzvC /opt -f <paste .tgz file>`**. Make sure to paste the zip file name after -f.

![tar](https://github.com/createdbymp/splunk_on_aws/assets/87043765/78c566af-7680-4e12-b26e-8d284441cc41)

 6. The zip file has been extracted. Now you should have folders inside the directory you created. Cd into bin. This is the folder you will execute your splunk commands. Once you are in the bin folder do the **`./splunk`** start command to start Splunk. 

![splunk-bin](https://github.com/createdbymp/splunk_on_aws/assets/87043765/881b9e56-7644-4abc-9a00-5e1f294cdde2)

 7.  It should prompt you to create a username and password. Please take note of that username and password. You will need it to login. Once that is complete it will give you the URL needed to login into Splunk Enterprise. Copy and paste that URL into the web browser and you should see the login page. You remember the username and password you created earlier in the terminal? You will use that to login. Congrats! You have officially deployed Splunk Enterprise on AWS.

![final 1](https://github.com/createdbymp/splunk_on_aws/assets/87043765/a6472447-f26a-491d-9124-9242f9178978)

![final 2](https://github.com/createdbymp/splunk_on_aws/assets/87043765/11210c64-1270-464a-97a8-ee09057ebd05)

## Conclusion

Splunk is a robust platform for managing, analyzing, and deriving insights from machine-generated data. Its infrastructure includes forwarders, indexers, search heads, and specialized servers for centralized control. Splunk's capabilities encompass data ingestion, indexing, powerful search, visualization, correlation, alerting, and machine learning. It excels in security, compliance, scalability, and customization, making it invaluable for IT operations, security, business intelligence, and various other applications. Theres so much that can be done, however, this project was only to get Splunk installed. 
