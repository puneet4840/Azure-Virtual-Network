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

e.g., Suppose there is a network in a company, it has multiple departments like Finance, Payroll, Sales and Development. If a company assign a single complete network to all these departments, If any employee from from sales department access malicious website and hacker got that device access through that malicous website. Now hacker can access all those device which are in the same network. This can be very dangerous situation for the company. 

To avoid this subnetting is being used. Company can create a subnet for each department in the company.

**Types of Subnet**

1 - Private Subnet: The network which does not have access to the Internet.

2 - Public Subnet: The network which has access to the Internet.


## Advance Networking Features

### VNet Peering

VNet peering means to connect two or more virtual networks with each other.

                                OR

VNet peering is the feature in azure that establish a direct connection between two or more virtual network with each other.

**Why do we need VNet peering**

We need VNet peering to securely communicate between the resources in the two different virtual network thorugh private IPs.

e.g., ![image](https://github.com/puneet4840/Azure-Virtual-Network/assets/65063977/a0026485-b5e1-4346-baf5-607f22a95dbd)

In the above example we have two VNets and inside those VNets there are virtual machines. So these VNets do not have direct connection (peering) between them, thus those VMs cannot communicate to each other.
To have a communication between them we need to establish a Vnet peering between those virtual networks. VNet peering here allows us to ping VM2 from VM1 using there private IP. VNet establish a secure connection so that resources can communicate without expose to the outside world.

**Types of VNet Peering**

Two types of VNet peering:-

1 - Regional VNet Peering (Same Regions):- Peering between the Vnets in the same azure regions. When two Vnets are created in the same azure region (EastUS-1) and privately connected to each other and resources inside vnets are accessible through private ips.

2 - Global VNet Peering (Different Regions):- Perring between the Vnets in the different azure regions. When two Vnets are created in the different azure regions (vnet1: EastUS, vnet2: WestUS) and privately connected to each other and resources inside the vnets are accessible through private ips.

**VNet Peering Features**

1- Direct Connectivity. 2- Low Latency. 3- High Bandwidth. 4- Resource Sharing.

**NOTE**

VNet peering does not support transitive peering. That means if Vnet-1 is peered to Vnet-2 and Vnet-2 is peered to Vnet-3 than Vnet-1 cannot connect with Vnet3 or the resources inside Vnet1 cannot access Vnet3 directly. e.g., a=b, b=c, a!=c.

**Step by Step VNet peering configuration**

Step-1: Create teo virtual networks in the same region or different regions like **VNet1**, **VNet2**.

Step-2: Now go to any of the **virtual networks** and select **Peering**, under **settings**, and then select **Add**.

![image](https://github.com/puneet4840/Azure-Virtual-Network/assets/65063977/2dc96305-90ae-4c89-b950-879f26e73b6e)

Step-3: Configuring the peering for two virtual networks and select **Add**.

![image](https://github.com/puneet4840/Azure-Virtual-Network/assets/65063977/fe8242ff-10cb-44fc-a53d-6516a046a4a7)

This Virtual Network: means the VNet 1.

Remote Virtual Network: means the VNet 2 ehich you want to peer with vnet1.

Step-4: The **PEERING STATUS** is connected, as shown in the following picture.

![image](https://github.com/puneet4840/Azure-Virtual-Network/assets/65063977/36d15c1a-56d3-4921-90c1-5129686a315b)

Step-5: Now connect any one of your vm and try to ping the private ip of second vm.

### VPN Gateway

**What is VPN?**

A VPN (Virtual Private Network) is a mechanism that creates a secure and encrypted connection between your device and a network. 

**How VPN Works?**

When you connect to a VPN, here's what happens:

1 - Connection Established: You connects to a VPN server, through a vpn client application on your device such as Nord_VPN (client application on your device).

2 - Encryption: Your data is encrypted when it leaves your device.

3 - Data Transmission: The enrypted data is sent through vpn tunnel to the VPN server from your device (Tunnel is the secure pathway).

4 - Decryption: The VPN server decrypts your data and sends it to the destination on the internet.

5 - Response Transmission: Any data coming back to you follows the same process: it is encrypted by the VPN server, sent through the tunnel, and decrypted by your VPN client.

**Real Life Examples**

e.g. Remote Work

Scenario: An employee is working from home and needs to access the company's internal network securely.

  - Without VPN: The emplyee's data travels over the internet, making it vulnerable to interception.

  - With VPN: The employee connects to company's vpn. Their data is encrypted and securely sent through the VPN tunnel to the company's network. This allows them to access internal resources like databases and file servers as if they were in the office.

**What is VPN Gateway?**

VPN Gateway is a service in azure which securely connects your (device, on-premise network, azure virtual network) to azure virtual network.

It acts as a secure bridge between your **device and azure virtual network**, **on-premise network and azure virtual network** and **between two azure virtual networks**.

We use azure vpn gateway to securely connect to azure virtual network.

**Core Components used in VPN Gateway**

1 - Virtual Network:- A private network within your azure wher you can deploy resources like vm or databases.

2 - Gateway Subnet:- A subnet for your VPN Gateway resource within a Vnet. It should ne named _GatewaySubnet_.

3 - VPN Gateway:- A vpn gateway resource that can establish secure communication.

4 - Public IP Address:- The VPN Gateway needs a public ip address to faciliate communiction over internet.

5 - Local Network Gateway:- A LNG resource that represents your on-premise network, LNG only needed in Site-to-Site connection.

**Setup and Configuration**

Step-1: Create a VNet and Gateway subnet:

- Create a VNet in azure with atleast one subnet. Add a _Gateway Subnet_ for the VPN Gateway. This subnet is crucial as it hosts the vpn gateway services.

Step-2: Deply the VPN Gateway:

- Create a VPN Gateway resource in azure and deploy it within the _Gateway Subnet_ you created earlier. During this step, you will allocate a public ip address to the vpn gateway.

Step-3: Create a Local Network Gateway (for site-to-site configuration):

- For site-to-site connections, define a local network gateway that represents your on-premise network

**Establishing the VPN Connection**

