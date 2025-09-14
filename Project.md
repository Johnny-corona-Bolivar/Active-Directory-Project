# Active-Directory-Project

 ## Diagram


📝 # Network Diagram Description

In the diagram, we can see that two servers (Active Directory and Splunk services) are connected to a switch with a preconfigured static IP. These servers are accessible from our Windows machine, which uses DHCP. 
All devices are connected to the switch, which in turn is connected to the router. Additionally, we have our Kali machine with a static IP configured.
We will install Atomic Red Team on Windows and generate alerts, based on the MITRE ATT&CK framework.

<img width="802" height="624" alt="image" src="https://github.com/user-attachments/assets/24cec5ee-93da-4867-988b-0917f47cb774" />


##  Active Directory Setup

To use Active Directory (AD), the **Active Directory Domain Services (AD DS)** role must be installed.  
After installation, the server must be promoted to a **Domain Controller**. Once this is done, it allows:

- **Authentication** using Kerberos  
- **Authorization** for the domain  

## AD DS Objects

AD DS can contain objects such as:

- **Users**  
- **Computers**  
- **Groups**  

Each object has attributes.  
**Example:**  
- User object: `Bob`  
  - First Name: Bob  
  - Last Name: Smith  

# Windows Image Creation

To create a Windows image, use:  
[Windows 10 Download](https://www.microsoft.com/en-ca/software-download/windows10)  

Steps:

1. Install the downloaded software.  
2. Choose whether to update the PC or create an ISO image.  
3. Click **Create ISO** and follow the steps.  
4. Install the ISO in VirtualBox.

