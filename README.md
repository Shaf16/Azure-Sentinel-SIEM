# Failed RDP logs to IP geolocation information using Azure Sentinel

## Overview:
This project utilizes ***Azure Sentinel***, ***PowerShell***, and a ***third-party API*** to create a threat map. The map provides IP geolocation information extracted from logs of failed Remote Desktop Protocol (RDP) brute force attacks attempted on a live honeypot ***virtual machine (VM)***.

## Skills Learned:

- Azure Sentinel
- PowerShell
- Honeypot Deployment and Management
- Virtual Machine Deployment and Configuration
- SIEM Tool Implementation
- Log Analysis
- Threat Analysis and Visualization

## Key Tools and Technologies:
- **Azure Sentinel**: A SIEM tool from Microsoft that enables us to capture real-time analytics and map cyber-attacks.
- **PowerShell**: A script designed to parse failed RDP attack logs from the Windows Event Viewer of the VM and interact with the IP geolocation API.
- **Virtual Machine**: Set up on Azure as a honeypot to attract, monitor, and analyze RDP brute force attacks.
- **IP Geolocation API (ipgeolocation.io)**: Provides geographic location based on the IP address of attackers.

## Project Methodology:

- ## Phase One: Setting Up VM Honeypot and Log Analytics Workspace in Azure

  We begin by creating a new Virtual Machine (VM) in Azure to serve as our "honeypot." A honeypot is a decoy system or network designed to lure cyber attackers. It mimics legitimate systems to attract malicious activity, allowing organizations to monitor and study attackers' methods without risking real data or systems. For our honeypot, we will select an operating system commonly targeted by attackers; Windows servers are often a popular choice. We will then configure the networking for our VM. It's crucial for a honeypot to be accessible by potential attackers, so we will set up the network security group to allow inbound Remote Desktop Protocol (RDP) connections. With the networking configured, we will deploy the VM. Once Azure completes the deployment, our honeypot will be live and ready to attract attention from threat actors across the internet.

  Following the establishment of our operational honeypot, it's essential to implement a mechanism for collecting and analyzing its data. This is achieved by creating an Azure Log Analytics workspace and utilizing Microsoft Defender for Cloud to ensure all raw data is collected as logs.

  The next step in this phase is to connect the newly created Log Analytics workspace to our VM. By establishing this connection, the Log Analytics workspace becomes the designated destination for the VM logs, facilitating the collection of logs for analysis.

  This integration forms the backbone of our data collection strategy, enabling deep analysis and insight generation.

- ## Phase Two: Setting up Azure Setinel and configuring the VM

  Azure Sentinel is a cloud-native Security Information and Event Management (SIEM) service from Microsoft. It helps organizations collect, analyze, and respond to security events and threats across their entire enterprise, including on-premises and cloud environments. Azure Sentinel enables proactive threat hunting, automated response capabilities, and seamless integration with other Microsoft and third-party security tools, empowering organizations to enhance their overall security posture and effectively protect against cyber threats.

  To set up Sentinel for the project, we open Azure Sentinel from the Azure portal and add it to our existing Log Analytics workspace. Doing so enhances the workspace's capabilities by providing specialized security monitoring, detection, and response functionalities, transforming the Log Analytics workspace into a comprehensive SIEM solution.

  Next, we connect to our honeypot VM and disable the firewall settings to ensure that the VM is open to the internet. We can verify this by pinging the IP address of the system through the command prompt in the VM.

- ## Phase Three: Generating IP geolocation information from logs using PowerShell and third-party API

  A [PowerShell script](https://github.com/Shaf16/Azure-Sentinel-SIEM/blob/main/PowerShell%20Script%20for%20exporting%20logs) is designed to parse failed RDP attack logs from the Windows Event Viewer of the VM, and enrich these logs with geographic information of the attackers using a third-party API ([ipgeolocation.io](https://ipgeolocation.io/)). This script plays a crucial role in visualizing the global origin of cyber-attacks, leveraging Azure Sentinel for real-time analysis and mapping.

  The script operates in two parts; first, it scans the Windows event logs for failed RDP login attempts. For each failed attempt, it extracts the IP address of the potential attacker. Next, the script sends these IP addresses to the third-party API, which returns the geographical location corresponding to each IP address. The script logs this information for further analysis. Running this script in PowerShell automates the process of monitoring and logging the failed RDP attempts, along with the attacker's location.

<p align="center">
 <b> Snapshot of PowerShell script running with geolocation information as output</b>
<br />
  
  <img src="https://github.com/Shaf16/Azure-Sentinel-SIEM/assets/95363766/127be571-ccb5-4077-b7f4-b2596e98f3d4" alt="PowerShell Script" width="85%" height="85%">
</p>

- ## Phase Four: Creating a custom log and setting up the Threat Map in Sentinel

  A custom log is created in our Log Analytics workspace to link the failed RDP attack logs with geolocation information from our VM. Once the custom log is created and synced with the VM, we can view event viewer data displaying the failed RDP logs with geolocation details when querying the custom log in our workspace.

  Next, we navigate to Azure Sentinel and create a new workbook to generate our threat map. Using Kusto Query Language (KQL) within the workbook, we write a [query](https://github.com/Shaf16/Azure-Sentinel-SIEM/blob/main/KQL%20Query%20for%20Threat%20Map) that selects failed RDP attempts and extracts the IP addresses and geographic locations associated with these attempts from our custom log. We configure the visualization setting to display a map, providing a visual representation of attacks on our honeypot VM mapped across the globe. Each point on the map represents a failed attempt to breach our system, offering valuable insights into the global distribution of threats.

<p align="center">
 <b> Threat Map showing the distribution of attacks</b>
<br />

  <img src="https://github.com/Shaf16/Azure-Sentinel-SIEM/assets/95363766/3a9dfcf5-8d76-4ed6-98da-ce6c4d44a7e7" alt="Threat Map" width="85%" height="85%">
</p>

## Insight and Analysis:
As the honeypot VM exposes vulnerabilities to the internet, it quickly becomes a prime target for attackers worldwide. Analyzing the collected data reveals patterns, frequency, and geographical distribution of cyber-attacks, highlighting the global scale and nature of cyber threats. Certain regions exhibit a higher concentration of attacks, indicating areas where cyber threats are more prevalent or specific vulnerabilities are exploited extensively. By observing the frequency of attacks from specific IP addresses or ranges, repeat offenders can be identified, allowing us to understand their tactics and potentially block these persistent threats.

Utilizing Azure Sentinel to visualize and analyze security data equips us with critical insights for understanding and proactively addressing cyber threats. The honeypot VM not only attracted attackers but also underscores the essential role of robust cybersecurity measures. Moreover, it exemplifies how honeypots serve as invaluable tools for studying attacker behavior and fortifying defensive strategies against evolving cyber threats.
