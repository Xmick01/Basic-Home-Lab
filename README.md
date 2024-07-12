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

- **Vultr**: Cloud infrastructure for creating and managing virtual machines.
- **Kali Linux**: Linux distribution used for penetration testing and security auditing.
- **Windows Machine**: Operating system used to run malware and generate telemetry.
- **Sysmon**: System Monitor tool for tracking system activity and creating logs.
- **Splunk**: Platform for searching, monitoring, and analyzing machine-generated data.

  ## Diagram of Basic Home Lab 

  ![basic home lab diagram](https://github.com/user-attachments/assets/360754e5-e360-458d-8a25-69b67206d902)

The diagram illustrates the flow of a basic home lab setup for cybersecurity testing. The network begins with an internet connection, followed by a router that connects to Vultr, a cloud service provider. Within Vultr, a Virtual Private Cloud (VPC) is established, housing two machines: a Kali Linux machine with IP 10.0.0.4 and a Windows machine with IP 10.0.0.3. This setup allows the user to safely test malware and cybersecurity tools within an isolated environment. The Kali Linux machine is typically used for penetration testing and other offensive security tasks, while the Windows machine, equipped with tools like Sysmon and Splunk, is used for monitoring and analyzing security events. The VPC ensures that any potential threats or malware are contained within the lab environment, protecting the rest of the network from compromise.

## Step 1: Spin up Two VMs

