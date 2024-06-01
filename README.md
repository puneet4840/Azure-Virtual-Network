# Azure-Virtual-Network

### What is Virtual Network in Azure?

A virtual network (VNet) is a private network in the cloud which allows azure resources such as virtual machines to securely communicate to each other, or on internet, or on-premises network.

**Why do we need Virtual Network?**

E.g. Suppose there are two devops engineers, one from Pums and one from Nike. They both devops engineers wants to create a virtual machine in azure cloud in East-us region and inside availability zone 1. Azure has created two virtual machines in the east-us region inside availablity zone 1. 

Now hacker hacked one of the vm. So, there is a possibility of that second vm can also easily be hacked by the hacker because the both vms are in the same region and same availability zone. This is the problem when there is not the concept of virtual netwrok like if one vm is hacked then other all vm in the same region and same availability zone can also be hacked.

This problem can be solved by the concept of virtual network-

Suppose Nike and Puma's devops engineer need vms in the same region and same availabilty zone. Here Azure can create vm in the same region and availability zone and attach those vm with their virtual network, where devops engineers can allow selected people to access the virtual machine. Then azure can give the option to devops engineers to create a virtual network that is private network and the resources inside the virtual network are only accessible by the user of that virutal machine only because no one can access the virtual network directly untill access is given to anyone.

This is how azure secure the people's resources using the virtual network. Virtual network create a logical isolation inside the azure's on-premise network. Virtual Network is only the isolation of resources.

e.g. A hospital might have a virtual network with a subnet for patient record databases and another subnet for administrative systems. This keeps sensitive patient data seperate from everyday administrative tasks.

**Components of Virtual Network**

Components are like when we create a vnet, what are the things created with it?

1 - Subnet.

2 - NSG (Network Security Grougs).

3 - IP Addresses.

4 - Firewall.

5 - Route Tables.

**NSG (Network Security Group)**

Network Security Group is a collection of security rules that filter incoming and outgoing traffic to and from resources like virtual machines, databases,etc.

Security rules are like which traffic can come to our resource and which traffic can not come to resource. e.g. Port 80, Port 443, SSH 22, etc.

Suppose you have a web application running on vm in azure. You want the web application to be accessible to users over the internet, for that you have to allow port (80) and port (443) so that http requests are made to the web application and users can access it. You can acheive this using the NSG. Here simply you have to open port (80) and port (443) inside inbound rules inside NSG. This is how we use the NSG and allow traffic to our resources.
