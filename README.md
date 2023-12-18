# SIEM Implementation in Azure Cloud

The objective of this project is to deploy a Microsoft SIEM (Security Information and Event Management) within the Azure Cloud environment. The focus is on enhancing cybersecurity through advanced threat detection capabilities and customized configurations. This involves deploying Microsoft Sentinel and integrating various methods, such as custom KQL (Kusto Query Language) analytics rules, to strengthen defenses against emerging threats.

## Deployment

**Steps for Deployment:**
1. **Access Repository:** Visit Azure/Azure-Sentinel on GitHub.
2. **Deploy to Azure:** Use the "Deploy to Azure" button on the repository.
3. **Configuration Setup:** Review detailed instructions in the repository's documentation for configuring Microsoft Sentinel to suit specific needs.

<img width="646" alt="Screenshot 2023-12-17 at 11 35 37 PM" src="https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/a6e23da5-f5fc-4c10-a33a-f39c0e2cdc6c">

## Viewing Logged Activity

1. Access the logs section to execute queries using KQL for viewing logged activities, tracking essential properties, and investigating incidents.

AzureActivity - returns the Activity log data 
```kusto
AzureActivity
```

This query checks interactive user logon and provides information on auth requirements, client usage, and location details 
```kusto
AADNonInteractiveUserSignInLogs
```

![Microsoft Sentinel  Logs](https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/4393da27-8291-4b5d-b91b-4c01e5424607)

## Analytics Settings

1. Monitor high-security threats like file deletions in the Microsoft Sentinel Analytics settings.
2. Activate User and Entity Behavior Analytics (UEBA) to detect atypical behavior using AI.

![Microsoft Sentinel  Analytics](https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/b7f3b457-db5e-437f-878a-498c859b6fb6)

## Creating Watchlist

1. Add a watchlist by selecting "New" and utilizing a CSV file for external data correlation.
2. Utilize watchlists in search and detection processes within Microsoft Sentinel.

<img width="1094" alt="Screenshot 2023-12-10 at 9 24 15 PM" src="https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/8dc5e943-28aa-4aec-94b4-5fd130e28f43">

![Watchlist wizard copy](https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/b68d9376-8bf7-4ad1-bd01-a9dc1c4f6516)

To use a watchlist in search query, write a Kusto query that uses the _GetWatchlist('watchlist-name') function
```kusto
_GetWatchlist('Tor-IP-Addr’)
```
<img width="925" alt="Screenshot 2023-11-29 at 11 07 13 PM" src="https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/a9c44d40-9873-4e00-bb95-e4771b85a12d">

## Analysis Detection Rule

Create scheduled query rules using KQL to specify criteria for threat detection.

<img width="852" alt="Analytics rule wizard - Create a new Scheduled rule" src="https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/273977d9-3eb0-46c9-bf38-6e9fc23d5e75">

This query specifies the data to be sought, retrieves a list of IP addresses, along with other associated fields, and stores it as a variable named TorNodes.
```kusto
let TorNodes = _GetWatchlist ('Tor-IP-Addr')
	| project TorIP = IpAddress) ;
SigninLogs
| where IPAddress in (TorNodes)
| where ResultType != 5026
| project
TimeGenerated,
Location,
IPAddress,
UserDisplayName,
UserPrincipalName,
UserId,
LocationDetails,
RiskState,
RiskLevelDuringSignIn,
AuthenticationRequirement,
ClientAppUsed,
ConditionalAccessPolicies
```

## Incident Handling

In the context of incident handling within this project, the following actions are simulated to understand and respond to potential threats effectively:

- **User Account Creation for SIEM Investigation:** Generating logs by creating a User Account in Azure specifically for SIEM investigation purposes.
  
- **Login Using the Tor Browser:** After setting the necessary rights, permissions, and roles, logging into the user account via the Tor browser to simulate threat actor actions.
  
- **Establishing Persistence:** Emulating a threat actor's actions by initiating persistence, beginning with changing the user account's password.
  
- **Resource Manipulation:** Attempting to disable and create resources within the Resource group /SEC-Monitor-Project/Diagnostic setting and navigating through Microsoft Sentinel settings to modify configurations.
  
- **Observing Incidents:** Observing and analyzing incidents within Microsoft Sentinel's Incidents section to understand the nature and severity of potential threats.
  
- **Incident Allocation and Management:** Allocating incidents to specific users, defining their severity, and managing them effectively using the Microsoft Sentinel interface.

![Screenshot 2023-11-30 at 8 24 29 PM copy](https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/fec91045-5bc8-42c9-8457-595602c46101)

## Investigation of Cybersecurity Incidents

During the investigation of cybersecurity incidents within Microsoft Sentinel, the following actions are conducted:

- **Observation of Incidents:** Monitoring and examining incidents recorded in Microsoft Sentinel's Incidents section to identify potential threats.
  
- **Incident Allocation and Severity Management:** Allocating incidents to specific users, defining their severity, and effectively managing them to ensure a prompt and organized response.
  
- **Detailed Incident Examination:** Viewing the "full details" of incidents to access information regarding Entities (users, IP addresses), Description, events, timestamps, alerts, IPs, and additional crucial data.
  
- **Checking Access IP for Malicious Activity:** Analyzing the accessed IP to verify potential associations with malicious activities. For instance, investigating if the IP address is linked to any malicious behavior or known Tor exit nodes.
  
- **Identification of Suspicious IPs:** Identifying suspicious IPs by examining specific details. For example, discovering that the access IP is 79.137.202.92, which could be linked to suspicious activities. Using external resources like “https://www.abuseipdb.com” to ascertain if the IP is associated with Tor exit nodes or potentially malicious behavior.

<img width="1440" alt="Screenshot 2023-11-30 at 9 24 27 PM" src="https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/12a494bd-086f-4768-bc10-39d72d21359c">

Edit the Query to examine the user's Sign-in behavior. Note the rapid country transition in the location field from US to DE within seconds.
```kusto
SigninLogs
| where UserPrincipalName == “ShyGuy@angeloqmartingmail.onmicrosoft.com”
```
![Screenshot 2023-11-30 at 9 47 47 PM copy](https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/afebd439-2d1c-4b56-8fc9-1020c2d7601d)

## Remediation Steps

Take prompt actions for remediation in case of security breaches:

1. **Quarantine:** Immediately disable the compromised account "ShyGuy" by navigating to Microsoft Entra > Manage > Users > Click on user > Edit > Account Status > Disable “Account enabled”
2. **Review User Permissions:** Conduct a thorough review of user accounts and permissions across the network and environment, particularly within the administrator's group. Remove unauthorized access and limit privileges to necessary functionalities.
3. **Forensic Analysis:** Perform in-depth forensic analysis on the compromised host and associated network logs to understand the extent of the intrusion and identify potential points of entry.
4. **Patch and Update Systems:** Ensure that all systems, including software and applications, are up-to-date with the latest security patches and configurations to mitigate known vulnerabilities.
5. **Re-enable resources:** Re-enable any resources that were disableed. For example, navigate to og Analytics workspace > select instance > monitor > diagnostic setting > +add diagnostic setting and Microsoft sentinel > configuration settings > settings > auditing and health monitoring
6. **Security Awareness Training:** Conduct security awareness training sessions for employees to educate them on identifying and reporting suspicious activities or security threats.
7. **Incident Response Plan:** Review and update the incident response plan to include steps for handling similar security incidents promptly in the future.
10. **Continuous Monitoring and Analysis:** Implement robust monitoring tools and practices to continuously analyze network traffic for abnormal activities or potential threats.
11. **Close Incident:** Following the implementation of remediation measures, proceed to close the incident(s) and add comments.

<img width="324" alt="Actions" src="https://github.com/angeloqmartin/SIEM-Implementation-in-Azure-Cloud/assets/37564935/3f920b4f-5480-4f58-a738-a2b1304838c8">

These remediation actions should be carried out promptly and in coordination with the organization's IT security team to effectively mitigate the risks posed by the identified security breach.
