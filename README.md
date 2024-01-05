# azure-network
<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
Explore virtual networks and traffic analysis in a hands-on lab. <br />




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

- Part 1: Building Our Virtual Playground
- Part 2: Observing Network Traffic in Action



 <h2>Building Our Virtual Playground </h2>

Create a Resource Group: 
![Screenshot 2024-01-05 153346](https://github.com/Gsegura95/azure-network/assets/87348052/62fd8e5a-796b-4cbd-bcdd-54a77eb59a1c)
- In the Azure portal, navigate to Resource Groups.



![Screenshot 2024-01-05 153431](https://github.com/Gsegura95/azure-network/assets/87348052/2c6bf80f-b35e-4530-9e30-a86bfd3a7ae2)
![Screenshot 2024-01-05 153521](https://github.com/Gsegura95/azure-network/assets/87348052/78b5c193-c6a3-423e-982b-178e0427e105)

- Click "Create" and provide a name for your resource group.
- Select the appropriate region and click "Create".

<h2>Create the Windows 10 VM:</h2>


- In the Azure portal, search for "Virtual Machines".
- Click "Create" and select "Windows Server" as the image.
- Choose the appropriate version (e.g., Windows 10 Pro).
- Select the resource group you created earlier.
- Provide a name for the VM.
- Choose a size (e.g., Standard B2s).
- Under "Networking", create a new virtual network and subnet or select an existing one.
- Click "Review + create" and then "Create".

<h2>Create the Ubuntu VM</h2>


- Repeat the VM creation process, but select "Ubuntu Server" as the image.
- Provide a name for the VM.
- Choose the same virtual network and subnet as the Windows VM.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<h2>Observing Network Traffic in Action</h2>

Connect to the Windows VM:

- Once the VMs are deployed, use Remote Desktop to connect to the Windows VM.
- Install Wireshark on the Windows VM (if not already installed).
- Capture and Analyze Traffic:

Refer to Wireshark's Documentation for detailed instructions on capturing and analyzing different types of traffic.

Focus on:
- ICMP (ping): Send pings between VMs and observe the packets.
- SSH: Connect to the Ubuntu VM using SSH and capture the encrypted traffic.
- DHCP: Renew IP addresses of VMs and observe the DHCP process.
- DNS: Use nslookup to query domain names and capture DNS queries and responses.
- RDP: Initiate a remote desktop connection and observe the RDP traffic.
  
<h2>Experiment with Security Groups:</h2>

In the Azure portal, navigate to Network Security Groups.
Edit the rules for the network security group associated with the Ubuntu VM.
Try blocking ICMP traffic and observe the effect on ping requests.

Here are the Azure-specific steps.

1. Initiate a perpetual/non-stop ping:

In the Windows 10 VM's command prompt or PowerShell, type:
ping -t <private IP address of Ubuntu VM>
This will send continuous ping requests to the Ubuntu VM.

2. Disable incoming ICMP traffic in the Network Security Group:

In the Azure portal, navigate to Network Security Groups.
Find the NSG associated with the Ubuntu VM.
Edit the inbound security rules.
Add a new rule with the following settings:
Priority: A lower number than existing rules (e.g., 100)
Source: Any
Source port ranges: *
Destination: Any
Destination port ranges: *
Protocol: ICMP
Action: Deny
Save the rule.

3. Observe ICMP traffic in Wireshark and ping activity:

In Wireshark on the Windows 10 VM, observe the ICMP packets.
You should see ping requests being sent, but no replies being received.
In the command prompt or PowerShell, the ping should also show timeouts.

4. Re-enable ICMP traffic:

In the Azure portal, edit the inbound security rule for ICMP in the NSG.
Change the action from "Deny" to "Allow".
Save the rule.

5. Observe ICMP traffic again:

In Wireshark, you should now see ping replies being received.
The ping in the command prompt or PowerShell should also start showing successful replies.

6. Stop the ping activity:

In the command prompt or PowerShell, press Ctrl+C to stop the ping.

</p>
<br />




