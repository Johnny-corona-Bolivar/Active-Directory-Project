# Active-Directory-Project

 ## Diagram


### 📝 Network Diagram Description

In the diagram, we can see that two servers (Active Directory and Splunk services) are connected to a switch with a preconfigured static IP. These servers are accessible from our Windows machine, which uses DHCP. 
All devices are connected to the switch, which in turn is connected to the router. Additionally, we have our Kali machine with a static IP configured.
We will install Atomic Red Team on Windows and generate alerts, based on the MITRE ATT&CK framework.

<img width="802" height="624" alt="image" src="https://github.com/user-attachments/assets/24cec5ee-93da-4867-988b-0917f47cb774" />


 ## 🔒 Active Directory Setup

To use Active Directory (AD), the **Active Directory Domain Services (AD DS)** role must be installed.  
After installation, the server must be promoted to a **Domain Controller**. Once this is done, it allows:

- **Authentication** using Kerberos  
- **Authorization** for the domain  

### AD DS Objects

AD DS can contain objects such as:

- **Users**  
- **Computers**  
- **Groups**  

Each object has attributes.  
**Example:**  
- User object: `Bob`  
  - First Name: Bob  
  - Last Name: Smith  

### Windows Image Creation

To create a Windows image, use:  
[Windows 10 Download](https://www.microsoft.com/en-ca/software-download/windows10)  

Steps:

1. Install the downloaded software.  
2. Choose whether to update the PC or create an ISO image.  
3. Click **Create ISO** and follow the steps.  
4. Install the ISO in VirtualBox.



## 📊 Splunk Server Set-Up

We will edit the settings to assign a **static IP address**.

<img width="647" height="73" alt="image" src="https://github.com/user-attachments/assets/834d18c2-3498-4e0b-85e8-cdd7689479ad" />

<img width="645" height="350" alt="image" src="https://github.com/user-attachments/assets/37c76133-26e1-45bf-a948-05559497a1e3" />

<img width="592" height="225" alt="image" src="https://github.com/user-attachments/assets/5d803443-25b4-4260-ad76-4f464a871623" />

<img width="698" height="298" alt="image" src="https://github.com/user-attachments/assets/179dc472-ed6e-464f-a545-8911535b064a" />



## 💻 Windows 10 set-up

We will configure an index called `endpoint` (you can name it as you wish, e.g., `desen`) to receive telemetry data and set up the corresponding port.

<img width="886" height="638" alt="image" src="https://github.com/user-attachments/assets/a0d0442b-9767-47bf-b12f-09285859e55a" />
<img width="886" height="600" alt="image" src="https://github.com/user-attachments/assets/d199787e-2de5-4216-82de-5d410758b3f8" />
<img width="886" height="358" alt="image" src="https://github.com/user-attachments/assets/bb1b4b68-3e8b-45c7-a25c-52071d4eb275" />
<img width="886" height="276" alt="image" src="https://github.com/user-attachments/assets/cee1a7e8-2906-4204-9877-627c06ebd80d" />
<img width="886" height="604" alt="image" src="https://github.com/user-attachments/assets/afae8190-dfdc-437c-8c20-6914731e5912" />
<img width="886" height="371" alt="image" src="https://github.com/user-attachments/assets/57c2d677-036c-4abd-91bc-f4439e374dfa" />



### The IP address belongs to the installed Splunk server from Windows-10.
<img width="786" height="653" alt="image" src="https://github.com/user-attachments/assets/0ebfd08d-2a02-483c-8ebc-d8960a1b4e60" />

### Sysmon Installation and Configuration

1. Download Sysmon:  
[Sysmon Download](https://learn.microsoft.com/es-es/sysinternals/downloads/sysmon)

2. Download the Sysmon configuration file by Olaf:  
[Sysmon Modular Repository](https://github.com/olafhartong/sysmon-modular)  
We will use the file:  
[sysmonconfig.xml](https://github.com/olafhartong/sysmon-modular/blob/master/sysmonconfig.xml)  
- Click **Raw** and save the file locally.

3. After extracting the Sysmon archive, copy its path.  
4. Open **PowerShell as Administrator** to continue with the installation and configuration.


We will navigate to the following path:

<img width="620" height="488" alt="image" src="https://github.com/user-attachments/assets/e3fce835-a138-436a-bd2b-daf412ecfc12" />


Install Sysmon:

<img width="620" height="389" alt="image" src="https://github.com/user-attachments/assets/ad5a8296-fbce-44ec-bd1d-3b536148fb28" />
<img width="659" height="413" alt="image" src="https://github.com/user-attachments/assets/f39eef84-f04c-4a7f-8150-096655f4ebbc" />



### Splunk Universal Forwarder Configuration

We will configure the `inputs.conf` file located at:  
`C:\Program Files\SplunkUniversalForwarder\etc\system\default`  

This file instructs the Splunk Forwarder where to send data, metrics, and other information. These data will be sent to our Splunk server.  

**Steps:**

1. Make a copy of the original file in:  
   `C:\Program Files\SplunkUniversalForwarder\etc\system\local`  
   - This ensures the original file is not lost. **Do not edit the original file**.

2. Edit the copy to configure the forwarder to send data related to:  
   - Applications  
   - Security  
   - System  
   - Sysmon  

This setup ensures the Splunk Forwarder sends the specified logs and telemetry to the Splunk server.

<img width="584" height="580" alt="image" src="https://github.com/user-attachments/assets/9eba8870-fc5b-4ffd-a4a3-fcf801bd29de" />


1. After saving the edited copy of `inputs.conf`, **restart the Splunk Forwarder service**.  
2. Complete the configuration in the Splunk server:  
   - Add the index `endpoint`  
   - Configure the corresponding port

<img width="886" height="129" alt="image" src="https://github.com/user-attachments/assets/3a2b1801-98d9-4c6e-bf84-72c2f78431fc" />
<img width="886" height="79" alt="image" src="https://github.com/user-attachments/assets/aa4c0aae-552e-4fd5-9476-1e01882419c4" />
<img width="886" height="245" alt="image" src="https://github.com/user-attachments/assets/5979a8b5-36b0-4c95-a2cb-52d8a206950f" />


## 🔒 Promoting Server to Domain Controller

We will now promote the server to a **Domain Controller**.

<img width="775" height="246" alt="image" src="https://github.com/user-attachments/assets/2fa28ad2-d6d6-41d4-a9c5-fc5266c18b4f" />
<img width="778" height="135" alt="image" src="https://github.com/user-attachments/assets/ab46bbd9-60bb-46d0-9e0e-e119dbec25c4" />
<img width="778" height="250" alt="image" src="https://github.com/user-attachments/assets/e2ea9dfb-1a0a-44e6-9590-48ba56d0a813" />
<img width="779" height="246" alt="image" src="https://github.com/user-attachments/assets/52b5326e-507f-4967-9474-107eb14fbff4" />
<img width="486" height="518" alt="image" src="https://github.com/user-attachments/assets/a980b833-0b66-4e5d-be9c-ed26820b109e" />
<img width="652" height="427" alt="image" src="https://github.com/user-attachments/assets/4afb8ba8-05a2-41b4-8772-1ff5256127cd" />

 Click on the warning triangle and select **"Promote this server to a Domain Controller"**.

<img width="615" height="398" alt="image" src="https://github.com/user-attachments/assets/b7144abb-641f-4bae-a1d1-aa0479691b50" />


 This will be the **Top-Level Domain**.

<img width="710" height="295" alt="image" src="https://github.com/user-attachments/assets/224816f4-f5c3-4393-8b41-78e045d5fe80" />

This is where all the server information is stored.  
It is a primary target for attackers because it contains hashes and other sensitive data.


<img width="730" height="332" alt="image" src="https://github.com/user-attachments/assets/022727de-5e91-4a72-afbc-a3d6102c9f82" />


Once completed, the server will restart, and the server will have been promoted to a **Domain Controller** with Active Directory installed.


<img width="736" height="272" alt="image" src="https://github.com/user-attachments/assets/21cb52b5-e4a9-4534-a4a6-9a450e017054" />

This section refers to managing **Users** and **Computers** within Active Directory.

<img width="387" height="730" alt="image" src="https://github.com/user-attachments/assets/878cd626-9f28-428b-824b-6fe9885abcd8" />

<img width="584" height="501" alt="image" src="https://github.com/user-attachments/assets/0c62b80e-2442-49d8-bbd0-09dacda2a237" />


To join our regular PC to the server's Domain Controller:

1. In the **Search Bar**, type `PC` → select **Properties** → …
   
   <img width="681" height="515" alt="image" src="https://github.com/user-attachments/assets/5347b8ef-3487-4a30-8953-a4266eaafd71" />

 Go to **Advanced System Settings** → **Computer Name**

 <img width="488" height="588" alt="image" src="https://github.com/user-attachments/assets/3263a822-d34f-4eef-849c-33e8a79b38a7" />

 Click **Change** → select **Member of:** and enter the **Domain Name**

 <img width="439" height="536" alt="image" src="https://github.com/user-attachments/assets/f752f2b1-c3c2-4291-a8c2-0e1837c309c5" />
 <img width="534" height="325" alt="image" src="https://github.com/user-attachments/assets/1c4d9b7d-9fa2-4736-8a1a-56cc8305d0b2" />

 When trying to add the PC, an error occurs because the PC cannot resolve the **DNS domain name**.  
We need to configure it manually by adding the **DNS of the server**.


<img width="542" height="685" alt="image" src="https://github.com/user-attachments/assets/19e5e3b3-ee03-45ef-b69d-019b4fca1707" />
<img width="634" height="570" alt="image" src="https://github.com/user-attachments/assets/ffd49431-51e6-48c3-8ffa-3a6d368fdd2b" />

 We will use the **server administrator account**.

<img width="662" height="369" alt="image" src="https://github.com/user-attachments/assets/ed829a1c-ee8a-4cf4-bf2e-151933a1d4df" />


Once restarted, we can log in using one of the created users.

<img width="565" height="386" alt="image" src="https://github.com/user-attachments/assets/b472dee9-c6ba-4220-b116-452f4a738b62" />

After completing all the previous steps, we will log in with our **administrator account** on the target PC and enable **RDP** so that users can access it remotely.

<img width="705" height="621" alt="image" src="https://github.com/user-attachments/assets/fee2e407-6e45-4725-ae08-f278ae86aa7d" />


## 📊 Install Atomic Red Team

- Log in as an administrator on the PC, and also launch PowerShell as Administrator

  <img width="734" height="322" alt="image" src="https://github.com/user-attachments/assets/a365297c-cbfb-4c4c-9b4f-dbe66eb6d6ba" />

 Exclude the **C:** drive folder from Windows Defender Antivirus.

 <img width="712" height="503" alt="image" src="https://github.com/user-attachments/assets/93906ee4-42ba-4e58-981d-afd5e622bccf" />
 <img width="731" height="465" alt="image" src="https://github.com/user-attachments/assets/4fa57eaf-d394-4d09-a257-eefa2dcc68d0" />


How to invoke Atomic Red Team on the **target PC** as **Administrator** from **PowerShell** (run as Administrator)

<img width="706" height="209" alt="image" src="https://github.com/user-attachments/assets/2caa6ea2-2990-45cf-93a0-9300ed78bbfd" />

telemtric

<img width="886" height="247" alt="image" src="https://github.com/user-attachments/assets/8f7a4138-a70c-4e6d-8b58-0865137d1883" />
<img width="886" height="52" alt="image" src="https://github.com/user-attachments/assets/edadbd06-f6ed-4909-99f7-1215d94afb3d" />



