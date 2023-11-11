<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Video Demonstration</h2>

- ### [YouTube: How to Deploy on-premises Active Directory within Azure Compute](https://www.youtube.com/watch?v=lzHRxxSmQXc)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>Deployment and Configuration Steps</h2>

<h3>Setup Resources in Azure</h3>

<p>
1. In the Azure portal, type in resource groups in the seach bar above and click on resource groups.
</p>

<p>
  
  ![2023-11-07_20-25-09](https://github.com/Gleejr/Configure-ad/assets/148407820/7cc33271-8449-4308-807e-c30cb75d85a6) 
</p>


<p>
2. Click create to create a new resource group.
</p>
  <p>
  
  ![image](https://github.com/Gleejr/Configure-ad/assets/148407820/12f10b7d-3861-4515-932b-ef475d904c35)
</p>


<p>
3. Enter a name for the resource group and pick a region for the resource group. Click review + create and create again. (Example AD-Lab Region is West US 3)
</p>
 
<p>
  <img width="687" alt="Screen Shot 2023-11-07 at 8 38 51 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/dcd3836d-38ec-4c55-8b46-fa69d78ef39a">
</p>


<p>
4. Once the resource group has been created, type in virtual machines in the search box above and click in virtual machines.
</p>

<p>
 <img width="888" alt="Screen Shot 2023-11-07 at 8 46 03 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/504f8572-b736-4ef7-8b51-4b23baf6b49e">
</p>


<p>
5. Click on "create a virtual machine hosted by Azure". 
</p>

<p>
  <img width="622" alt="Screen Shot 2023-11-07 at 8 50 42 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/650e51a1-27dd-436d-adb8-37db85bbc6bb">
</p>


<p>
6. Select the resource group that was created in step 2, enter a name for the virtual machine, select the same region as the resource group, and select Windows Server 2022 for the image. (Example name: DC-1)
</p>

<p>
  <img width="741" alt="Screen Shot 2023-11-07 at 8 55 16 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/3b63cbc1-50b0-484b-b973-1fabf00e3385">
</p>


<p>
7. Select "Standard_E_2s_v3 - 2 vCPUs 16 GiB memory" for the size and create a username and password. (Example username: labuser, password: Password1234)
</p>

<p>
  <img width="717" alt="Screen Shot 2023-11-07 at 9 02 03 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/332926f6-558c-459f-87d2-8107ae15eda6">
</p>


<p>
8. Click review + create and create again to the 1st virtual machine.
</p>

<p>
  <img width="282" alt="Screen Shot 2023-11-07 at 9 20 18 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/edbeace0-962d-4353-b7d2-ebc042b7cb01">
  <img width="363" alt="Screen Shot 2023-11-07 at 9 22 01 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/d98e55e4-cca2-43c8-91a9-1024c243600f">
</p>

<p>
9. Repeat the same steps to create the 2nd virtual machine. However this virtual machine's image will be Windows 10 pro.
</p>

<p>
  <img width="684" alt="Screen Shot 2023-11-07 at 9 28 02 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/ac993fa3-555b-485e-b719-a9d3d49e8657">
</p>

<p>
10. Go to the networking portion and validate that the 2nd virtual machine is one the 1st virtual machines virtual network.
</p>

<p>
  <img width="684" alt="Screen Shot 2023-11-07 at 9 34 26 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/29c679d7-cd8d-48e4-9f20-82775327657a">
</p>


<p>
11. Click review + create and create again to build the 2nd virtual machine.
</p>

<p>
12. Go to virtual machines, the 1st virtual machine (the machine running Windows Server/DC-1), go to networking, and go to the network interface.
</p>

<p>
  <img width="961" alt="Screen Shot 2023-11-07 at 9 42 44 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/b018ff89-98e6-442b-82c5-47e9169d1755">
</p>

<p>
13. Go to IP configurations and go to ipconfig1. (the Private IP address should currently show as dynamic)
</p>

<p>
  <img width="747" alt="Screen Shot 2023-11-07 at 9 45 31 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/38aa627f-74f1-4c76-81d5-673ef7a28dc9">
  <img width="1265" alt="Screen Shot 2023-11-07 at 9 47 09 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/2f856146-0281-4deb-90b3-ad53490125f3">
</p>

<p>
14. Change the allocation from "dynamic" to "static", click save, and refresh the the virtual machine.
</p>

<p>
  <img width="519" alt="Screen Shot 2023-11-07 at 9 52 05 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/55011ee6-c097-48cc-8be7-c49a1a03a5ca">
</p>

<p>
15. Grab the public IP address of the 2nd virtual machine (Client-1) running Windows 10 Pro and open remote desktop. Input the IP address, username, and password to take control of the virtual machine.
</p>

<p>
  <img width="920" alt="Screen Shot 2023-11-07 at 9 58 37 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/73ad9818-1d7a-4dbe-b6c7-73e7131d3f11">
  <img width="453" alt="Screen Shot 2023-11-07 at 9 59 53 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/a99935cf-b9fa-4d48-9d0d-67022709019c">
  <img width="662" alt="Screen Shot 2023-11-07 at 10 01 31 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/25d7140c-568c-4551-bec2-b54e957d6598">
</p>




<h3>Ensure Connectivity between the client and Domain Controller</h3>

<p>
15. Grab the private IP address of the 1st virtual machine (DC-1) running Windows Server, open the command prompt on the 2nd virtual machine (Client-1), and ping the private IP address of the 1st virtual machine (DC-1). (the request will time out because the 1st virtual machine's (DC-1) firewall is blocking ICMP traffic)
</p>

<p>
  <img width="1351" alt="Screen Shot 2023-11-07 at 10 09 21 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/9180650d-9d6d-46fb-b3f8-dfe109e6ef63">
  
  ![image](https://github.com/Gleejr/Configure-ad/assets/148407820/f238c677-7c5d-4ca6-af89-693c01da3877)
</p>


<p>
16. Grab the public IP address for the 1st virutal machine (DC-1), open remote desktop, input the public IP adress, and the username and password to take coontrol of the 1st virtual machine.
</p>

<p>
  <img width="1351" alt="Screen Shot 2023-11-07 at 10 14 17 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/6059021f-dae1-4c5e-b1e0-8467d0215f27">
  <img width="662" alt="Screen Shot 2023-11-07 at 10 16 55 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/b77a73dc-3a49-414f-bf9a-f5b6462d3765">
</p>


<p>
17. Go to start and type in "wf.msc".
</p>

<p>
  <img width="1440" alt="Screen Shot 2023-11-07 at 10 20 07 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/22eecde0-4a92-4ad2-8dd0-7e9ca9390411">
</p>

<p>
17. Go to inbound rules, select protocol, and find ICMPv4
</p>

<p>
  <img width="1440" alt="Screen Shot 2023-11-07 at 10 23 23 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/aceab3bc-efcf-4265-90cf-fff8829f6140">
</p>


<p>
18. Enable the 1st two ICMP Echo Request. Switch back to the 2nd Virtual machine (Client-1) and the request will now go through successfully and receive replies back.
</p>

<p>
  <img width="1136" alt="Screen Shot 2023-11-07 at 10 26 49 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/ec7075c8-ac7b-4325-86c9-778936e563bd">
  <img width="990" alt="Screen Shot 2023-11-07 at 10 30 14 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/fd1dda9a-3a77-4ba0-89fd-be49c9c14025">
</p>



<h3>Install Active Directory</h3>

<p>
19. Switch back to the 1st virtual machine (DC-1), open up server manager, and go to "add roles and features".
</p>

<p>
  <img width="1440" alt="Screen Shot 2023-11-07 at 10 35 15 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/efca79ef-d555-4afc-ab39-3c08d52c81ec">
</p>

<p>
20. Keep selecting next, select "Active Directory Domain Services", and select "add features".
</p>

<p>
  <img width="1440" alt="Screen Shot 2023-11-07 at 10 38 05 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/90ad805a-ccc4-4a18-b339-e884717b3185">
  <img width="414" alt="Screen Shot 2023-11-07 at 10 39 29 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/bc3c4ca5-d132-4835-a4aa-5b53554b9b12">

</p>

<p>
21. Keep clicking next until install shows at the bottom and then once it has installed select close.
</p>

<p>
  <img width="791" alt="Screen Shot 2023-11-07 at 10 42 16 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/ec07fee3-5c52-4e9f-a7a9-672744aaf077">
  <img width="788" alt="Screen Shot 2023-11-07 at 10 45 20 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/58e1ff7b-6546-4050-96a1-e4ddec9ee07e">
</p>


<p>
22. In top right corner (the notification tab), click the flag and then click "promote this server to domain controller".
</p>

<p>
  <img width="1265" alt="Screen Shot 2023-11-09 at 10 20 13 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/89d5ac2b-0699-431d-a450-425b0eab8ca6">
</p>


<p>
23. Select add a new forest, enter a root domain name (example: mydomain.com), and click next.
</p>

<p>
 <img width="808" alt="Screen Shot 2023-11-09 at 10 24 44 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/da748968-b741-48d1-8530-9bbf4d2d755a">
</p>


<p>
24. Create a password (Example Password1234) and keep clicking next. Once intall populates click install.
</p>

<p>
  <img width="775" alt="Screen Shot 2023-11-09 at 10 29 15 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/4de1c2b0-91e4-42c2-8fc3-24ee1b4c11a4">
  <img width="775" alt="Screen Shot 2023-11-09 at 10 38 45 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/108fcfa8-413e-4cc3-8e31-5dfa8ee9687d">
</p>


<p>
25. The virtual machine will restart. Open remote desktop and reconnect to the 1st virtual machine (DC-1).
</p>

<p>
 <img width="1440" alt="Screen Shot 2023-11-09 at 10 42 17 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/482bb603-0d3f-4d3b-9481-9fb44cf38c7a">
</p>


<p>
26. The 1st virtual machine (DC-1) is now a domain controller. Enter the root domain name and the password for the 1st virtual machine (DC-1). (example username: mydomain.com\labuser)
</p>

<p>
<img width="662" alt="Screen Shot 2023-11-09 at 10 52 54 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/bfa99078-101d-42f9-8255-848ec2f09f8e">
</p>



<h3>Create an Admin and Normal User Account in AD</h3>

<p>
27. Click on tools and select "Active Directory Users and Computers"
</p>

<p>
<img width="1440" alt="Screen Shot 2023-11-09 at 10 57 44 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/83eaa07e-7797-4e6c-9e6e-3877c0b6b31f">
</p>


<p>
28. Under "mydomain.com", create two organizational units "_Employees" and "_ADMINS". 
</p>

<p>
<img width="943" alt="Screen Shot 2023-11-09 at 11 01 31 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/ddb463a9-8733-4687-9108-a13198ce2496">
<img width="755" alt="Screen Shot 2023-11-09 at 11 08 58 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/f9e67d12-4611-481a-8165-2469ed20c023">
</p>

<p>
29. In admin, right click and select "new" and "users".
</p>

<p>
<img width="765" alt="Screen Shot 2023-11-09 at 11 11 48 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/bbeb356c-d371-4863-b9d6-d7a9f346136c">
</p>

<p>
30. Enter a name for the user and a user login (example name: jane doe, user login: jane_admin). Create a password and only check "password never expires". Click next and finish.
</p>

<p>
<img width="437" alt="Screen Shot 2023-11-09 at 11 15 24 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/53c8c62a-6686-4735-853d-f5b9d5566c1f">
<img width="444" alt="Screen Shot 2023-11-09 at 11 17 41 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/c2d2c39a-6d98-4713-bc9d-c03d6fd61246">
</p>

<p>
30. Right click on the user that was created in the previous step and select properties. Go to "member of" and click add.
</p>

<p>
<img width="753" alt="Screen Shot 2023-11-09 at 11 21 44 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/55dba63a-6f55-4f91-9586-92c37f7bc1ed">
<img width="410" alt="Screen Shot 2023-11-09 at 11 22 45 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/a36ce2b6-574d-4b42-8236-aee9008d4cfa">
</p>

<p>
31. Enter "domain" and click on check names. Select domain admins and click on OK. Click on OK again, click on apply, and click on OK.
</p>

<p>
<img width="743" alt="Screen Shot 2023-11-09 at 11 27 43 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/53e33f63-20b9-44a1-a65d-c4008188687e">
<img width="756" alt="Screen Shot 2023-11-09 at 11 28 37 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/2c03de18-528c-4cc8-964f-97a533cebd05">
</p>

<p>
32. Sign out of the 1st virtual machine (DC-1) and log back in as jane_admin. (example: mydomain.com\jane_admin)
</p>

<p>
<img width="662" alt="Screen Shot 2023-11-09 at 11 38 13 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/8f186d43-a93d-4405-ae22-49d9a4d624f8">
</p>



<h3>Join Client-1 to your domain (mydomain.com)</h3>

<p>
32. Go to the 1st virtual machine (DC-1) on Azure, networking, and copy the NIC private IP addreess.

<p>
<img width="1053" alt="Screen Shot 2023-11-09 at 11 46 45 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/ae9ba5e9-972e-459c-817a-47cae6d82b64">
</p>


<p>
33. Go to the 2nd virtual machine (Client-1) on Azure, clickn on networking, click on network interface, and click on DNS server. 

<p>
<img width="1054" alt="Screen Shot 2023-11-09 at 11 50 08 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/2e5a274b-a4bf-4576-9159-018a635a04e0">
<img width="1054" alt="Screen Shot 2023-11-09 at 11 52 48 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/244eace2-a23f-4872-9c01-2b4d9e9d44f7">
</p>

<p>
34. Change "inherit from virtual network" to "custom". Enter the private IP address for the 1st virtual machine (DC-1) and click save. Restart the 2nd virtual machine (Client-1).

<p>
<img width="1054" alt="Screen Shot 2023-11-09 at 11 55 57 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/188f614a-8b31-4d10-84e7-a1683624a2f6">
<img width="1054" alt="Screen Shot 2023-11-09 at 11 59 27 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/e7841bea-dd8d-498e-9a3b-09e309852b9f">
</p>


<p>
35. Log back into the 2nd virtual machine (Client-1) and open the command prompt. Type in "ipconfig /all" and the DNS server will be the same as the private IP address of the 1st virtual machine (DC-1).

<p>
<img width="984" alt="Screen Shot 2023-11-10 at 9 56 01 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/a74cbbd0-2dd7-4da3-917b-56c33a304a97">
</p>


<p>
36. In the start menu, go to settings, and go to "rename this PC(advanced)".
<p>
<img width="1440" alt="Screen Shot 2023-11-10 at 10 04 11 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/a90d634a-4d31-4f25-826d-e449ce64f980">
</p>


<p>
37. Under system properties select change, under member of select domain and enter mydomain.com, and enter the login for the admin that was created earlier. (Example jane_admin)
<p>
<img width="405" alt="Screen Shot 2023-11-10 at 10 08 11 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/ba19c3e7-cea0-44a5-a9e9-1ff117586e66">
<img width="334" alt="Screen Shot 2023-11-10 at 10 10 28 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/ca4fcae2-f03d-4e4f-a815-de8054df3204">
<img width="456" alt="Screen Shot 2023-11-10 at 10 11 29 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/8ac447d7-ddce-4bf8-be03-4b0b19c31ee9">
</p>


<p>
38. A message will pop up showing that it was a success. Restart the 2nd virtual machine (Client-1) and log in as the jane_admin.
<p>
<img width="309" alt="Screen Shot 2023-11-10 at 10 17 13 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/6e2bc3ee-e3d3-44a7-bf9b-2d3411de9585">
</p>



<h3>Setup Remote Desktop for non-administrative users on Client-1</h3>

<p>
39. Go to system, go to remote desktop, and click on "select users that can remotely access this pc"
<p>
<img width="1440" alt="Screen Shot 2023-11-10 at 10 27 42 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/623416fa-6510-4e49-8a51-72ffe1312485">
<img width="1440" alt="Screen Shot 2023-11-10 at 10 30 41 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/d31019fc-ef4d-466d-8f40-4c5472f8cda7">
</p>

<p>
39. Click on add, Type in "domain users", click on check names. Click on OK and OK again.
<p>
<img width="472" alt="Screen Shot 2023-11-10 at 10 36 08 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/b13cb4bd-a23c-4813-8224-0aba2b71aeeb">
</p>



<h3>Create a alot of additional users and attempt to log into client-1 with one of the users</h3>

<p>
40. Switch back to the 1st virtual machine (DC-1), open up windows powershell ISE, and run it as an administrator. 
<p>
<img width="1440" alt="Screen Shot 2023-11-10 at 10 49 13 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/dd82d30e-b510-4ab6-a27f-8edaa0890197">
</p>

<p>
41. Click on new script, input a script (the script will create many user that can be tested to login into Client-1) and select execute.
<p>
<img width="1440" alt="Screen Shot 2023-11-10 at 10 51 03 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/ee90a70d-edcd-4b09-9720-c855153a06e9">
<img width="1440" alt="Screen Shot 2023-11-10 at 10 55 40 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/534398b8-5cf5-466d-92a3-1efbf5e611a1">
</p>


<p>
41. Go back to Active Directory Users and Computers, go to _EMPLOYEES, and grab a random employee's name that was generated. Switch back to the 2nd virtual machine (Client-1) and login as the employee.
<p>
<img width="964" alt="Screen Shot 2023-11-10 at 11 06 54 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/3c34c3ae-22d6-4d73-b699-11ee38a181a3">
<img width="662" alt="Screen Shot 2023-11-10 at 11 10 58 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/b09ab25f-f7c7-42f4-ac6f-eda8862b5a22">
<img width="997" alt="Screen Shot 2023-11-10 at 11 12 13 PM" src="https://github.com/Gleejr/Configure-ad/assets/148407820/f71e022a-f5d6-4f0b-adae-2378fdaad13e">
</p>


<br />


<br />
