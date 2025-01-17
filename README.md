# Basic Home Lab

## Objective

The objective of this basic home lab project was to create a controlled environment for testing new cybersecurity tools and techniques using Vultr, Kali Linux, and a Windows machine. The lab setup allowed for safe execution of malware samples to observe potential indicators of compromise without risking the security of personal or production systems. Additionally, by installing Sysmon and Splunk on the Windows machine, telemetry data was generated and analyzed, enhancing the understanding of system behavior during malware activity. This project aimed to develop practical skills in threat detection and response in a secure and isolated setting.

### Skills Learned


- **Malware Analysis**: Gained practical experience in safely executing and analyzing malware to identify indicators of compromise without affecting personal or production systems.
- **Tool Proficiency**: Developed skills in using cybersecurity tools like Sysmon and Splunk for system monitoring and telemetry data analysis.
- **Network Configuration**: Enhanced ability to set up and configure virtual machines and networks using Vultr, ensuring secure and isolated environments for testing.
- **Threat Detection**: Improved capability to detect and respond to threats through hands-on practice in a controlled lab setting.
- **Data Analysis**: Strengthened skills in generating and analyzing telemetry data to understand system behavior during security incidents.

### Tools Used

- **[Vultr](https://my.vultr.com/)**: Cloud infrastructure for creating and managing virtual machines.
- **Kali Linux**: Linux distribution used for penetration testing and security auditing.
- **Windows Machine**: Operating system used to run malware and generate telemetry.
- **Sysmon**: System Monitor tool for tracking system activity and creating logs.
- **Splunk**: Platform for searching, monitoring, and analyzing machine-generated data.

  ## Diagram of Basic Home Lab


  ![basic home lab diagram](https://github.com/user-attachments/assets/360754e5-e360-458d-8a25-69b67206d902)

The diagram illustrates the flow of a basic home lab setup for cybersecurity testing. The network begins with an internet connection, followed by a router that connects to Vultr, a cloud service provider. Within Vultr, a Virtual Private Cloud (VPC) is established, housing two machines: a Kali Linux machine with IP 10.0.0.4 and a Windows machine with IP 10.0.0.3. This setup allows the user to safely test malware and cybersecurity tools within an isolated environment. The Kali Linux machine is typically used for penetration testing and other offensive security tasks, while the Windows machine, equipped with tools like Sysmon and Splunk, is used for monitoring and analyzing security events. The VPC ensures that any potential threats or malware are contained within the lab environment, protecting the rest of the network from compromise.

## Step 1: Spin up Two VMs

* Use a cloud provider, like [Vultr](https://my.vultr.com/), or virtualization software like VirtualBox or VMware to create two virtual machines (VMs). One VM machine will be Kali Linux and the other machine will be a Windows machine.

![two vms](https://github.com/user-attachments/assets/e034d808-0eff-47eb-bcf6-c19948650f6c)

## Step 2: Download Sysmon and Splunk to Windows Machine
* Download [Sysmon](https://www.youtube.com/watch?v=uJ7pv6blyog) and [Splunk Enterprise](https://www.youtube.com/watch?v=iaBJ-PK8_RI)
* Sysmon is a powerful tool used specifically for monitoring detailed system activity on Windows machines.
* Splunk is a comprehensive platform for collecting, indexing, searching, and analyzing logs and events.
* Together, they work well to enhance an organization's ability to detect and respond to security incidents.
  


## Step 3: Configure VMs

* After making the VMs, it's time to create a Virtual Private Cloud (VPC). The VPC makes sure that the two VMs are able to communicate with each other over a private network and to secure the lab environment to contain malware.
* Vultr gives the option to make a VPC
  ![internal network 1](https://github.com/user-attachments/assets/01a92c92-6ade-49a8-88da-0bac1159e2cd)
* After creating the VPC, attach both VMs to the private network.
  
  ![kali linux private IP](https://github.com/user-attachments/assets/517d05f4-7812-4855-998c-e52b503c8e8a)
  - Kali Linux private IP address

  ![windows private IP](https://github.com/user-attachments/assets/bcdcedf5-de71-41e5-9f97-cc3b918d33a3)
  - Windows private IP address

* Now that both VMs are attached to the VPC, the next step is to configute the network on both so that they can communicate with one another.

* In the Kali Linux machine, get access to the command prompt and enter: sudo nano /etc/network/interfaces. This gives you access to the network interface config file for Kali Linux. The primary network interface is typically configured for DHCP to automatically obtain an IP address for internet connectivity. To enable communication with the Windows machine through the VPC, a static IP address must be assigned. Below the section labeled # The primary network interface, add a new section labeled # private network interface. eth1 is the secondary network interface. The IP address and netmask used are the same as the ones provided by the VPC.
  ![kali config](https://github.com/user-attachments/assets/f5c65880-7d23-4b85-b2c0-d74380625671)
* On the Windows machine, navigate to network connections and select IPv4 properties. DHCP is automatically configured just like in the Kali Linux instance. Unlike with Kali Linux, adding the static IP is more straigh-forward. Just select "Use the following IP address:" and then fill out the IP address and subnet mask provided by the VPC.

![windows config](https://github.com/user-attachments/assets/a8b78505-23bd-424c-ae14-ba94d290b3a2)

* When completed, ping the two VMs to make sure that connection is established.
![kali ping to windows](https://github.com/user-attachments/assets/183c3f0e-429d-4476-93e8-0a77f0597d71)
![window ping kali](https://github.com/user-attachments/assets/c27fbab1-d08f-4eef-a0ed-86611f6f61bc)

## Step 4: Make the Malware
* On the Kali Linux machine, open the terminal and type nmap -A followed by the IP address of the windows machine -Pn to see what ports are open.

![nmaps 1](https://github.com/user-attachments/assets/713a35be-150e-45f4-b90b-0ae2d47557d3)
![nmaps 2](https://github.com/user-attachments/assets/d6a2dd89-0335-42ee-93bf-86928596d895)

 - port 3389 is the Remote Desktop Protocol(RDP) this port being open leaves it vulnerable to a reverse TCP payload.

* To create the malware that will be used to attack the target machine, use msfvenom in Kali Linux.

![msfvenom](https://github.com/user-attachments/assets/ed6b0c93-bc1b-4afe-8c00-bd38c4abd2c4)

* Because the RDP port is open, I am going with the shell reverse TCP.

![msfvenom amazon giftcard](https://github.com/user-attachments/assets/03fdf43b-ca02-4a22-a304-2d10e3aa2a03)

* This command will generate malware using meterpreter's reverse TCP payload that will connect back to Kali Linux based on the lhost and lport. The default port from meterpreter is 4444. The file format (-f) will be exe and the name (-o) will be Amazon_giftcard.pdf.exe.
* Type ls to make sure the file exists. 

* Now that the malware has been created, it's time to open up a handler and configure the setting to make sure that the lhost and lport matches the reverse TCP payload.

![msfconsole](https://github.com/user-attachments/assets/48b34f4b-a995-4738-b133-569b2ab84a69)
![msfconsole 2](https://github.com/user-attachments/assets/73b79c84-a783-45c7-9cd3-1a4f4ff531e5)


* Afterwards, set up a http server on Kali Linux so the Windows machine can download the malware.
   - on Kali Linux, run the command python3 -m http.server 9999

## Step 5: Download and Run Malware

* On the Windows machine, turn off virus and threat protections in Windows Security. The malware that was created is easily thwarted by basic malware protections provided by Windows Security.

* Afterwards, navigate to the http server, download the malware, and run it.

![windows download malware](https://github.com/user-attachments/assets/00b8b109-32e3-4da3-8ed3-aba6a15c95b0)

* Open up command prompt and run the command nstat -anob to see if there is an established connection to the Kali machine.

![kali windows connection](https://github.com/user-attachments/assets/f04aff0f-ce2d-4a5f-93df-277cece06a90)

* Over on Kali, there should be an open shell in the handler with remote access to the Windows machine.

![kali windows connection 2](https://github.com/user-attachments/assets/202d20ac-27d8-47f9-806a-33e19f4ed1f0)

* Run a few commands to get information from the Windows machine. This will generate telemetry in Splunk.
![windows ip config from kali](https://github.com/user-attachments/assets/a7fbf149-591e-4be4-8f3c-d531c85ccb53)

## Step 6: Analyzing Logs

* After running a few commands from the Kali Linux machine head over to the Windows machine and log into Splunk.
* Splunk has a wide range of fields that can be used to analyze events.
  
  ![event details](https://github.com/user-attachments/assets/bdd70c07-099f-431d-a4e4-a02fd7526a48)

* From this image we can see that the Amazon_giftcard was the malware that triggered the event and that command prompt was the process used to get access to the host.
* To get more information, take the ProcessGuid and copy paste it into the search. Make a table with the queried information.

![table event final](https://github.com/user-attachments/assets/3a64f268-6ec4-44a7-bd0a-8b3ef1b1daf5)

* Here we can see the parentimage Amazon_giftcard.pdf.exe produced cmd.exe and it ran net user, net localgroup, and ipconfig.
