<h2>
<img width="120" alt="Microsoft Azure Logo" src="images/AzureImage.png">
Active Directory Lab – Virtual Machine Environment Setup
</h2>

<h3>Prerequisites</h3>

<p>
Before beginning this lab, you must have a <strong>Microsoft Azure account with an active subscription</strong>. 
Azure provides the cloud infrastructure used to deploy the virtual machines, networking, and other resources required to build the Active Directory environment.
</p>

<p>
If you do not already have one, Microsoft offers a free Azure account that includes limited credits for learning and testing purposes.
</p>

<br/>

<h3>Creating a Resource Group</h3>

<p>
In the Azure Portal, begin by searching for <strong>Resource Groups</strong> in the search bar at the top of the page. 
Resource groups allow you to organize related Azure resources together so they can be managed, monitored, and deleted as a single unit.
</p>

<p>
<img width="1400" alt="Search Resource Groups" src="images/01-DC.png">
</p>

<p>
Once inside the Resource Groups page, select <strong>Create</strong> to begin creating a new resource group for the lab environment.
</p>

<p>
<img width="1400" alt="Create Resource Group Page" src="images/02-DC.png">
</p>

<p>
During the creation process, configure the following settings:
</p>

<ul>
<li><strong>Subscription:</strong> Azure subscription 1</li>
<li><strong>Resource Group Name:</strong> ActiveDirectoryLab</li>
<li><strong>Region:</strong> Central US</li>
</ul>

<p>
Resource groups act as logical containers for all the resources associated with a specific project or environment. 
In this case, the resource group will hold the virtual machines, virtual networks, and supporting infrastructure required for the Active Directory lab.
</p>

<p>
<img width="1400" alt="Configure Resource Group Settings" src="images/03-DC.png">
</p>

<p>
After reviewing the configuration settings, select <strong>Create</strong> to deploy the resource group.
</p>

<p>
<img width="1400" alt="Review and Create Resource Group" src="images/04-DC.png">
</p>

<p>
Once the deployment is complete, the new resource group should appear in the list of available resource groups within Azure.
</p>

<p>
<img width="1400" alt="Resource Group Created Successfully" src="images/05-DC.png">
</p>

<br/>

<h3>Preparing to Configure the Virtual Network</h3>

<p>
Next, search for <strong>Virtual Networks</strong> using the Azure search bar. 
Virtual networks allow Azure resources such as virtual machines to communicate with each other privately within the same network environment.
</p>

<p>
Virtual networking is essential for Active Directory because the Domain Controller and client machines must be able to communicate with each other over the internal network.
</p>

<p>
<img width="1400" alt="Search Virtual Networks" src="images/06-DC.png">
</p>

<br/>

<h3>Creating the Virtual Network</h3>

<p>
From the Virtual Networks page, select <strong>Create</strong> to begin creating a new virtual network for the Active Directory lab environment.
</p>

<p>
<img width="1400" alt="Virtual Networks Page" src="images/07-DC.png">
</p>

<p>
When creating the virtual network, configure it within the same resource group created earlier. 
This ensures that all infrastructure used for the Active Directory lab remains organized within a single logical container in Azure.
</p>

<p>
<img width="1400" alt="Create Virtual Network Configuration" src="images/08-DC.png">
</p>

<p>
For this lab, configure the virtual network with the following settings:
</p>

<ul>
<li><strong>Subscription:</strong> Azure subscription 1</li>
<li><strong>Resource Group:</strong> ActiveDirectoryLab</li>
<li><strong>Virtual Network Name:</strong> ActiveDirectory-Vnet</li>
<li><strong>Region:</strong> Central US</li>
</ul>

<p>
A virtual network (VNet) in Azure functions similarly to a traditional internal network within a physical data center. 
It allows virtual machines and other resources deployed inside the network to communicate with each other privately and securely.
</p>

<p>
<img width="1400" alt="Review Virtual Network Configuration" src="images/09-DC.png">
</p>

<p>
After reviewing the configuration settings, select <strong>Create</strong> to deploy the virtual network.
</p>

<p>
<img width="1400" alt="Virtual Network Deployment Complete" src="images/10-DC.png">
</p>

<br/>

<h3>Preparing to Create the Domain Controller Virtual Machine</h3>

<p>
Next, search for <strong>Virtual Machines</strong> in the Azure search bar. 
Virtual machines will be used to simulate systems within the Active Directory environment, including the Domain Controller and client machines.
</p>

<p>
<img width="1400" alt="Search Virtual Machines in Azure" src="images/11-DC.png">
</p>

<p>
From the Virtual Machines page, select <strong>Create</strong> to begin deploying the first virtual machine for the lab.
</p>

<br/>

<h3>Creating the Domain Controller Virtual Machine</h3>

<p>
In the virtual machine creation menu, begin configuring the first system that will serve as the <strong>Domain Controller</strong> for the lab environment.
</p>

<p>
<img width="1400" alt="Domain Controller VM Basic Configuration" src="images/13-DC.png">
</p>

<p>
During the basic configuration stage, assign the virtual machine to the previously created resource group and region. 
For this lab, the virtual machine is named <strong>DC-01</strong>, which will represent the Domain Controller for the Active Directory environment.
</p>

<p>
<img width="1400" alt="Selecting Windows Server Image and VM Size" src="images/14-DC.png">
</p>

<p>
The operating system image selected for this virtual machine is <strong>Windows Server 2025 Datacenter: Azure Edition</strong>. 
Windows Server provides the necessary services required to install and manage Active Directory Domain Services (AD DS).
</p>

<p>
The VM size selected is <strong>Standard_D2s_v3</strong>, which provides 2 virtual CPUs and 8 GB of memory. 
This configuration is sufficient for running a Domain Controller within a lab environment.
</p>

<p>
<img width="1400" alt="Configuring Administrator Credentials" src="images/15-DC.png">
</p>

<p>
Next, configure the local administrator account credentials for the virtual machine. 
These credentials will be used to initially log into the server once the virtual machine is deployed.
</p>

<p>
<img width="1400" alt="Allowing RDP Inbound Port" src="images/16-DC.png">
</p>

<p>
Remote Desktop Protocol (RDP) on port <strong>3389</strong> is enabled so the virtual machine can be accessed remotely after deployment. 
RDP allows administrators to connect to the Windows Server interface from their local computer in order to configure the server.
</p>

<p>
<img width="1400" alt="Networking Configuration for Domain Controller VM" src="images/17-DC.png">
</p>

<p>
Within the networking configuration, ensure that the virtual machine is connected to the previously created virtual network <strong>ActiveDirectory-Vnet</strong>. 
This allows the server to communicate with other virtual machines that will later be deployed in the same lab environment.
</p>

<p>
<img width="1400" alt="Virtual Machine Deployment Complete" src="images/18-DC.png">
</p>

<p>
After reviewing all configuration settings, select <strong>Create</strong> to deploy the virtual machine. 
Once deployment finishes successfully, the Domain Controller virtual machine will be available within the resource group and ready for further configuration.
</p>

<br/>

<h3>Creating the Client Virtual Machine</h3>

<p>
Next, create a second virtual machine that will act as a <strong>client workstation</strong> within the Active Directory environment.
This machine will later be joined to the domain and used to simulate a standard user computer within the network.
</p>

<p>
<img width="1400" alt="Searching for Virtual Machines in Azure" src="images/01-Client.png">
</p>

<p>
From the search results, select <strong>Virtual Machines</strong> to navigate to the list of existing virtual machines in the Azure environment.
</p>

<p>
<img width="1400" alt="Virtual Machines Page" src="images/02-Client.png">
</p>

<p>
Select <strong>Create</strong> and then choose <strong>Virtual Machine</strong> to begin deploying the client system.
</p>

<p>
<img width="1400" alt="Create Client Virtual Machine" src="images/03-Client.png">
</p>

<p>
During the basic configuration stage, assign the virtual machine to the same resource group used earlier for the Domain Controller.
For this lab, the virtual machine is named <strong>Client1</strong>.
</p>

<p>
<img width="1400" alt="Selecting Windows 11 Image for Client VM" src="images/04-Client.png">
</p>

<p>
The operating system selected for the client system is <strong>Windows 11 Pro</strong>. 
This operating system will represent a typical workstation that would exist within a corporate Active Directory environment.
</p>

<p>
<img width="1400" alt="Configuring Administrator Credentials for Client VM" src="images/05-Client.png">
</p>

<p>
Next, configure the administrator credentials that will be used to initially log into the client machine once it has been deployed.
</p>

<p>
<img width="1400" alt="Allowing RDP Access to Client VM" src="images/06-Client.png">
</p>

<p>
Remote Desktop Protocol (RDP) is enabled so that the client machine can be accessed remotely after deployment.
This allows administrators to remotely manage and configure the virtual machine from their local computer.
</p>

<p>
<img width="1400" alt="Networking Configuration for Client VM" src="images/07-Client.png">
</p>

<p>
When configuring the networking settings, it is important that the client virtual machine is connected to the 
<strong>same virtual network (ActiveDirectory-Vnet)</strong> as the Domain Controller.  
This ensures both machines exist on the same internal network and can communicate with each other, which is required for the client machine to later join the Active Directory domain.
</p>

<p>
<img width="1400" alt="Client VM Deployment Complete" src="images/08-Client.png">
</p>

<p>
After reviewing the configuration settings, select <strong>Create</strong> to deploy the client virtual machine.
Once the deployment completes successfully, the client system will be ready for domain configuration and further Active Directory testing.
</p>

<br/>

<h3>Configuring the Domain Controller Private IP Address</h3>

<p>
Before configuring the client machine, the Domain Controller’s private IP address should be set to <strong>static</strong>. 
This ensures the server always maintains the same internal address within the network.
</p>

<p>
<img width="1400" alt="Searching for Virtual Machines to access DC networking" src="images/01-Static:Client.png">
</p>

<p>
Navigate to the <strong>DC-01</strong> virtual machine and open the <strong>Networking</strong> settings.
</p>

<p>
<img width="1400" alt="Opening Domain Controller network settings" src="images/02-Static:Client.png">
</p>

<p>
Select the network interface attached to the Domain Controller to view the IP configuration settings.
</p>

<p>
<img width="1400" alt="Opening DC network interface configuration" src="images/03-Static:Client.png">
</p>

<p>
Inside the network interface configuration, open the <strong>IP configuration</strong> settings.
</p>

<p>
<img width="1400" alt="Viewing IP configuration for the Domain Controller" src="images/04-Static:Client.png">
</p>

<p>
Change the private IP address allocation from <strong>Dynamic</strong> to <strong>Static</strong>.
</p>

<p>
<img width="1400" alt="Setting Domain Controller private IP to static" src="images/05-Static:Client.png">
</p>

<p>
Setting the Domain Controller’s IP address to <strong>static</strong> is important because other machines on the network will rely on this address to locate critical services such as <strong>Active Directory authentication and DNS</strong>. 
If the IP address were assigned dynamically and later changed, client systems might no longer be able to locate the Domain Controller, which could cause authentication and domain connectivity issues.
</p>

<br/>

<h3>Configuring the Client Virtual Machine DNS Settings</h3>

<p>
Next, configure the client virtual machine to use the Domain Controller as its DNS server.
</p>

<p>
<img width="1400" alt="Opening Client VM network settings" src="images/06-Static:Client.png">
</p>

<p>
Within the network interface settings for <strong>Client1</strong>, navigate to the <strong>DNS servers</strong> configuration page.
</p>

<p>
<img width="1400" alt="Setting custom DNS server on Client VM" src="images/07-Static:Client.png">
</p>

<p>
Select <strong>Custom DNS</strong> and enter the Domain Controller’s static private IP address <strong>(10.0.0.4)</strong>.
</p>

<p>
Configuring the client machine to use the Domain Controller’s IP address for DNS ensures that the client sends its DNS queries directly to the Domain Controller. 
Active Directory environments rely heavily on DNS to locate domain services, authenticate users, and allow machines to join the domain. 
By pointing the client to the Domain Controller’s static IP address, the system can reliably locate the domain infrastructure once Active Directory services are installed.
</p>



<p>
<img width="1400" alt="Create Virtual Machine Menu" src="images/12-DC.png">
</p>

