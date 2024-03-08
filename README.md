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

First, let's create a VPC: <br>
1.	Log in to our AWS account <br>
2.	Navigate to the <strong>VPC service </strong>. <br>
3.	Click <strong>Create VPC </strong>. <br>
4.	Under VPC Settings, select <strong>VPC Only </strong>. <br>
5.	Create a new VPC with the following settings: <br>
o	Name tag: <strong>Arun-VPC </strong> <br>
o	IPv4 CIDR block:  <strong>10.0.0.0/16 </strong> <br>
o	IPv6 CIDR block: <strong> No IPv6 CIDR Block </strong><br>
o	Tenancy: <strong>Default </strong> <br>
6.	Click <strong>Create VPC </strong>. <br>

<h2> Create Public Subnet</h2>
A public subnet is a subnet that has a route to the internet. It is usually used for resources that need access from the internet. In this case, the resource will be an <strong> EC2 instance</strong>.<br>
1.	Navigate to the <strong>Subnets </strong> section in the VPC service.<br>
2.	Click <strong>Create subnet</strong>.<br>
3.	Create a new subnet with the following settings:<br>
o	VPC ID: <strong>Arun-VPC </strong> <br>
o	Subnet name: <strong>Arun-Public-Subnet </strong><br>
o	Availability Zone: <strong>No Preference </strong> <br>
o	IPv4 CIDR block: <strong>10.0.1.0/24 </strong> <br>
4.	Click <strong>Create subnet. </strong>
<img width="1241" alt="VPC Public Subnet" src="https://github.com/arundhik97/AWS-VPC/assets/38269066/54176de9-b115-46b2-8b09-9a53a9d5f87f"> <br>
A few things to note: <br>
•	Although we have a /16 CIDR block, we are using <strong>/24 </strong>, meaning that we are using 256 addresses for our subnet.<br>
•	We are not selecting an availability zone, meaning that AWS will choose an availability zone for us. <br>
•	Although the name of our subnet is Arun-Public-Subnet, it is not a public subnet yet. We still need to create a route to the internet.
<h1> Create Private Subnet</h1>
Having a private subnet allows us to have resources to restrict internet access, which is excellent for security—maybe a Vault server that houses all secrets and tokens. We don't want that to be accessible from the internet. <br>
Let's configure our private subnet: <br>
1.	Navigate to the <strong>Subnets</strong> section in the VPC service. <br>
2.	Click <strong>Create subnet</strong>. <br>
3.	Create a new subnet with the following settings: <br>
o	VPC ID: <strong>Arun-VPC</strong> <br>
o	Subnet name: <strong>Arun-Private-Subnet</strong> <br>
o	Availability Zone: <strong>No Preference</strong> <br>
o	IPv4 CIDR block: <strong>10.0.2.0/24</strong> <br>
4.	Click <strong>Create subnet</strong>. 

<img width="1242" alt="VPC Private Subnet" src="https://github.com/arundhik97/AWS-VPC/assets/38269066/dcb96983-f731-4fe7-a6c8-6f0a06dbff81">

Our next steps are to create an <strong> internet gateway </strong>and configure our <strong>route tables</strong> to make our subnets reachable from the internet.
<h1>Create Internet Gateway</h1>
•	An internet gateway is a horizontally scaled, redundant, and highly available VPC component that allows communication between instances in your VPC and the internet. <br>
•	An internet gateway is not a router. It does not perform any routing functions. It simply serves as a point of entry and exit for traffic going to and from the internet.<br>
•	An internet gateway is typically attached to a subnet, enabling instances in the subnet to communicate with the internet. In our case, we will attach it to our public subnet, Arun-Public-Subnet.
But before we start, let's change the settings of our Arun-Public-Subnet to allow auto-assign of public IPv4 IP addresses.
![image](https://github.com/arundhik97/AWS-VPC/assets/38269066/97ebd6eb-507f-478b-8492-2f4226e343a0)

Select <strong>Arun-Public-Subnet</strong>:
1.	Click <strong>Actions</strong>.
2.	Select <strong>Edit subnet settings</strong>.
3.	Check <strong>Enable auto-assign public IPv4 address</strong>.
4.	Click <strong>Save</strong>.<br>
Now let's go ahead and build our internet gateway:
1.	Navigate to the Internet Gateways section in the VPC service.
2.	Click Create Internet Gateway.
3.	Create a new internet gateway with the following setting:
o	Name tag: CiscoU-IGW
4.	Click Create Internet Gateway.
Great! Let's attach it to our CiscoU-VPC:
1.	Select CiscoU-IGW.
2.	Click Actions.
3.	Select Attach to VPC.
4.	Select CiscoU-VPC.
5.	Click Attach Internet Gateway.

