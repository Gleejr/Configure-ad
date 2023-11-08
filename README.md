<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Video Demonstration</h2>

- ### [YouTube: How to Deploy on-premises Active Directory within Azure Compute](https://www.youtube.com)

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


<p>
19. Switch back to the 1st virtual machine (DC-1), open up serber manager, and go to "add roles and features".
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









<br />


<br />
