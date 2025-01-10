# Creating a Virtual Machine on Azure

You can use this guide to create a virtual machine in Azure. It will explain every parameter you need to configure to create a virtual machine successfully. It will also explain the not so well known parameters that you might want to consider. 

## Table of Contents
- [Prerequisites](#prerequisites)

## Prerequisites
Before we begin, make sure you have the following:

- An Azure subscription
- Basic knowledge of virtual machines and cloud computing concepts

## Step 1: Sign in to Azure Portal
1. Open your web browser and go to the Azure Portal (https://portal.azure.com).
2. Sign in using your Azure account credentials.

## Step 2: Create a Virtual Machine
1. In the Azure Portal, click on the "Create a resource" button.
2. Search for "Virtual Machine" and select the "Virtual Machine" option from the search results.
3. Click on the "Create" button to start the virtual machine creation process.

## Step 3: Basics Tab
On the Basics tab, you will configure the basic settings for your virtual machine. Here are the parameters you need to fill in:

- **Subscription**: Select the Azure subscription you want to use.
- **Resource group**: Choose an existing resource group or create a new one. Resource groups are used to organize things that share the same lifecycle. An exmaple of resources that share the same lifecycle are a virtual machine, a virtual network, and a storage account. Another example is a web app, a database, and a storage account.
- **Virtual machine name**: Enter a name for your virtual machine. Best practice for naming a virtual machine is to use a name that describes the purpose of the virtual machine. For example, if you are creating a virtual machine for a web server, you can name it "webserver-01".
- **Region**: Select the Azure region where you want your virtual machine to be located. You want to choose a region that is closest to your users to reduce latency. If you are in Colorado, you might want to choose the West US region. If you are in Virginia, you might want to choose the East US region. For more information about Azure regions, see [Azure Regions](https://azure.microsoft.com/en-us/global-infrastructure/regions/).
- **Availability options**: Choose the availability options for your virtual machine. 
    + **No infrastructure redundancy** is the default option & it means that your VM will be deployed to a single physical server. If the physical server fails, your VM will be down until the physical server is repaired. 
    + **An availability set** is a group of virtual machines that are deployed across multiple physical servers. If one physical server fails, your VM will be moved to another physical server in the availability set. This will reduce downtime for your VM. 
    + **Virtual machine scale sets** distributes your VMs across multiple physical servers. This is used for high availability and scalability. The most expensive option of the three is the virtual machine scale sets. The lowest cost option is no infrastructure redundancy. For more information about availability options, see [Availability options for virtual machines in Azure](https://docs.microsoft.com/en-us/azure/virtual-machines/availability). 
- **Security type**: 
    + **Standard**: This is a basic level of security for your virtual machines. 
    + **Trusted launch**: Protects against advanced threats like rootkits and bootkits with configurable features like Secure Boot, Virtual Trusted Platform Module (vTPM), and System Guard Secure Launch.
    + **Confidential computing**: Protects data in use with confidential computing capabilities.
- **Availability Zone**: Choose the availability zone for your virtual machine.
- **Image**: Choose the operating system image for your virtual machine. 
    If you **click on "see all images"**, it will take you to the marketplace where you can choose from a variety of images.
    + You can also **configure VM generation'**. Gen 1 VMs supports older operating systems. Gen 2 VMs support newer operating systems.

    Run with Azure Spot discount basically means that you are willing to accept the possibility that your VM might be deallocated if Azure needs the capacity back. In return, you get a discount on the VM.
- **Size**: Select the size of your virtual machine based on your workload requirements.
    + **B-series**: for light burstable workloads that don't use the full CPU all the time.
    + **D-series**: for general-purpose workloads.
    + **F-series**: for compute-intensive workloads & CPU focused. 
    + **E-series**: for memory-intensive workloads.
    + **NV-series**: for GPU workloads.
It can be really hard to understand letters that come after the VM family and number of cores. Here is a quick breakdown. 
    + [Family] + [Number of Cores] + [Number of Constraint Cores] + [Attributes] + [Version Number] 
For more information about the attributes, see [VM Skus Explained] (https://getnerdio.com/resources/azure-vms-explained-understanding-vm-skus-and-attributes/)
- **VM Architecture**
    + **x86**: Provide the most software compatibility.
    + **Arm64**: Arm64-based VMs provide up to 50% better price-performance than comparable x64 VMs.
- **Size**: Select the size of your virtual machine based on your requirements.
- **Username**: Enter a username for accessing your virtual machine.
- **Password**: Set a password for the username you provided.

Once you have filled in all the required parameters, click on the "Next" button to proceed to the next tab.

## Step 4: Disks Tab
On the Disks tab, you can configure the disk settings for your virtual machine. Here are the parameters you need to consider:

- **OS disk type**: Choose the type of disk for the operating system.
- **Data disks**: Add any additional data disks if required.

Once you have configured the disk settings, click on the "Next" button to proceed.

## Step 5: Networking Tab
On the Networking tab, you can configure the network settings for your virtual machine. Here are the parameters you need to configure:

- **Virtual network**: Select the virtual network you want to use.
- **Subnet**: Choose the subnet within the virtual network.
- **Public IP**: Decide whether you want to assign a public IP address to your virtual machine.
- **Network security group**: Configure the network security group rules for inbound and outbound traffic.

After configuring the networking settings, click on the "Next" button to proceed.

## Step 6: Management Tab
On the Management tab, you can configure additional management settings for your virtual machine. Here are some parameters you might want to consider:

- **Boot diagnostics**: Enable boot diagnostics for troubleshooting purposes.
- **Monitoring**: Enable monitoring for your virtual machine.
- **Auto-shutdown**: Set a schedule for automatically shutting down your virtual machine.

Once you have configured the management settings, click on the "Next" button to proceed.

## Step 7: Review + Create
On the Review + Create tab, review all the settings you have configured for your virtual machine. If everything looks good, click on the "Create" button to start the virtual machine creation process.

## Conclusion
By following these steps and configuring the parameters on each tab, you can create a virtual machine on Azure. Remember to review your settings carefully before creating the virtual machine.
 