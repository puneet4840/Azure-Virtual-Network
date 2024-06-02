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

### NSG (Network Security Group)

Network Security Group is a collection of security rules that filter incoming and outgoing traffic to and from resources like virtual machines, databases,etc.

e.g., Suppose you have a web application running on vm in azure. You want the web application to be accessible to users over the internet, for that you have to allow port (80) and port (443) so that http requests are made to the web application and users can access it. You can acheive this using the NSG. Here simply you have to open port (80) and port (443) inside inbound rules inside NSG. This is how we use the NSG and allow traffic to our resources.

**Key Concepts**

Rules: NSG contains list of security rules that define whether to allow or deny traffic based on various criteria.

Criteria: Security rules within and NSG are set either _Inbound_ or _Outbound_ and have five additional properties to determine how to handle network traffic:

- Source: The origin of the network traffic, This could be an IP Address. This means specific IP address are only allowed to access the network.

- Destination: The desination of the network traffic, This could be an Ip Address. This means incomming traffic destination.

- Port: The port number on which traffic is received (80 for HTTP, 443 for HTTPS).

- Protocol: The type of protocol used (TCP, UDP, ICMP).

**Components of NSG rule**

Priority: Each rule has priority number, lower numbers indicating higher priority. Azure processes NSG rules in order of their priority.

Action: The action can be either allow or deny, if action set to allow it allows the traffic matches the rule. If action set to deny it deny all the traffic that matches the rule.

**How NSG works?**

NSG is attached to either _Subnets_ or individual _Network Interfaces_ (NIC) of virtual machines. NSG when attached with subnet, the NSG rules apply to all resources within that subnet. NSG when attached with NIC, the NSG rules apply only to that specific NIC of virtual machine. 


### ASG (Application Security Group)

ASG are the security rules that allow to group your virtual machines and apply network security rules based on these groups rather than individually configuring each vm.

### IP Address

IP (Internet Protocol) address is the unique address for a device that is used to identify a device on the internet. 

e.g. You have a router provided by your Internet Service Provider (ISP) like we have a Jio Fiber wifi. Jio has provided a router which has a global IP address. All devices connected to this router will have the same IP Address that IP address is the local IP Address given using the DHCP protocol by the router.
If any of the devices make a request to google that means that router is making a request to google because router has the global IP address. Google sends response to router then router decides which device to send that response and that is done by NAT (Network Access Translation).

Now router knows that device 1 made the google request but which application in device 1 made that request. IP address decides which device to send the data but how to decide which application to send the data to that device. That is done by the **PORT** numbers.

### Subnet

A subnet is the small network divided form a large network.

Subnetting is the process of creating a subnet.

e.g., Suppose there is a network in a company, it has multiple departments like Finance, Payroll, Sales and Development. If company assign a single complete network to all these departments, If any employee from from sales department access malicious website and hacker got that device access through that malicous website. Now hacker can access all those device which are in the same network. This can be very dangerous situation for the company. 

To avoid this subnetting is being used. Company can create a subnet for each department in the company.

**Types of Subnet**

1 - Private Subnet: The network which does not have access to the Internet.

2 - Public Subnet: The network which has access to the Internet.
