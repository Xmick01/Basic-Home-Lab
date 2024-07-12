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

## Step 2: Configure VMs

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
