![AwsGIF (2)](https://github.com/arundhik97/AWS-VPC/assets/38269066/2dc0707f-d6e4-470d-a902-5e0074135510)

 # AWS-VPC
 <!DOCTYPE html>
 <html>
 <body>
  <h2> VPC </h2>
  VPC stands for Virtual Private Cloud, which is a virtual network dedicated to your AWS account. It is logically isolated from other virtual networks in the AWS Cloud.
<h2> Subnet </h2>
A subnet is a range of IP addresses in your VPC. We can launch AWS resources into a subnet that you select.
<h2> Internet gateway </h2> 
An internet gateway is a horizontally scaled, redundant, and highly available VPC component that allows communication between instances in our VPC and the internet.
  <h2> EC2 </h2>
EC2 stands for Elastic Compute Cloud, a web service that provides secure, resizable computing capacity in the cloud. Think of it as a virtual machine in the cloud.
The rest is basic networking concepts. We need to create subnets, route tables, and security groups. <br>
 We also need to create network ACLs.
<br>
 We have a VPC with two subnets—one public and one private. We also have an internet gateway to configure and create routes between our subnets.

<img width="691" alt="VPC" src="https://github.com/arundhik97/AWS-VPC/assets/38269066/4e84fce5-fd47-4739-8997-52251c9f11da">

![image](https://github.com/arundhik97/AWS-VPC/assets/38269066/faf483ed-4685-481b-a97a-aa8ffcb7b75c)
<h2> Create Public Subnet</h2>
A public subnet is a subnet that has a route to the internet. It is usually used for resources that need access from the internet. In this case, the resource will be an EC2 instance.<br>
1.	Navigate to the Subnets section in the VPC service.<br>
2.	Click Create subnet.<br>
3.	Create a new subnet with the following settings:<br>
o	VPC ID: Arun-VPC <br>
o	Subnet name: Arun-Public-Subnet <br>
o	Availability Zone: No Preference <br>
o	IPv4 CIDR block: 10.0.1.0/24 <br>
4.	Click Create subnet.
<img width="1241" alt="VPC Public Subnet" src="https://github.com/arundhik97/AWS-VPC/assets/38269066/54176de9-b115-46b2-8b09-9a53a9d5f87f"> <br>
A few things to note: <br>
•	Although we have a /16 CIDR block, we are using /24, meaning that we are using 256 addresses for our subnet.<br>
•	We are not selecting an availability zone, meaning that AWS will choose an availability zone for us. <br>
•	Although the name of our subnet is Arun-Public-Subnet, it is not a public subnet yet. We still need to create a route to the internet.
<h1> Create Private Subnet</h1>
Having a private subnet allows us to have resources to restrict internet access, which is excellent for security—maybe a Vault server that houses all secrets and tokens. You don't want that to be accessible from the internet. <br>
All right, let's configure our private subnet: <br>
1.	Navigate to the Subnets section in the VPC service. <br>
2.	Click Create subnet. <br>
3.	Create a new subnet with the following settings: <br>
o	VPC ID: Arun-VPC <br>
o	Subnet name: Arun-Private-Subnet <br>
o	Availability Zone: No Preference <br>
o	IPv4 CIDR block: 10.0.2.0/24 <br>
4.	Click Create subnet. 


