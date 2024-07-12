![image](https://github.com/user-attachments/assets/e1ca559c-2919-4e84-be36-97a0d9a12f7b)
</p>

<h1>Active Directory Configuration Tutorial</h1>
Configuration of Active Directory with Azure VMs.<br />
<br />
Objective 1: Setup Resources in Azure <br />
Objective 2: Ensure Connectivity between the client and Domain Controller <br />
Objective 3: Install Active Directory Domain Services + promote as DC <br />
Objective 4: Create an Admin User Account in Active Directory <br />
Objective 5: Join a client to the domain <br />
Objective 6: Allow multiple users on the domain to log into Client1<br />
Objective 7: Test case for Part 6 <br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure 
- Remote Desktop
- Internet Information Services (IIS)
- Active Directory Users and Computers
- Server Manager
- Powershell

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>List of Prerequisites</h2>

- Microsoft Azure Active Subscription (Creation of Reasearch Group, VMs, Virtual Networks, Subnets)
  
<h2>Objective 1: (Setup Resources in Azure) Steps: 1 - 17</h2>

![image](https://github.com/user-attachments/assets/fa26d93d-513c-4939-8d21-684ac1bb277a)
<p>
Step 1: Open Virtual Machines services
</p>
<br />

![image](https://github.com/user-attachments/assets/ec03abdd-ed64-4f1f-afcf-1d7b015448fa)
<p>
Step 2: Click Create Azure virtual machine
</p>
<br />

![image](https://github.com/user-attachments/assets/02de7ab0-eb5d-44ed-8078-8adfea0242da)
<p>
Step 3: Create new Resource Group and choose a name. (ex: ActiveDirectory)
</p>
<br />

![image](https://github.com/user-attachments/assets/87cfe799-266d-4180-946f-cf5842917948)
<p>
Step 4: Enter information, ie: Virtual machine name that we will use for our Domain Controller (ex DC1) image: Windows Server 2022 Datacenter: Azure Edition.
</p>
<br />

![image](https://github.com/user-attachments/assets/0cbf5f7c-7f45-46b7-8600-ed556bf47f31)
![image](https://github.com/user-attachments/assets/8fb5b250-c76d-465f-9a88-1a3b90ba63e8)<p>
Step 5: Choose at least 2 vcpus. Enter a Username/password (ex: labuser). Check in confirmation box below. Click Next.
</p>
<br />

![image](https://github.com/user-attachments/assets/6162eb01-f30a-43f3-b5aa-289fe14d8bd7)
<p>
Step 6: Click Next: Networking 
</p>
<br />

![image](https://github.com/user-attachments/assets/447acddd-eeff-41b5-a683-840c932c806c)
![image](https://github.com/user-attachments/assets/f54c3061-ebc2-46e5-8f24-de97dd131190)
![image](https://github.com/user-attachments/assets/9cc2ec31-307d-4fab-8477-a47a649562a0)
<p>
Step 7: Click Review + Create -> Click Create
</p>
<br />

![image](https://github.com/user-attachments/assets/129f4e38-e395-40a4-81d0-10faddffbb96)
<p>
Step 8: Navigate back to Virtual Machines -> Create -> Azure virtual machine.  We are going to create our client computer that will join the domain
</p>
<br />

![image](https://github.com/user-attachments/assets/9d99cb2c-fc26-4937-bdc0-c037d525dbb6)
![image](https://github.com/user-attachments/assets/1cc5b2ac-3793-4e78-ab7e-f236e657383d)
![image](https://github.com/user-attachments/assets/a8d8d8d2-4766-4a5e-9acc-d629f09c88d1)
<p>
Step 9: Fill out info ex: Choose RG we created (ex: activeDirectory). Enter name (ex: Client1). Click Review + Create -> Next -> Next: Networking
</p>
<br />

![image](https://github.com/user-attachments/assets/58fe1606-f19a-4aba-be09-1947eff4c748)
<p>
Step 10: Virtual Network: Choose the same virtual network as the Domain Controller. (should have been created when we created the DC). Click Review + create -> Create
</p>
<br />

![image](https://github.com/user-attachments/assets/2e8f19a4-6a40-40b6-a100-511f9c3572cf)
<p>
Step 11: Navigate to Virtual machines -> Click Domain Controller (ex: DC1)
</p>
<br />

![image](https://github.com/user-attachments/assets/8718fc99-e2cc-43e1-aa74-986b9f508f2e)
<p>
Step 12: Navigate on the left to Networking -> Network Settings
</p>
<br />

![image](https://github.com/user-attachments/assets/f3a9b18b-81e0-4b0e-a34f-f2bb209b2058)
<p>
Step 13: When we have a server (ex: DC1) that will offer services to another computer, (ex: we have a domain controller offering active directory services), in these cases we DONT want the ip address to change aka do not get it from DHCP, so we are gonna change domain controller virtual nic ip address from dynamic to static. Click on Network interface (ex: dc1559)
</p>
<br />

![image](https://github.com/user-attachments/assets/0323e40e-db2e-4bc4-abde-60c2df17ade1)
<p>
Step 14: Click IP configurations. When we have a server (ex: DC1) that will offer services to another computer, (ex: we have a domain controller offering active directory services), in these cases we DONT want the ip address to change aka do not get it from DHCP, so we are gonna change domain controller virtual nic ip address from dynamic to static. Click on Network interface (ex: dc1559)
</p>
<br />

![image](https://github.com/user-attachments/assets/6b7c1716-dbc8-4a93-a231-ca5b051bed16)
<p>
Step 15: Here we see the Private IP address is set to dynamic. Lets change this to Static. Click the Name (ex: ipconfig1)
</p>
<br />

![image](https://github.com/user-attachments/assets/03c8c08e-82d3-4f68-9596-14aeac0f7547)
<p>
Step 16: Change the Private IP address from dynamic to static (ex: 10.0.0.4). Click Save.
</p>
<br />

![image](https://github.com/user-attachments/assets/470574a7-eb26-4d7e-9ae5-d217ed2d7642)
![image](https://github.com/user-attachments/assets/7f31d683-9be8-4749-811f-0ece39dd55c9)
<p>
Step 17: Navigate to Virtual Machines. Ensure Both Client1 and DC1 are in the same Virtual network/subnet (ex: DC1-vnet/default)
</p>
<br />
<br />
<br />

<h2>Objective 2: (Ensure Connectivity between the client and Domain Controller) Steps: 1 - 5</h2>
