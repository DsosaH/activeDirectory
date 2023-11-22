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
  
  ![image](https://github.com/DsosaH/activeDirectory/assets/148100125/4d92e725-1ba2-4c3d-bcf1-aac445f46a08) <br/>

  Create another VM, but make this one a normal **Windows 10 OS**, this one will be our VM acting as a client of the **Active Directory DC**. Make sure that both VMs are inside the same Vnet group, this is very important.<br>
  Once both VMs are deployed, We'll need to make some changes to ensure correct connection. For this we simply go to our DC VM's Network Settings and select our Network Interface.<br>

  ![image](https://github.com/DsosaH/activeDirectory/assets/148100125/50c4c7a2-e476-4bd2-9030-45abebe6a715) <br>
  
  Then we'll go into the IP Configurations and then into the IPConfig of type IPv4 that we have added automatically. As you can see, by default, this IP is set to Dynamic, however, in order for the clients VM to connect and not worry about getting out of the DC, we need to make the DC's IP Static, this way our IP will stay always the same and no need to enter a new one will be needed in the future.
  
  ![image](https://github.com/DsosaH/activeDirectory/assets/148100125/f03659e1-bcfc-451e-bbf8-d5f66b311143)<br>

Inside ipconfig, simply change dynamic to static and take note of the IP that is assigned because it'll be necessary for the future. Save and now the IPv4 should appear as Static.<br>

![image](https://github.com/DsosaH/activeDirectory/assets/148100125/97479b5a-14c4-4645-891e-d28d00ac2e06)
![image](https://github.com/DsosaH/activeDirectory/assets/148100125/0c672a9b-2dad-48cf-92ef-13c3def1897b)<br/>

Now in order to ensure that connection is working correctly, we are going to use ICMP from the Client's VM to try and ping the DC.<br>
If we tried to ping the DC right now, We'd have no response because the DC's Firewall is not allowing inbound ICMPv4. To fix this We need to go into our DC's Firewall Settings and enable the inbound rule to allow ICMPv4 first. Be sure that both of the shown rules are enabled. <br>

![image](https://github.com/DsosaH/activeDirectory/assets/148100125/1fd73648-270a-40e8-b041-5827a3ab3357)

Now if We ping, there should be a proper reply, so We are good to continue.

![image](https://github.com/DsosaH/activeDirectory/assets/148100125/cca81786-ad80-4d9b-b2f3-b5a486ce5e67)
  
</p>
