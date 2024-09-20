<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Video Demonstration</h2>

- COMING SOON!

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>Deployment and Configuration Steps</h2>

<p>
For this lab, we are going to be creating two VMS that have the same VNET, we will be creating a Domain Controller (Windows Server 2022) and the other VM will be a Windows 10 OS. The Domain Controller will have Active Directory on it along with the 10,000+ users that we are going to create. Furthermore, we are going to join client-1 to the same DNS server as the Domain Controller so that all the users will have access to the Client-1 VM. 
</p>

<p>
![lab5-activedirectory](https://github.com/user-attachments/assets/174def96-6ff7-4d0a-bd2f-52cf513cf7c5)
</p>
<br />

<p>
After creating DC-1, you will need to change the DNS from dynamic to static. This is because whenever we have a server that is offering resources such as Active Directory we don't want DHCP to assign it an IP address. So, after it is changed to static we are going to use Remote Desktop to login into Client-1 and try to ping DC-1. At first, the ping isn't going to work and that is when we are going to use Remote Desktop to login into DC-1 and change the default ICMPv4 firewall that is placed within the server. You will need to enable both the ICMpv4 that are associated with the Core Networking Diagnostics group. Once both ICMPv4s are enabled you will see that it pings correctly on Client-1.
</p>
<p>
<img width="1430" alt="Screenshot 2024-09-03 at 11 12 18 AM" src="https://github.com/user-attachments/assets/c4e34551-3864-4d9d-b1dd-093e06c7dc08">
</p>
<p>
<img width="1415" alt="Screenshot 2024-09-03 at 12 38 15 PM" src="https://github.com/user-attachments/assets/230611cf-bcf9-4a4b-8b17-ef6357d76e83">
</p>
<p>
<img width="1001" alt="Screenshot 2024-09-03 at 12 38 53 PM" src="https://github.com/user-attachments/assets/74856b13-1f16-469c-9985-fba2926cb55b">
</p>
<br />

<p>
Now the next step in the lab is to go back into DC-1 and install Active Directory Domain Services. In the server manager click add roles and features and go forth with the installation. Make sure to set up a new forest and use the URL: mydomain.com... once you are done with the installation the VM will restart. When it asks you to log back in use mydomain.com\(username of VM) and the same password for that username.
</p>
<p>
<img width="945" alt="Screenshot 2024-09-03 at 2 40 06 PM" src="https://github.com/user-attachments/assets/e6b3167f-4a6e-4c73-bb21-3afda2e41f39">
</p>
<br />

<p>
You now should have Active Directory installed on your domain controller. The next steps now is to create an admin using your name and that is what we are going to use to login from here on out through DC-1 so remember the login and password. To navigate to this section search up Active Directory Users & Computers and once you are there create two organizational units (_EMPLOYEES & _ADMINS) within mydomain.com. Within the _ADMINS folder is where you are going to create this user using your name. To add permissions (right click the user you created and go to properties) once you are there navigate to memberof and assign Domain Admin to your user.
</p>
<p>
<img width="860" alt="Screenshot 2024-09-03 at 3 37 01 PM" src="https://github.com/user-attachments/assets/8d24d451-0f42-4735-8254-3b30a0269303">
</p>
<br />

<p>
Great! We are almost there... now since Active Directory is downloaded on our Domain Controller, we need to make the DNS on Client-1 the same as DC-1. So, that is what we are doing in the image below. Go into Client-1 VM, and go to DNS server tab and make it the same private IP address as DC-1 for me my DC-1 IP was 10.0.0.4. YOurs may be differnet so don't copy exactly what I have! Once you change it make sure to restart the VM and then proceed to login... From now you use the admin account you created to login to Client-1.
</p>
<p>
<img width="931" alt="Screenshot 2024-09-03 at 4 28 35 PM" src="https://github.com/user-attachments/assets/cb0a9e4a-7353-4f14-8019-497b37ecb568">
</p>
<p>
<img width="928" alt="Screenshot 2024-09-03 at 4 31 13 PM" src="https://github.com/user-attachments/assets/1b5a2d0f-98c3-4fc2-b8ca-2b28f178f21a">
</p>
<br />

<p>
Now we need to connect Client-1 to DC-1, in order to do so navigate to your system settings and right clicke rename this pc and then click change. From here you will need to type the DC-1 url we chose which was mydomin.com into (Domain:). Then it will ask you to enter your credentials for the VM so use the username and password that you typed in to create the VM. For example mine would be, mydomain.com\mekhilab5, password: MCcoursecareerslab5. After you enter the correct credentials your Client-1 VM will now be connected to DC-1!
</p>
<p>
![1](https://github.com/user-attachments/assets/3f4848f6-cf9c-4623-8da5-e96d7fd9bc9b)
</p>
<br />

<p>
This last step we will need to do for Client-1 is to open our system settings again and navigate to Remote Desktop. We need to give access to all the users we are going to create on DC-1 so that they can login on Client-1. So, that is what I am doing in the image below. Right click select users that can remotely access this pc and type in Domain users and click ok, this will grant all users the ability to login through Remote Desktop on Client-1.
</p>
<p>
<img width="910" alt="Screenshot 2024-09-03 at 4 43 12 PM" src="https://github.com/user-attachments/assets/dc7f1f0b-ed4e-4496-8ab6-de41257d9958">
</p>
<br />

<p>
Lastly, in DC-1 we are going to load up powershell ISE and we are going to use the code script seen below to generate 10,000+ random users. They will be located in our _EMPLOYEES organizational unit we created. The images below the code snippet is me picking a random user and then going back into Client-1 and logging in as that user.
</p>
<p>
<img width="598" alt="Screenshot 2024-09-03 at 4 49 41 PM" src="https://github.com/user-attachments/assets/fd15be27-b447-4d9b-a4ea-61f72626a673">
</p>

<p>
<img width="630" alt="Screenshot 2024-09-03 at 5 42 10 PM" src="https://github.com/user-attachments/assets/71843d31-cc11-4763-b0c3-5e5621e1bb6b">
</p>

<p>
<img width="1240" alt="Screenshot 2024-09-03 at 5 45 29 PM" src="https://github.com/user-attachments/assets/bf419bfc-0317-4107-b8f1-4b6b85582d09">
</p>
