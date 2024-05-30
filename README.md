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
