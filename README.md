<p align="center">

  ![image](https://ticgrup.com/wp-content/uploads/2022/02/Que-es-Active-Directory_ticgrup.jpg)

</p>
<h1>Using Azure to create an On-premises configiuration of Active Directory</h1>
By this mean, I'll demonstrate how a Microsoft Active Directory server can be installed and used by using Azure Virtual Machines as the premises.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Microsoft Active Directory

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)
- Windows Server 2022

<h2>Setting Up Azure Resources</h2>
<p>
  We need to make sure that our VMs are using the correct configuration and Vnet in order for this to work properly.<br>
  First, We'll create our **Domain Controller**, this VM will act a our main server where all the data will be stored, for this we'll select **Windows Server 2022** as our operating system.
  
  ![image](https://github.com/DsosaH/activeDirectory/assets/148100125/4d92e725-1ba2-4c3d-bcf1-aac445f46a08)

  
</p>
