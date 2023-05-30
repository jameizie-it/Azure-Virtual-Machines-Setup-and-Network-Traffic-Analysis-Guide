<p align="center">
<img src="https://i.imgur.com/xDzGmCo.png" alt="Traffic Examination"/>
</p>

<h1>Azure Virtual Machines Setup and Network Traffic Analysis Guide</h1>
This step-by-step guide provides instructions for setting up Azure Virtual Machines and analyzing network traffic. It covers creating a resource group in Azure, creating Windows 10 and Linux (Ubuntu) virtual machines, observing ICMP, SSH, DHCP, DNS, and RDP traffic using tools like Wireshark, and concludes with closing the Remote Desktop connection and deleting the resource group and associated resources. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>Overview of Steps:</h2>

- Step 1: Create a Resource Group within Azure. <br>
- Step 2: Create a Windows 10 Virtual Machine (VM).<br>
- Step 3: Create a Linux (Ubuntu) VM.<br>
- Step 4: Observe ICMP Traffic.<br>
- Step 5: Re-enable ICMP Traffic.<br>
- Step 6: Observe SSH Traffic.<br>
- Step 7: Observe DHCP Traffic.<br>
- Step 8: Observe DNS Traffic.<br>
- Step 9: Observe RDP Traffic.<br>
- Step 10: Deletion

<h2>Actions and Observations</h2>

<!DOCTYPE html>
<html>
  
<body>
  <h1>Step-by-Step Guide: Setting up Azure Virtual Machines and Analyzing Network Traffic</h1>
 
  <h2>Step 1: Create a Resource Group within Azure</h2>
  <p>
    1. Sign in to the Azure portal.<br>
    2. Click on "Resource groups" in the left-hand menu.<br>
    3. Click on "Add" to create a new resource group.<br>
    4. Provide a name for the resource group and select the desired subscription.<br>
    5. Choose the appropriate region and click on "Review + Create."<br>
    6. Finally, click on "Create" to create the resource group.
  </p>
  
   <p>
  <img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
  </p>
  
  <h2>Step 2: Create a Windows 10 Virtual Machine (VM)</h2>
  <p>
    1. In the Azure portal, navigate to your resource group.<br>
    2. Click on "Add" to add a new resource.<br>
    3. Search for "Windows 10" in the Azure Marketplace and select the appropriate image.<br>
    4. Configure the VM settings, including the name (e.g., VM1), resource group (select the previously created one), image (Windows 10), and size (choose a suitable configuration, such as 2 vCPUs and 16 GB memory).<br>
    5. Create a username and password for the VM.<br>
    6. Ensure that the license box is checked and proceed to the next step.<br>
     7. Keep the default disk and network settings.<br>
    8. Click on "Create" to provision the Windows 10 VM.
  </p>
  
   <p>
  <img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
  </p>
  
  <h2>Step 3: Create a Linux (Ubuntu) VM</h2>
  <p>
    1. Follow the same steps as above to add a new resource within the same resource group.<br>
    2. Search for "Ubuntu" in the Azure Marketplace and select the appropriate image.<br>
    3. Configure the VM settings, including the resource group (select the previously created one), image (Ubuntu), and other desired specifications.<br>
    4. Instead of using an SSH public key, choose a password and make note of it.<br>
    5. Configure the networking settings to use the same virtual network (VNet) as the Windows VM.<br>
    6. Click on "Create" to provision the Ubuntu VM.
  </p>
  
   <p>
  <img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
  </p>
  
  <h2>Step 4: Observe ICMP Traffic</h2>
  <p>
    1. Use Remote Desktop to connect to the Windows 10 VM (for macOS, download Microsoft Remote Desktop and connect using the VM's IP address).<br>
    2. Disable privacy settings and accept the network connection.<br>
    3. Install Wireshark within the Windows 10 VM by following the installation steps.<br>
    4. Open Wireshark and ensure that the ethernet adapter is selected.<br>
    5. Click on the first blue icon (start capturing packets).<br>
    6. Apply a filter to display ICMP traffic only.<br>
    7. To enhance visibility, use the "Ctrl +" shortcut to zoom in.<br>
    8. Obtain the private IP address of the Ubuntu VM and attempt to ping it from the Windows 10 VM.<br>
    9. Observe the ping requests and replies within Wireshark.<br>
    10. From the Windows 10 VM, open the command line or PowerShell and ping a public website (e.g., www.google.com) to observe the traffic in Wireshark.<br>
    11. Initiate a perpetual/non-stop ping from the Windows 10 VM to the Ubuntu VM.<br>
    12. Restart the packet capturing by clicking the green icon in Wireshark (without saving the previous capture).<br>
    13. To ping continuously, use the command: ping private-ip -t.<br>
    14. The goal is to stop this continuous ping by disabling ICMP through the Network Security Group (NSG) in Azure.<br>
    15. Open the NSG associated with the Ubuntu VM and disable inbound ICMP traffic.<br>
    16. Access the inbound security rules, select the existing rules, and create a new rule to deny all ICMP traffic.<br>
    17. Back in the Windows 10 VM, observe the ICMP traffic in Wireshark and the ping activity in the command line.
  </p>
  
   <p>
  <img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
  </p>
  
  <h2>Step 5: Re-enable ICMP Traffic</h2>
  <p>
    1. Enable ICMP traffic for the NSG associated with the Ubuntu VM.<br>
    2. Allow ICMP in the VM's firewall settings.<br>
    3. Once again, observe the ICMP traffic in Wireshark and verify that the ping activity is working.<br>
    4. Stop the perpetual ping by pressing "Ctrl+C" in the command line.
  </p>
  
   <p>
  <img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
  </p>
  
  <h2>Step 6: Observe SSH Traffic</h2>
  <p>
    1. Filter Wireshark to display SSH traffic only.<br>
    2. From the Windows 10 VM, establish an SSH connection with the Ubuntu VM using its private IP address.<br>
    3. Enter the necessary credentials (username and password) for the SSH connection.<br>
    4. Within the SSH connection, execute commands and observe the SSH traffic in Wireshark.<br>
    5. To exit the SSH connection, type 'exit' and press Enter.
  </p>
  
   <p>
  <img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
  </p>
  
  <h2>Step 7: Observe DHCP Traffic</h2>
  <p>
    1. Filter Wireshark to display DHCP traffic only.<br>
    2. From the Windows 10 VM, attempt to renew the IP address using the command line (ipconfig /renew).<br>
    3. Observe the DHCP traffic appearing in Wireshark.
  </p>
  
   <p>
  <img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
  </p>
  
  <h2>Step 8: Observe DNS Traffic</h2>
  <p>
    1. Filter Wireshark to display DNS traffic only.<br>
    2. From the Windows 10 VM's command line, use nslookup to query the IP addresses of websites like google.com and disney.com.<br>
    3. Observe the DNS traffic displayed in Wireshark.
  </p>
  
   <p>
  <img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
  </p>
  
  <h2>Step 9: Observe RDP Traffic</h2>
  <p>
    1. Filter Wireshark to display RDP traffic only (tcp.port == 3389).<br>
    2. Observe the continuous stream of RDP traffic and discuss the reason for its constant transmission.
  </p>
  
   <p>
  <img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
  </p>
  
  <h2>Step 10: Closing</h2>
  <p>
    1. Close the Remote Desktop connection to the Windows 10 VM.<br>
    2. Delete the resource group created at the beginning of this guide.<br>
    3. Verify that the resource group and associated resources have been successfully deleted.
  </p>
</body>
</html>
