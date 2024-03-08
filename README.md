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
But before we start, let's change the settings of our Arun-Public-Subnet to allow auto-assign of public IPv4 IP addresses. <br>
Select <strong>Arun-Public-Subnet</strong>: <br>
1.	Click <strong>Actions</strong>. <br>
2.	Select <strong>Edit subnet settings</strong>. <br>
3.	Check <strong>Enable auto-assign public IPv4 address</strong>. <br>
4.	Click <strong>Save</strong>.<br>

![image](https://github.com/arundhik97/AWS-VPC/assets/38269066/a6dbddf4-0af5-4ae2-b61a-6c3454e83a35)

Now let's go ahead and build our internet gateway:
1.	Navigate to the <strong>Internet Gateways</strong> section in the VPC service.
2.	Click <strong>Create Internet Gateway</strong>.
3.	Create a new internet gateway with the following setting:<br>
            o	Name tag: <strong>Arun-IGW</strong>
4.	Click <strong>Create Internet Gateway</strong>.
<img width="640" alt="Arun-IGW" src="https://github.com/arundhik97/AWS-VPC/assets/38269066/4a6a286d-2493-43c2-a3ad-7b9889ef6d04">
   Let's attach it to our Arun-VPC:
1.	Select <strong>Arun-IGW</strong>. <br>
2.	Click <strong>Actions</strong>. <br>
3.	Select <strong>Attach to VPC</strong>. <br>
4.	Select <strong>Arun-VPC</strong>. <br>
5.	Click <strong>Attach Internet Gateway</strong>. <br>

<img width="643" alt="image" src="https://github.com/arundhik97/AWS-VPC/assets/38269066/4e8b712e-4c34-4f31-a85c-656a7ddefe43">

We now have a way to get public IP addresses to our instances, but we don't have a route created to direct traffic from our public subnet to the internet gateway. <br>
Let's create a route table and add a route to our internet gateway. <br>
<h1> Create Route Tables</h1>
A route table contains a set of rules, called routes, that are used to determine where network traffic is directed. It is no different from a routing table in a router. As a network engineer, we should be familiar with the concept. <br>
Let's create a route table for our CiscoU-Public-Subnet: <br>
1.	Navigate to the <strong>Route tables</strong> section in the VPC service. <strong>Notice that we have a default route table that was created when we created our VPC.</strong> <br>
2.	Click <strong>Create route table</strong>. <br>
3.	Create a new route table with the following settings: <br>
o	Name tag: <strong>Arun-Public-RT</strong> <br>
o	VPC: <strong>Arun-VPC</strong> <br>
4.	Click <strong>Create route table.</strong> <br> 
<img width="640" alt="Arun-Public-RT" src="https://github.com/arundhik97/AWS-VPC/assets/38269066/e040f3d1-5fc3-4f0a-b4f9-563a037482e8">

You now have a way to direct traffic from your public subnet to the internet gateway, but we have to define a route to do that. <br>
1.	Select <strong>Arun-Public-RT</strong>.
2.	In the Routes tab, click <strong>Add routes</strong>. <br>
<img width="642" alt="Default route to IGW" src="https://github.com/arundhik97/AWS-VPC/assets/38269066/cdceaef7-2911-43f2-8a1b-2e4217e30701">

<strong>Notice that we have a default route to resolve all traffic to the local VPC. This is a default route that was created when we created our VPC</strong>. <br>
3.Let's create a <strong>catch all</strong> route that will allow us to reach the public internet. - Destination: <strong>0.0.0.0/0</strong> - Target: <strong>Internet Gateway</strong> - Select <strong>Arun-IGW</strong>. <br>
4. Click <strong>Save routes</strong>.<br>

Next, we need to associate our Arun-Public-RT to our Arun-Public-Subnet.
1.	Select the <strong>Subnet Association </strong>tab.
2.	Click <strong>Edit subnet associations</strong>.
3.	Select <strong>Arun-Public-Subnet</strong>.
4.	Click <strong>Save associations</strong>. <br>
We now have a public subnet that has a route to the internet.<br>
Let's attach some computing to our newly created network.<br>

<h1>Launch Public EC2 Instance</h1>
EC2 is a web service that provides secure, resizable computing capacity in the cloud. Think of it as a virtual machine in the cloud.<br>
EC2 can help with:<br>
•	Deploying applications quickly <br>
•	Scaling applications <br>
•	Providing developers with complete control of their computing resources <br>
•	Reducing the time required to obtain and boot new server instances to minutes, allowing you to quickly scale capacity, both up and down, as your computing requirements change. <br>
Let's launch an EC2 instance in our Arun-Public-Subnet.<br>
Navigate to the <strong>EC2</strong> service: <br> <br>
1.	In the search bar, type <strong>EC2</strong> and click the service. <br>
2.	In the left pane, click <strong>Instances</strong>. <br>
3.	Click <strong>Launch Instance</strong>. <br> <br>
Here is where we will configure our EC2 instance:<br>
1.	Give your instance a name: <strong>Arun-EC2-Pub</strong> <br>
2.	Select an Amazon Machine Image (AMI): <strong>Amazon Linux 2023 AMI</strong> <br>
3.	Architecture: <strong>64-bit (x86)</strong> <br>
4.	Instance Type: <strong>t2.micro free tier eligible</strong> <br>
5.	Key pair: <strong>Create a new key pair</strong> <br>
o	Key pair name: <strong>Arun-EC2-Key-Pub</strong> <br>
o	Key pair type: <strong>RSA</strong> <br>
o	Key pair file format: <srong>pem</srong> for Mac and Linux, <strong>ppk</strong> for Windows <br>
o	Click <strong>Create key pair</strong>. <br>
o	Download the key pair and save it in a safe place. You will need it to use Secure Shell (SSH) into your public instance. <br>
6.	In the Network Settings section, click <strong>Edit</strong>. Let's make sure that we are launching our instance in the right subnet: <br>
o	Network: <strong>Arun-VPC</strong> <br>
o	Subnet: <strong>Arun-Public-Subnet</strong><br>
o	Auto-assign Public IP: <strong>Enable</strong> <br>
o	Firewall (Security Group): <strong>Create a new security group</strong> <br>
	Security group name: <strong>Arun-EC2-Pub-SG</strong> <br>
	Description: <strong>Arun-EC2-Pub-SG</strong> <br>
	Type: <strong>SSH</strong> <br>
	Source: <strong>MY IP</strong>. <strong>Make a note of your IP address!</strong> For example,  <strong>69.181.208.75/32</strong>.
	Click <strong>Add Rule</strong>. <br>
7.	Add another rule to allow SSH traffic: <br>
o	Type: <strong>SSH</strong> <br>
o	Source type: <strong>Custom</strong> <br>
o	Source: Our VPC CIDR block, which is <strong>10.0.0.0/16</strong> <br>
The rest of the settings can be left as is. <br>
8.	Scroll down and click <strong>Launch instance</strong>. <br>
9.	Once launched, click <strong>View All Instances</strong> to see your instance. <br>
Next, let's launch an EC2 instance in our Arun-Private-Subnet. <br>


