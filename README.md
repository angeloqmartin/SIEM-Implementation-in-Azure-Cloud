# SIEM-Implementation-in-Azure-Cloud

The central objective of this Microsoft SIEM in Azure Cloud project is to initiate the creation and deployment of Microsoft SIEM within the Azure Cloud environment. The primary focus is on enhancing cybersecurity by leveraging advanced threat detection capabilities and customized configurations. This involves deploying Microsoft Sentinel and integrating various methods, such as custom KQL (Kusto Query Language) analytics rules, to bolster defenses against emerging threats.

This project centers around monitoring the Microsoft Sentinel SIEM, conducting incident investigations, and executing remedial measures to minimize the impact of cybersecurity threats. The goal is to effectively manage risks and prevent potential recurrence, thus safeguarding the integrity of Azure-based infrastructure.

## Deployment

Using a straightforward method to create and deploy a custom Microsoft SIEM in the Azure Cloud by uploading the Microsoft Sentinel All-in-One configuration file available at GitHub - [Azure/Azure-Sentinel](https://github.com/Azure/Azure-Sentinel/tree/master/Tools/Sentinel-All-In-One).

Follow these steps to proceed with the deployment:

1. Access the Repository: Visit [Azure/Azure-Sentinel](https://github.com/Azure/Azure-Sentinel/tree/master/Tools/Sentinel-All-In-One) on GitHub.
2. Use the "Deploy to Azure" on the repository as shown below:
<br>
<img width="836" alt="• Azure user account with enough permissions to enable the desired connectors  See table" src="https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/d2ee467b-5b20-421d-97f5-a9138e22edfc">
<br>
3. This will redirect you to your Azure Portal "Custom deployment" page
<br>
<br>
<img width="959" alt="Screenshot 2023-11-29 at 5 48 51 PM" src="https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/e266b1fc-62ed-49ca-a829-885d0dca335d">
<br>
<br>
4. Configuration Setup: Review the detailed instructions provided in the repository's documentation for configuring Microsoft Sentinel to suit your specific needs.
<br>
<br>
5. Review + create

## View Logged Activity
<img width="962" alt="Screenshot 2023-11-29 at 6 27 16 PM" src="https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/816d1437-84e7-4d9b-93ff-726238ae955f"><br>

1. Access the logs section from your overview page. Here, you can execute queries using KQL to view logged activities, tracking details such as the action's performer (or Caller), and other essential properties crucial for investigation purposes.

<img width="955" alt="Microsoft Sentinel  Logs" src="https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/3c0c9af5-618b-46d4-9f68-d7f8ec2ecae9">

<br>
<br>
2. "AADNonInteractiveUserSignInLogs" query which checks interactive user log on, provides information on auth requirements, client usage, and location details 
<br>
<br>
	
![Microsoft Sentinel  Logs](https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/4393da27-8291-4b5d-b91b-4c01e5424607)

## Analytics Setting

<img width="964" alt="Microsoft Sentinel  Analytics" src="https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/d15502d0-385a-43a7-996e-d8281cca1ff7">
<br>
<br>
1. Within the Microsoft Sentinel Analytics settings, it's important to monitor high-security threats like file deletions. Effective management involves reviewing and adjusting settings for anomalies to minimize the occurrence of false positives.
<br>
<br>

![Microsoft Sentinel  Analytics](https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/b7f3b457-db5e-437f-878a-498c859b6fb6)

2. Engaging with User and Entity Behavior Analytics involves activating Playbook - AI (Artificial Intelligence) within the SIEM to detect and notify about atypical behavior (Microsoft Sentinel's UEBA).

<img width="902" alt="Screenshot 2023-11-29 at 10 30 29 PM" src="https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/a0fd4333-fdc7-45e4-ba93-bed7d03c21d8">

<img width="842" alt="Manage permissions" src="https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/422128ac-ab46-4a22-9073-75a8cf0ff03c">

## Create Watchlist

Watchlist allows data collection from external sources for correlation with events in the Microsoft Sentinel environment. Once established, utilize these watchlists in your search and detection processes.

<img width="1094" alt="Screenshot 2023-12-10 at 9 24 15 PM" src="https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/8dc5e943-28aa-4aec-94b4-5fd130e28f43">
<br>
<br>
1. To add a watchlist select "New"
<br>
<br>
<img width="623" alt="Screenshot 2023-12-10 at 9 32 48 PM" src="https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/ca6017e0-96be-4c6b-a84f-bfb1a7985438">
<br>
<br>
2. In this project, a CSV file was utilized to create a watchlist that verifies all outgoing Tor nodes' IP addresses.
<br>
<br>

![Watchlist wizard copy](https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/b68d9376-8bf7-4ad1-bd01-a9dc1c4f6516)

<img width="1215" alt="Screenshot 2023-11-29 at 11 03 27 PM" src="https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/de1130e0-57a8-4494-9117-07895a959788">

3. Make a Call to the watch with KQL with “_GetWatchlist('Tor-IP-Addr’)”

<img width="925" alt="Screenshot 2023-11-29 at 11 07 13 PM" src="https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/a9c44d40-9873-4e00-bb95-e4771b85a12d">

## Create Analysis Detection Rule

To create Analysis Detection Rules for Cybersecurity Threats navigate to Microsoft Sentinel > Configuration > Analytics > Create > Schedule Query Rule

1. Analytics rule wizard - Create a new Scheduled rule

<img width="852" alt="Analytics rule wizard - Create a new Scheduled rule" src="https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/273977d9-3eb0-46c9-bf38-6e9fc23d5e75">

2. Utilizing KQL to specify the date range for the following function that retrieves a list of IP addresses and stores it as a variable named TorNodes:

![I project TorIP = IpAddress); copy](https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/02f51624-7957-4ab9-9e3a-e5fd5ee6f097)

3. Review rules and create:

<img width="875" alt="Screenshot 2023-11-30 at 12 06 25 PM" src="https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/52608d01-bc86-4595-9e30-75e6a22a3c9e">

4. The new rule will appear under the Analytics section 

 ![Microsoft Sentinel  Analytics copy](https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/bbe2ffc0-13c2-4ce7-bb13-d7f3f4bfe2d9)

## Create a "New User"

Utilize the search bar at the top to find Active Directory or the current Microsoft Entrata. Next, access "Manage," select "Users," and create a "New User." Once the necessary rights, permissions, and roles have been configured proceed to log in as the user.

<img width="838" alt="Screenshot 2023-11-30 at 1 25 41 PM" src="https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/9f4e358f-36d7-42e9-a883-5321a4956105">

To initiate incidents within SIEM, user logins will be conducted through the Tor Browser. As a threat actor, the initial step involves establishing persistence by accessing My Account > Change Password.

![Password copy](https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/f1225476-95ea-4545-b3f4-a833e9d6afab)

Another action a threat actor could take is disabling multiple resources. Begin by going to the home page, then proceed to Resource Groups > Select your instance > Diagnostic Settings > Delete. Additionally, attempt to navigate to Microsoft Sentinel > Settings > Auditing and health monitoring > Configure diagnostic settings > Edit setting > Delete this setting.

<img width="986" alt="Diagnostic setting" src="https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/a1e05929-98b9-48ce-bf4b-a060c87f2a42">

## Review New Incidents

The actions conducted previously can be observed in Microsoft Sentinel | Overview (Preview) / (Manage) Incidents.

<img width="949" alt="Screenshot 2023-11-30 at 8 24 29 PM" src="https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/68984d50-c709-4b0f-9cc8-ca6a5cf3d3ef">

## Assign Incidents 

Incidents can be allocated to the user who spotted them or to someone else, facilitating an organized approach for users to handle multiple incidents concurrently. This can be achieved by selecting the specific incident, clicking on "Actions," and designating the "Owner." Additionally, this is where you can define the severity.

![Screenshot 2023-11-30 at 8 56 01 PM copy](https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/fad62461-5f76-4d3e-b31c-147443217fce)

## Investigate Cybersecurity Incidents in SIEM

For examining cybersecurity incidents in the SIEM, explore the "full details" page of the incident. This provides access to view Entities (such as users, IP addresses), Descriptions, events, timestamps, alerts, IPs, and additional information.


<img width="1440" alt="Screenshot 2023-11-30 at 9 24 27 PM" src="https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/12a494bd-086f-4768-bc10-39d72d21359c">

For further exploration of incidents, use the "Investigate" option located at the bottom of the incident's detailed page.

<img width="250" alt="Screenshot 2023-12-10 at 11 00 59 PM" src="https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/4af28be7-d162-467b-99c0-d5526d966e61">

This action will unveil log data, including usernames if relevant, and IP addresses.

![Screenshot 2023-11-30 at 9 29 52 PM copy](https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/c41ea16e-0af3-4a20-a773-291f0deb45b0)

Upon further investigation, it was revealed that the IP address 79.137.202.92 is associated with Tor exit nodes and potentially malicious activities.

<img width="607" alt="AbuselPDB » 79 137 202 92" src="https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/ef839dd7-c08f-48ef-8d8a-62d214ee649d">

By employing the query provided below, we can observe the user's Sign-in patterns mentioned in the incident.

SigninLogs<br>
｜ where UserPrincipaiName == "ShyGuy@angeloqmartingmail.onmicrosoft.com"

<img width="999" alt="Screenshot 2023-11-30 at 9 45 09 PM" src="https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/0eb79b98-2054-4f73-a6f6-44ca8f8e5900">

Take note of that the location field, where the country transitioned from US to DE within a matter of seconds.

![Screenshot 2023-11-30 at 9 47 47 PM copy](https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/afebd439-2d1c-4b56-8fc9-1020c2d7601d)

For a deeper investigation, navigate to Microsoft Sentinel > Incidents > Threat management > Entity behavior. This feature allows you to search for IPs, devices, or users to examine their complete activity, including actions like deletion or disabling of resources. This exploration will aid in identifying any relevant patterns or anomalies.

![Screenshot 2023-11-30 at 10 12 53 PM copy](https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/202d032b-f3da-42c4-ae7d-9196e88e60ba)

<img width="403" alt="Screenshot 2023-12-11 at 12 47 37 PM" src="https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/ca24210e-629e-4b8e-bed3-ec287a51a687">

## Remediation



1. Quarantine:
	- Immediately disable the compormised account "ShyGuy" by navigating to Microsoft Entra > Manage > Users > Click on user > Edit > Accout Status > Disable “Account enabled”
 - <img width="889" alt="ShyGuy" src="https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/07ba61ce-6f6e-482b-8fe9-725c75ae6be5">
3. Review User Permissions:
	- Conduct a thorough review of user accounts and permissions across the network and environment, particularly within the administrator's group. Remove unauthorized access and limit privileges to necessary functionalities.
5. Forensic Analysis:
	- Perform in-depth forensic analysis on the compromised host and associated network logs to understand the extent of the intrusion and identify potential points of entry.
6. Patch and Update Systems:
	- Ensure that all systems, including software and applications, are up-to-date with the latest security patches and configurations to mitigate known vulnerabilities.
7. Re-enable resources:
	- Re-enable any resources that were disableed. For example navigate to og Anltics workspace > select instance > monitor > diagnotic setting > +add dianogostic setting and microsoft sentinel > configuration settings > settings > auditing and health monitoring
 - <img width="883" alt="Diagnostic setting" src="https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/2982e8d8-4141-48fd-bd77-2463f8b12fe4">
- <img width="871" alt="Microsoft Sentinel  Settings" src="https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/17fffd1d-b711-4f6d-a7aa-62d1ed3d3f73">
8. Security Awareness Training:
	- Conduct security awareness training sessions for employees to educate them on identifying and reporting suspicious activities or security threats.
9. Incident Response Plan:
	- Review and update the incident response plan to include steps for handling similar security incidents promptly in the future.
10. Continuous Monitoring and Analysis:
	- Implement robust monitoring tools and practices to continuously analyze network traffic for any abnormal activities or potential threats.
11. Close Incident:
	- Following the implementation of remediation measures, proceed to close the incident(s) and add comments.
<img width="324" alt="Actions" src="https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/3f920b4f-5480-4f58-a738-a2b1304838c8">

These remediation actions should be carried out promptly and in coordination with the organization's IT security team to effectively mitigate the risks posed by the identified security breach.
