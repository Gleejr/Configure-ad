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






<br />


<br />
