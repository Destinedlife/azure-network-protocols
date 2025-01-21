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
- Observe ICMP Traffic
- Configure a Firewall [Network Security Group]

<h2>Actions and Observations</h2>

![image](https://github.com/user-attachments/assets/9fda66f7-6832-4348-91e1-947bfeb1deff)

<p>
Sign in to Azure Portal, and from the home page navigate to resource groups. Give the resource Group a name and choose a region to host the resource group. *It's best practice to make everything that goes inside the resource group go to the same region" Then, Click "review + Create" and then click "create".
</p>
<br />

![step 2](https://github.com/user-attachments/assets/506597c8-33bc-4034-adf5-c89cf359e36c)

<p>
Navigate to Virtual Machines (VM) from the homepage or the search bar. Click Create and choose "Azure Virtual Machine". Then choose the resource group and region used in the last step. Name this virtual machine "Windows-vm"
<br />

![step 3](https://github.com/user-attachments/assets/758c1740-7585-4057-be3a-f3f03e70c2d3)

<p>
Next, scroll down to "image". This is where we choose the operating systems for our Virtual machine. For this virtual machine choose "Windows 10 pro, ver. 22h2". Next, for size pick an option with "2 vcpus". Next, scroll down to the Administrator account and create a username and password. Then, write them down in a notepad for later. Lastly, under Licensing check " I confirm I have an eligible Windows 10/11 license with multi-tenant hosting rights."
</p>
<br />

![step 4](https://github.com/user-attachments/assets/2172626d-1f4a-4b62-aa86-102bf5d08e63)


<p>
Next, go to the networking page. Here is where you can create a virtual network. Azure's default settings are good enough for this tutorial, but for practice, we're going to change the name of the network. Under "Network interface" for virtual network click create new. Then name it "Lab-vn" and click ok. Then go to "Review + create" and click Create.
</p>
<br />

![step 5](https://github.com/user-attachments/assets/3925577f-d333-4cf1-9cec-c6c7609c32c2)



<p>
Once the Windows-VM is deployed we'll create a linux virtual machine. Go back to the virtual machines page in Azure and hit create (You should see the Windows-vm listed there now). Choose the same resource group we created earlier (RG-Network-Activies). Next, name the virtual machine "linux-vm" and choose the same region from before. They make the size, user name, and password the same as the Windows-vm. Click the check mark under Licensing. Click next until the networking page. Choose the virtual Network we created earlier (Lab-vn).
   Then Click "review + Create" the click "create".
</p>
<br />

![image](https://github.com/user-attachments/assets/a87cfc75-7fe1-49e7-9084-28ee124d6506)


<p>
**Bonus step at any point you feel like you want to take a break you can stop your virtual machine from running. Go to the virtual machine page in Azure. Then, select both of the virtual machines and then click stop. This will save money while the virtual machines are not in use a for long period without deleting them. When you are ready to use them again come back to this page and hit start.
</p>
<br />

![step 6](https://github.com/user-attachments/assets/1b8db5b9-60a8-4cfa-89f8-ea6f292aa422)

<p>
Once both VMs are deployed we are going to remotely control the windows-vm. To do this we are going to use the "Remote desktop connection" app, which is natively on all Windows computers ( you'll have to install this app if you're using a Mac). Next, go to the virtual machine page in Azure and find the IP address listed to the right of the Windows-vm. Copy it and paste it into the "computer" section of the remote desktop. Then click Show More, put in the user name you created earlier, and click Connect. Lastly, put in the password for the windows-vm in the Windows Security pop-up and click ok. Click yes on the next pop-up, set all the privacy settings to no, and click accept.
</p>
<br />

![step 7](https://github.com/user-attachments/assets/f22ff5a4-c2c3-4706-a2fa-4c6075175780)

<p>
Now that we are in the windows-vm we're going to analyze the network traffic of the computer using Wireshark. Inside the Windows-vm open Edge (skip any of the extra prompts that pop up) and go to: www.wireshark.org . Then click download and choose the Windows x64 installer. Once downloaded, run the installer. Keep clicking next until it says to install and hit install. Click "I agree" to Npcap setup and then click install> next> finished.
</p>
<br />

![step 8](https://github.com/user-attachments/assets/13121fa5-4805-4ad5-8135-7156c13ccef7)


<p>
 Once Wireshark is installed open it. In Wireshark, Click ethernet and at the top left corner click the shark fin. Now we can see all the network traffic happening inside the VM. Now we are going filter the traffic down to just ICMP traffic. In the Search bar at the top type "icmp". Now you shouldn't see any traffic coming in. Now we are going to ping the Linux-vm from the Windows-vm and observe the icmp traffic. In Azure, Open the Virtual machine page, click on the linux-vm, and find the private IP Address on the right under networking.
</p>
<br />

![step 9](https://github.com/user-attachments/assets/fbf521cd-a594-4583-96f7-308f343c00be)

<p>
  In Azure, Open the Virtual machine page, click on the linux-vm, and find the PRIVATE IP Address on the right under networking and copy it. Back in the windows-vm, open Powershell. We are going to use Powershell to ping the Linux-vm. In Powershell type "Ping (linux-vm's Private IP Address)" then hit enter. Back in Wireshark, we can now see we have ICMP activity.
</p>
<br />

![step 10](https://github.com/user-attachments/assets/4beb15d0-e337-4bd4-8580-fcc82808070a)

<p>
   Now we will see what happens when we set up a firewall (network security group) for the linux-vm and try to ping it. First, we are going to start a non-stop ping from windows-vm to the linux-vm. In the windows-vm in PowerShell type: "ping (linux-vm's private IP address) -t". This created a nonstop ping, which we can see in Wireshark. Now back in Azure go to the Virtual machines> linux-vm> network> network settings then click on "Linux-security-nsg" under Network security group. Then go to Settings > Inbound security rules then click add. Change the destination port ranges to "*", protocol to "ICMPv4", and priority to "290" then click add.
</p>
<br />

![step 11](https://github.com/user-attachments/assets/5784c9e8-8aba-4a32-82e6-b4803af0ee55)

<p>
  Now that the rule has been deployed we can see in Powershell that the request is being timed out now. Also, in Wireshark under the info section, the only activity being reported are requests and there are no replies. In Azure go back to the Linux-vm network security group inbound security rules and delete the rule. Once the rule is gone things should go back to normal. We can stop the ping. Go to Powershell and press "Control + C" to stop the ping. Then close Wireshark.
</p>
<br />

