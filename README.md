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
<h2>Installing Active Directory</h2>
<p>
  Now that We are sure our VMs are working correctly, We can proceed to Install Active Directory inside our DC.<br>
  In the Server Manager Window, **We click on Add Roles and Features** option this will open a new window.<br>
  
  ![image](https://github.com/DsosaH/activeDirectory/assets/148100125/53d248ff-102c-49d9-9b1d-0dd932d04a23)

  Leave all as default until you reach Server Roles. Here be sure to check **Active Directory Domain Services** before continuing. Then just keep clicking next and then install at the end.<br>

  ![image](https://github.com/DsosaH/activeDirectory/assets/148100125/f0bd044d-a9a3-47ba-a782-9fe0426ff0e5)<br>

  Now We need to promote this server to a proper **Domain Controller**. After the installation finishes, a notification should appear in the upper right corner of the window with the option to begin the promotion. Click there to continue.<br>
  
  ![image](https://github.com/DsosaH/activeDirectory/assets/148100125/64ea9c75-800b-40ec-ad75-c9f8e22b95cd)

  In the new window that opens, We'll check to add a new forest and choose the name of our domain. This is a private address, so it won't appear in searches unless you are inside the domain, therefore it can be whatever you please.

  ![image](https://github.com/DsosaH/activeDirectory/assets/148100125/6e107c48-fd45-4b50-b3ba-a6b1e40f013c)

  Next, assignate a password for the **Domain Controller Options**.

  ![image](https://github.com/DsosaH/activeDirectory/assets/148100125/60d4e8ac-493a-463f-83ae-d87b00f4fe09)

  Now just let everything default, click next on all and then install. After the installation is over restart the VM.<br>
  Now, instead of entering by using our normal credential, enter by using your _domainname/username_ as shown in the image below. If you have no proble to log like this, then we can continue. <br>

  ![image](https://github.com/DsosaH/activeDirectory/assets/148100125/c96c6e5c-d4ff-4a06-b940-e369ea5c12a3)

</p>
<h2>Active Directory Configuration</h2>

<p>
  The next step is to add users to our Active Directory. Go to your search bar and look for **Active Directory Users and Computers** and open it.<br>
  Inside this window, You'll see the domain that was created and all the **Organizational Units** that come with it by default. Here is where We can create new organizational units to store, employees, clients or whatever We need. 
  
  ![image](https://github.com/DsosaH/activeDirectory/assets/148100125/c20aa29b-1fd9-46b8-b57d-da5285e764b0)<br>

  By right clicking on our domain and going _New->Organizational Unit_, We can create new OUs to store our users. In this case I created 2 as an example.<br>

  ![image](https://github.com/DsosaH/activeDirectory/assets/148100125/ad43c608-5084-4adf-9961-7def8da1d397)

  Users are created very similarly. In this example, I'll create a user inside the **_ADMINS** OS by right clicking on it and going _New->User_. Assign the credentials of your choice and watch your new user appear inside of the OS.<br>

  ![image](https://github.com/DsosaH/activeDirectory/assets/148100125/eab5a629-38f7-4192-a629-cbf1a447ee81)
  ![image](https://github.com/DsosaH/activeDirectory/assets/148100125/6d2851e8-0a9d-463b-a1f2-3766bce947f6)
  ![image](https://github.com/DsosaH/activeDirectory/assets/148100125/0a64667f-9eed-44e4-939b-dc038dff3ba7)

  

</p>
