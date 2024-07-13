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
Step 13: Click IP configurations.When we have a server (ex: DC1) that will offer services to another computer, (ex: we have a domain controller offering active directory services), in these cases we DONT want the ip address to change aka do not get it from DHCP, so we are gonna change domain controller virtual nic ip address from dynamic to static. Click on Network interface (ex: dc1559)
</p>
<br />

![image](https://github.com/user-attachments/assets/0323e40e-db2e-4bc4-abde-60c2df17ade1)
<p>
Step 14: Here we see the Private IP address is set to dynamic. Lets change this to Static. Click the Name (ex: ipconfig1)
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

![image](https://github.com/user-attachments/assets/723b15b8-29b9-4738-905e-0edb729de37b)
<p>
Step 1: If we log in to Client1 and ping DC1, it will fail. We need to log in to our Domain Controller(DC1) and enable ICMPv4 on the local windows Firewall. Copy IP address from DC1 (ex:52.228.79.205) -> Use this to RDC into DC1 -> Enter credentials (ex:labuser/password)
</p>

![image](https://github.com/user-attachments/assets/6628faeb-70f3-4813-a0bb-8dbeaa55a31a)
<p>
Step 2: Open Windows Defender Firewall with Advanced Security
</p>
<br />

![image](https://github.com/user-attachments/assets/cc29f55b-9e61-4650-8c9d-588efff53929)
![image](https://github.com/user-attachments/assets/1652b8bc-d853-47b6-97c3-0bb5c0abd481)
<p>
Step 3: Click Inbound Rules -> Enable both ICMP Echo Requests on protocol ICMPv4
</p>
<br />

![image](https://github.com/user-attachments/assets/a118f457-8719-4aa3-aad3-e65daf746d31)
<p>
Step 4: Minimize DC1 -> RDC into Client1
</p>
<br />

![image](https://github.com/user-attachments/assets/55d1c509-2b32-4e15-95da-f5d0283682fd)
<p>
Step 5: Open Command Line -> echo ping the Domain Controller's private IP address (ex: 10.0.0.4) -> Confirm connectivity is working -> close command lin -> minimize Client 1
</p>
<br />
<br />
<br />

<h2>Part 3: (Install Active Directory Domain Services + promote as DC) Steps: 1 - 5</h2>

![image](https://github.com/user-attachments/assets/2f225a45-c603-45a0-a48d-d44a9a5d600d)
<p>
Step 1: RDC into DC1. In Server Manager click Add roles and features -> next -> next -> next
</p>
<br />

![image](https://github.com/user-attachments/assets/d7434a87-32f9-4ba6-b082-f0be962fa38f)
<p>
Step 2: Check the box for Active Directory Domain Services -> Add Features -> next through all dependencies -> install
</p>
<br />

![image](https://github.com/user-attachments/assets/bec271da-cbbd-48b7-98ce-12c5abf76afb)
<p>
Step 3: Click exclamation in top right corder of Server Manager -> Click "Promote this server to a domain controller"
</p>
<br />

![image](https://github.com/user-attachments/assets/d83ff733-bbd9-4ed9-bee2-a5d45da4eba0)
<p>
Step 4: Choose Add a new forest -> Add a root domain name (ex: mydomain.com) -> Next
</p>
<br />

![image](https://github.com/user-attachments/assets/b845316f-3a86-4baa-b2e4-de6f1efd6e17)
<p>
Step 5: Enter a password -> Next through all checks -> Install -> Computer will restart when finished -> RDC back into DC1 after restart -> May have to enter username with domain: (username: mydomain.com\labuser)
</p>
<br />

![image](https://github.com/user-attachments/assets/8d513049-fae1-48fe-8488-4dd04ce541f5)
<p>
Domain Controller is online with domain set up.
</p>
<br />
<br />
<br />


<h2>Part 4: (Create an Admin User Account in Active Directory) Steps: 1 - 7</h2>

![image](https://github.com/user-attachments/assets/24ccca06-a926-40f2-9e31-e62c22134e31)
<p>
Step 1: Navigate to Active Directory Users and Computers
</p>
<br />

![image](https://github.com/user-attachments/assets/554e2d1f-56f8-437e-9e76-93bede2ff4fa) 
![image](https://github.com/user-attachments/assets/d8b43806-1c57-474e-9d30-3340b82a6cf2)
<p>
Step 2: Create a new Organizational Unit (ex: _EMPLOYEES). note: underscore in name makes it easier to filter. Create another OU (ex: _ADMINS)
</p>
<br />

![image](https://github.com/user-attachments/assets/eb610b5a-0b8d-461c-b14d-22e4a5ebd771)
![image](https://github.com/user-attachments/assets/2d2bbc18-39e3-4f34-a329-dcefd4727a79)
<p>
Step 3: We can continue using labuser, however ambiguous account names are not best practices. We are going to create another ADMIN account that is tied to an identity. Right click _ADMINS to create a new user.
</p>
<br />

![image](https://github.com/user-attachments/assets/1972bec6-f0e6-4d12-940e-ed793645efe1)
<p>
Step 4: Fill out information for the new user. (ex: jerry_admin) -> Next -> Set Password
</p>
<br />

![image](https://github.com/user-attachments/assets/c8d1ea1f-ff03-4f96-bcca-88f11a7d0185)
<p>
Step 5: Go to properties of user we want to give admin permissions
</p>
<br />

![image](https://github.com/user-attachments/assets/2f990c75-0046-4766-a40a-dec3c9040db2)
<p>
Step 6: Click Member of -> enter domain and click Check Names -> Domain Admins -> Ok -> Ok -> Apply
</p>
<br />

![image](https://github.com/user-attachments/assets/1a1601a3-66ce-4c37-a93d-c11cdb8a0339)
![image](https://github.com/user-attachments/assets/3a5c2df1-9c87-40bd-95f1-d7a682fc9a45)
<p>
Step 7: Log out of Domain Controller(currently is labuser), log back in as our new user (ex:jerry_admin)
</p>
<br />
<br />
<br />


<h2>Part 5: (Join a client to the domain) Steps: 1 - 8</h2>

![image](https://github.com/user-attachments/assets/ecf0835e-4495-4a3b-8126-2bea29c3a689)
Step 1: Navigate to Domain Controller(ex: DC1) Virtual Machine -> Network settings -> copy private IP ADDRESS (ex: 10.0.0.4)
FYI: We are planning to join a client computer to the domain and need to manage its DNS settings. When creating a VM within an Azure virtual network, IP addressing is automatically configured, and the DNS is set to use the VNET DNS Server. However, we want our client computer to use the IP address of the Domain Controller as its DNS server. This is because, when Active Directory is installed on a server and it becomes a Domain Controller, a DNS service is also installed. For the client to join the domain, it must use the Domain Controller as its DNS server. The Domain Controller has information about our domain (e.g., mydomain.com). If the client uses the VNET DNS server, it will attempt to resolve mydomain.com via the internet and fail.
</p>
<br />

![image](https://github.com/user-attachments/assets/74c6ba13-873e-4bdd-a3b2-a2c012aa2a47)
![image](https://github.com/user-attachments/assets/03f2f733-3ce5-403f-8d57-695a95b58610)
<p>
Step 2: Navigate to the Client1 Virtual Machine -> Network settings -> click Network interface (ex: client 1582)
</p>
<br />

![image](https://github.com/user-attachments/assets/b99ccb39-4240-446c-acb3-2dc3c242120a)
<p>
Step 3: Settings -> DNS servers -> Check in Custom -> Enter Domain Controller (ex:DC1) private IP ADDRESS -> Save
</p>
<br />

![image](https://github.com/user-attachments/assets/f7a2c635-d1e0-4279-98da-77518dd31e56)
<p>
Step 4: Navigate to Client1 Virtual Machine -> Restart -> RDC into Client1 using labuser bc its not part of the domain yet.
</p>
<br />

![image](https://github.com/user-attachments/assets/0ca38c07-cc6f-4137-a96a-784f0a24e55b)
<p>
Step 5: Open command line -> ipconfig /all -> DNS Server should be 10.0.0.4 (Domain Controller private IP ADDRESS)
</p>
<br />

![image](https://github.com/user-attachments/assets/6e7a5687-2d21-449a-89c8-6306b4e8554f)
<p>
Step 6: Start -> System -> Rename this PC(adavanced) -> Change -> Check in Domain -> enter domain (ex:mydomain.com) -> Ok -> Enter the info of the Domain Administrator that we created (ex: mydomain.com\jerry_admin) -> Computer will restart
</p>
<br />

![image](https://github.com/user-attachments/assets/4a693033-9831-4cd6-849a-3944a1b5b40f)
<p>
Step 7: Now that Client1 is part of the domain, we can log into Client1 with our domain admin account.
</p>
<br />

![image](https://github.com/user-attachments/assets/181d4d0d-4c72-49c6-a512-9de6d970babd)
<p>
Step 8: To check, log into Client1 using admin username/password. 
</p>
<br />
<br />
<br />


<h2>Part 6: (Allow multiple "domain users" to log into client) Step: 1 </h2>
