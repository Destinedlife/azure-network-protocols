<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Video Demonstration</h2>

- ### [YouTube: Azure Virtual Machines, Wireshark, and Network Security Groups](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Creating a Resource Group
- Creating Windows and Linux virtual machines and virtual network.
- 
- 

<h2>Actions and Observations</h2>

![image](https://github.com/user-attachments/assets/9fda66f7-6832-4348-91e1-947bfeb1deff)

<p>
Sign into Azure Portal, from the home page navigate to resource groups. Give the resource Group a name and choose a region to host the resource group. *It's best practice to make everything that going inside the resource group to go to the same region"
  Then Click "review + Create" the click "create".
</p>
<br />

![step 2](https://github.com/user-attachments/assets/506597c8-33bc-4034-adf5-c89cf359e36c)

<p>
Navigate to Virtual machines from the homepage or the search bar. Click create and choose "Azure Virtual Machine". Then choose the resource group and region used in the last step. Name this virtual mmachine "Windows-vm"
<br />

![step 3](https://github.com/user-attachments/assets/758c1740-7585-4057-be3a-f3f03e70c2d3)

<p>
Next scroll down to image. This is where we choose our operating systems for our Virtual machine. For this virtual machine choose "windows 10 pro, ver. 22h2". Next for size choose an option with "2 vcpus". next scroll down to the Administrator account and create a user name and password. Then, write them down in a notepad for later. Lastly, under Licensing check " I confirm I have an eligible Windows 10/11 license with multi-tenant hosting rights."
</p>
<br />

![step 4](https://github.com/user-attachments/assets/2172626d-1f4a-4b62-aa86-102bf5d08e63)


<p>
Next go to the networking page. Here is where you can create a virtual network. Azure's default settings are good enough for the purpose of this tutorial, but for practice we're going to change the name of the network. Under "Network interface" for virtual network click create new. Then name it "Lab-vn" and click ok. then go to "Review + create" and click create.
</p>
<br />

![step 5](https://github.com/user-attachments/assets/3925577f-d333-4cf1-9cec-c6c7609c32c2)



<p>
Once the Windows-vm is deployed we'll create linux virtual machine. Go back to virtual machines page in Azure and hit create (You should see the Windows-vm listed there now). Choose the same resource group we created earlier (RG-Network-Activies). Next, name the virual machine "linux-vm" and choose the same region from before. The make the size, user name, and password the same as the Windows-vm. Click the check mark under Licensing.Click next until to you get the netorking page. Choose the virtual Network we created earlier (Lab-vn).
   Then Click "review + Create" the click "create".
</p>
<br />

<p>

</p>
<br />

