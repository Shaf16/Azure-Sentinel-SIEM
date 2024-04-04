# Failed RDP logs to IP geolocation information using Azure Sentinel

## Overview:
This project utilizes ***Azure Sentinel***, ***PowerShell***, and a ***third-party API*** to create a threat map. The map provides IP geolocation information extracted from logs of failed RDP brute force attacks attempted on a live honeypot ***virtual machine (VM)***.

## Key tools and technologies:
- **Azure Sentinel**: A SIEM tool from Microsoft that enables us to capture real-time analytics and map cyber-attacks.
- **PowerShell**: A script designed to parse failed RDP attack logs from the Windows Event Viewer of the VM and interact with the IP geolocation API.
- **Virtual Machine**: Set up on Azure as a honeypot to attract, monitor, and analyze RDP brute force attacks.
- **IP Geolocation API (ipgeolocation.io)**: Provides geographic location based on the IP address of attackers.

## Project methodology:

- ### Phase one - Setting up VM honeypot and log analytics workspace in Azure

  We start by creating a new Virtual Machine (VM) in Azure to serve as our "honeypot". A honeypot is a decoy system or network designed to lure cyber attackers. It mimics legitimate systems to attract malicious activity, allowing organizations to monitor and study the attackers' methods without risking real data or systems. For our honeypot, we will select an operating system commonly targeted by attackers. Windows servers tend to be a popular choice. We will then set up the networking for our VM. It is crucial for a honeypot to be accessible by potential attackers, therefore, we will configure the network security group to allow inbound RDP connections. With the networking configured, we will create and deploy the VM. Once the deployment is completed by Azure, our honeypot is live and ready to attract attention from threat actors across the internet.

  When the honeypot is up and running, it is crucial to have a mechanism in place for collecting and analyzing it's data. We do this by creating an Azure log analytics workspace and then using Microsoft Defender for Cloud to make sure that all raw data gets collected as logs.

  The next step in this phase is to connect this newly created log analytics workspace to our VM. This makes the log analytics workspace the destination for the logs from our VM and allows the collection of logs for analysis.

  This setup forms the backbone of our data collection strategy, enabling deep analysis and insight generation.

- ### Phase two - 
