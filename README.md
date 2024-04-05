# Failed RDP logs to IP geolocation information using Azure Sentinel

## Overview:
This project utilizes ***Azure Sentinel***, ***PowerShell***, and a ***third-party API*** to create a threat map. The map provides IP geolocation information extracted from logs of failed Remote Desktop Protocol (RDP) brute force attacks attempted on a live honeypot ***virtual machine (VM)***.

## Key tools and technologies:
- **Azure Sentinel**: A SIEM tool from Microsoft that enables us to capture real-time analytics and map cyber-attacks.
- **PowerShell**: A script designed to parse failed RDP attack logs from the Windows Event Viewer of the VM and interact with the IP geolocation API.
- **Virtual Machine**: Set up on Azure as a honeypot to attract, monitor, and analyze RDP brute force attacks.
- **IP Geolocation API (ipgeolocation.io)**: Provides geographic location based on the IP address of attackers.

## Project methodology:

- ### Phase One: Setting Up VM Honeypot and Log Analytics Workspace in Azure

  We begin by creating a new Virtual Machine (VM) in Azure to serve as our "honeypot." A honeypot is a decoy system or network designed to lure cyber attackers. It mimics legitimate systems to attract malicious activity, allowing organizations to monitor and study attackers' methods without risking real data or systems. For our honeypot, we will select an operating system commonly targeted by attackers; Windows servers are often a popular choice. We will then configure the networking for our VM. It's crucial for a honeypot to be accessible by potential attackers, so we will set up the network security group to allow inbound Remote Desktop Protocol (RDP) connections. With the networking configured, we will deploy the VM. Once Azure completes the deployment, our honeypot will be live and ready to attract attention from threat actors across the internet.

  Following the establishment of our operational honeypot, it's essential to implement a mechanism for collecting and analyzing its data. This is achieved by creating an Azure Log Analytics workspace and utilizing Microsoft Defender for Cloud to ensure all raw data is collected as logs.

  The next step in this phase is to connect the newly created Log Analytics workspace to our VM. By establishing this connection, the Log Analytics workspace becomes the designated destination for the VM logs, facilitating the collection of logs for analysis.

  This integration forms the backbone of our data collection strategy, enabling deep analysis and insight generation.

- ### Phase Two: Setting up Azure Setinel and configuring the VM

  Azure Sentinel is a cloud-native Security Information and Event Management (SIEM) service from Microsoft. It helps organizations collect, analyze, and respond to security events and threats across their entire enterprise, including on-premises and cloud environments. Azure Sentinel enables proactive threat hunting, automated response capabilities, and seamless integration with other Microsoft and third-party security tools, empowering organizations to enhance their overall security posture and effectively protect against cyber threats.

  To set up Sentinel for the project, we open Azure Sentinel from the Azure portal and add it to our existing Log Analytics workspace. Doing so enhances the workspace's capabilities by providing specialized security monitoring, detection, and response functionalities, transforming the Log Analytics workspace into a comprehensive SIEM solution.

  Next, we connect to our honeypot VM and disable the firewall settings to ensure that the VM is open to the internet. We can verify this by pinging the IP address of the system through the command prompt in the VM.

- ### Phase Three: 
